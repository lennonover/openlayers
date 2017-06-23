# 一个地图简单的组成

- Map(ol.map)

  它可以说是整个地图的大脑和一个容器的作用，负责将其它模块组合在一起，它是所有模块的入口。

- View(ol.view)

  一个 Map 必须包含一个 View，它是初始化地图的必备的三要素之一，主要是控制地图与人的交互，如地图显示中心、进行缩放、调节分辨率、地图的旋转等控制。

- Layer(ol.layer)

  Layer 它是初始化地图的第二个必要条件(第三个是HTML标签)，它是一个数组，所以说可以有一个或者多个 layer 。
  对于多个 layer 时他们是重叠在一起，相互之间互不干扰的。

- Source(ol.source)

  Source 数据源它是和 layer 一一对应，提供图层加载的数据源。

- Control(ol.control)

  Control 它是地图空间的控制类，比如地图放大缩小等等，可以根据此类扩展自己业务组件。

- Interaction(ol.interaction)

  它和 Control 区别是 Control 的触发都是一些可见的 HTML 元素触发，如按钮、链接等；而 interaction 交互功能都是一些设备行为触发，都是不可见的，如鼠标双击、滚轮滑动等，手机设备的手指缩放等.
