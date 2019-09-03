---
layout: post
title: "matrix tool"
categories: tool
---

# Matrix Tool 使用说明

## 主要用途

​        通过**矩阵**的方式给物体之间添加带动关系，并可以通过参数来设置影响的权重，

包含了矩阵的**创建**，**修改**，**导入导出**，**管理**和**转化**

[TOC]

## 矩阵的创建

### Global 

> 全局关联控制，不拆分到具体的每一个属性

![matrixTool_golbal](https://raw.githubusercontent.com/shabbySilence/shabbySilence.github.io/master/images/matrixTool/matrixTool_golbal.png)

**1 ， 2， 3  **  选择器， 可以点击选择是否关联对应的 translate ，rotate ， sale

**4**  选择器，设置选择被关联的物体是否仍被父层级控制（默认效果同约束）

**5** 选择 **控制物体** 加选 **被控制物体** ，添加1对1 的关联 (同1对1添加约束效果)（1对1效果与**6** 比，节点更简化）

**6**  选择 **控制物体们** 加选 **被控制物体** ，添加多对1 的关联 (同多对1添加约束效果)

**7，8**  选择 **控制物体** 加选 **被控制物体** ，添加关联（transform变换属性都为默认值），可以选择 **SDK** 同时控制

> （SDK ： set Driven Key  ， sdk物体 代指 可以跟控制器产生**同样控制效果**的辅助控制物体）

**9 ， 10 ** 在生成的matrix 控制，选择被控制物体是否受父层级控制 ，选择**被控制物体**执行

**11**  选择**被控制物体**， 移除对应添加的matrix 关联

**12** 导入 matrix  数据信息

**13** 选择**被控制物体** ， 导出matrix信息

**14** 选择 **点约束** 或 **父子约束** 或 **方向约束** 或 **缩放约束** ， 替换为 Matrix 关联方式

**15 ** 导入约束 数据信息

**16** 选择 **14** 中提到的约束类型的节点，**导出** 约束 数据信息

***

功能**14**动图展示：



![matrix_Global](https://raw.githubusercontent.com/shabbySilence/shabbySilence.github.io/master/images/matrixTool/matrix_Global.gif)

***

### Part 

> 拆分到具体的每一个属性，进行控制

![matrixTool_Part](https://raw.githubusercontent.com/shabbySilence/shabbySilence.github.io/master/images/matrixTool/matrixTool_Part.png)

**1**  选择要加载的**控制物体**（可以多选，**1** 和**2**可多选，  不可同时多选）

**2** 选择要加载的**被控制物体**

**3** 如何有SDK物体，则加载SDK 物体， 可以多选。1或2 多选的情况下 通过 *SDK 方式确定对应SDK 物体

**4 ,5,6 ** 同**Global**  中对应按钮功能

**7**  点击按钮执行命令，添加partMatrix

**8**  选中**被控制物体** ， 镜像 Matrix Weight （如果基于x轴正负方向添加了对称设置）

**9**  选中**被控制物体**，移除添加在此物体上的所有matrix关系

**10** 选中**控制物体**，加选**被控制物体**，移除 控制物体对被控制物体的 影响

**11，12 **  partMatrix 数据信息的导入导出

***



## 矩阵的管理

### P_Manager

> 对场景中的matrix 信息，查找，检索，修改，删除等系列操作界面画

![matrixTool_P_Manager](https://raw.githubusercontent.com/shabbySilence/shabbySilence.github.io/master/images/matrixTool/matrixTool_P_Manager.png)



**操作方案A:**

选择被关联物体，通过按钮**2**，加载到**3**中，点击**3**中条目可以直接在**1**跟**5** 中显示出对应的控制物体和 **matrix Weight Group** ，选择5中条目 可以执行对应 **7，8，10** 操作 **（在Part部分中是选择被关联的物体执行）** ，**1**中右键可以针对性的删除具体条目的影响

**操作方案B:**

直接点击按钮4 列出场景中所有的**matrix Weight Group** ，可以通过**6** 进行检索，

找到对应的weight Group 直接执行 **7, 8 ,10** 



***

## 矩阵的转化

### P_Conversion

> 通过计算matrix weight  ， 模拟一些复杂的变形效果实现精细化控制
>
> 此方案为曲线的模拟，解决曲线，甚至曲面无法解决的旋转缩放控制

![matrixTool_P_Conversion](https://raw.githubusercontent.com/shabbySilence/shabbySilence.github.io/master/images/matrixTool/matrixTool_P_Conversion.png)

**1** 选择控制曲线的所有控制器（同时也是生成控制矩阵的控制器）加载

**2** 设置是否选择控制器的上层级作为sdk控制

**3** 指定控制器具体属性进行采样取值

**4** 设置控制器采样偏移的数值

**5** 选择具体的最多蒙皮骨骼的相应层级 的物体 作为被关联的物体 加载

**6 ，7 ，8**  选择器

**9**  蒙皮骨骼对应最高层级的组的后缀

**10** 执行操作 

***

具体操作动图展示：

![matrix_conversion](https://raw.githubusercontent.com/shabbySilence/shabbySilence.github.io/master/images/matrixTool/matrix_conversion.gif)



> 只转化的旋转和缩放部分，位移的带动为默认的曲线
>
> 故控制器旋转时，轴心一直在曲线上

