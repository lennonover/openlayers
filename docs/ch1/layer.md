# Layer 详解

- ol.layer.base

  一个虚基类，只用于让子类型继承和实现，自身不能实例化。主要功能是对 矢量地图数据 和 栅格地图数据的可视化表达。图层的外观，主要与数据渲染方式有关，与数据的来源关系不大。

  它包含连个子类，他们是用来实例化的。

  - ol.layer.Group
  - ol.layer.Layer

  初始化参数


  | 名称    | 参数类型     | 说明     |
  | :------------- | :-------------| :------------- |
  |opacity|	number 或者 undefined	|透明度，默认为 1 ，即完全透明|
  |visible|	boolean 或者 undefined	|是否可见，默认为 true|
  |extent|	ol.Extent 或者 undefined	|图层渲染的区域，即浏览器窗口中可见的地图区域。extent 是一个矩形范围，格式是[number, number, number, number] 分别代表 [left, bottom, right, top] 。如果没有设置该参数，图层就不会显示|
  |zIndex|	number 或者 undefined	|图层的层级，默认0|
  |minResolution|	number 或者 undefined	|图层可见的最小分辨率，当图层的缩放级别小于这个分辨率时，图层就会隐藏|
  |maxResolution|number 或者 undefined	|图层可见的最大分辨率，当图层的缩放级别等于或超过这个分辨率时，图层就会隐藏|

  支持的事件


  | 事件名   | 说明     |
  | :------------- | :------------- |
  |change (ol.events.Event)| 统一属性发生变化事件|
  |change:extent (ol.Object.Event)|extent发生变化事件|
  |change:maxResolution (ol.Object.Event)|maxResolution发生变化事件|
  |change:minResolution (ol.Object.Event)|minResolution发生变化事件|
  |change:opacity (ol.Object.Event)|opacity发生变化事件|
  |change:visible (ol.Object.Event)|visible发生变化事件|
  |change:zIndex (ol.Object.Event)|zIndex发生变化事件|
