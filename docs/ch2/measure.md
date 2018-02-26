# Map 文字避让

webGis 经常会遇到地图上标记文字问题，但是文字空间不够时，就会造成文字重叠显示混乱的现象，导致效果很不好，下面就说说解决方案。

## 文字避让

文字标注算法是 GIS 中最复杂（NP）的问题之一，本篇将介绍四分位模型算法。
关于文字在地图上的坐标是经纬度坐标根据墨卡托转换而来。

```
[
  {
    "name": "南京市",//要显示的文字
    "lon": 118.15,
    "lat": 32.89,
    "pixel": { //像素坐标
      "x": 968,
      "y": 736
    }
  }
]
```
- 求出每段文字矩形的实际大小

```
let ctx = this.container.getContext('2d'); // canvas 上下文
let width= ctx.measureText(name).width;
```
通过 measureText 得到每个文字的宽度，canvas 并没有直接获取文字的方法，那文字的高度如何的得到呢？

我们通过反复测试发现 canvas 的 font 等于 “13px Arial” 字体的时候，文字的高度大概是 fontSize 的 1.1 倍。

```
let fontSize = parseInt(ctx.font);
let height = fontSize * 1.1;
```
文字的宽度和高度得到后，我们就可以创建文字矩形的坐标系了。

所谓四分位模型，每一个标记点都有上下左右四个放文字的位子，如果左边放不下，那就放右边试试，还不行就放到下面试试，以此类推

创建右侧虚拟矩形坐标描述：

```
_getLeftAnchor() {
    let x = this.center.x - this.radius - this.textReact.width,
        y = this.center.y - this.textReact.height / 2,
        diam = this.radius * 2,
        maxH = diam > this.textReact.height ? diam : this.textReact.height; //矩形的高度
    return {
        x,
        y,
        minX: x,
        maxX: this.center.x + this.radius,
        minY: this.center.y - maxH / 2,
        maxY: this.center.y + maxH / 2
    };
}
```
以此类推，描述下面、左面、上面的虚拟矩形坐标。

- 判断碰撞

判断两个矩形是否覆盖相交，根据矩形的 minX,maxX,minY,maxY 判断相交，原理比较简单，代码如下：
```
/**
 * 判断分位是否相交
 * @param {*} target 
 */
 
isAnchorMeet(target) {
    let react = this.getCurrentRect(),
        targetReact = target.getCurrentRect();
    if ((react.minX < targetReact.maxX) && (targetReact.minX < react.maxX) &&
        (react.minY < targetReact.maxY) && (targetReact.minY < react.maxY)) {
        return true;
    }
    return false;
}
```
- 创建虚拟文字集合对象

```
let labels = pixels.map((val) => {
    let radius = val.pixel.radius + this.style.normal.borderWidth; //圆点半径
    return new Label(val.pixel.x, val.pixel.y, radius, fontSize, byteWidth, val.name);
});
```
递归遍历虚拟文字集合、判断是否与其他相交，如果有相交就移动当前文字位子，直到不相交为止。当找不到合适位置时，就选择隐藏当前文字。

```
do {
    var meet = false; //本轮是否有相交
    for (let i = 0; i < labels.length; i++) {
        let temp = labels[i];
        for (let j = 0; j < labels.length; j++) {
            if (i != j && temp.show && temp.isAnchorMeet(labels[j])) {
                temp.next();
                meet = true;
                break;
            }
        }
    }
} while (meet);
```

- 绘画文字

```
labels.forEach(function (item) {
    if (item.show) { //是否显示
        let pixel = item.getCurrentRect();
        ctx.beginPath();
        ctx.fillText(item.text, pixel.x, pixel.y);
        ctx.fill();
    }
});
```