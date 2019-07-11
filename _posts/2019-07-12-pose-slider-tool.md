---
layout: post
title: "pose slider tool"
categories: tool
---

### 发布一个业余时间改写的工具 pose slider tool。
> 原工具是目前 Sony Pictures Imageworks 的 lead rigger  Mike Cole 在2015年为DT出的一款pyqt4教程。

### 顾名思义 pose的滑动调节，可以快速的进行pose切换，摆脱重复的拖动手柄或在时间滑条上重复k帧。
***
#### 改写为pyside2格式 可以在maya2017 之后版本运行。
#### 改写的过程中 除了QtGui的布局迁移到QtWidgets外，PyQt4的旧式的信号和槽不再被支持。
#### 因此以下用法在PyQt5(同pyside2)中已经不能使用。
- QObject.connect()
- QObject.emit()
- SIGNAL()
- SLOT()

---
### github地址 [poseSliderTool][poseSliderTool] 
[poseSliderTool]: https://github.com/shabbySilence/poseSliderTool


