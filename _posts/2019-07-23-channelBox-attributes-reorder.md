---
layout: post
title: "channelBox attributes reorder"
categories: tool
---

# 通道栏自定义属性的顺序调整

#### 通道栏中的属性顺序经常会需要调整
#### 手动操作的极限步骤是依次删除对应属性然后撤销操作

***
### 我们这里通过with 来实现上下文管理，即 退出with循环前要执行 cmds.undo() 这个方法
---
#### 有父属性的自定义属性不能单独删除，兼容了复合属性的顺序调整
***
![image](https://raw.githubusercontent.com/shabbySilence/shabbySilence.github.io/master/images/20190723_attributeReorder.gif)


---
### talk is cheap show you the code

``` python
from contextlib import contextmanager
import maya.cmds as mc
import pymel.core as pm
import maya.mel as mel

@contextmanager
def undo():
    try:
        yield
    finally:
        mc.undo()
@contextmanager
def restoreSelection():
    sel = mc.ls(sl=1)
    try:
        yield
    finally:
        mc.select(sel)
class ReOrderAttr():
    def __init__(self):
        pass
    def getAtrName(self):
        sel = mc.ls(sl=True)
        if not sel:
            return
        history = mel.eval("channelBox -q  -selectedHistoryAttributes  $gChannelBoxName")
        main = mel.eval("channelBox -q  -selectedMainAttributes  $gChannelBoxName")
        nameList = []
        if history:
            for attr in history:
                fullName = '{}.{}'.format(sel[0], attr)
                longNameAttr = mc.attributeName(fullName, l=True)
                longName = '{}.{}'.format(sel[0], longNameAttr)
                nameList.append(longName)
        elif main:
            for attr in main:
                for n in sel:
                    fullName = '{}.{}'.format(n, attr)
                    longNameAttr = mc.attributeName(fullName, l=True)
                    longName = '{}.{}'.format(n, longNameAttr)
                    nameList.append(longName)
        else:
            nameList = sel
        return nameList
    #
    def orderAttrList(self,object=''):
        orderDict={}
        allAttrs = pm.PyNode(object).listAttr(k=True,ud=True)
        for n , i in enumerate(allAttrs):
            attr = i
            if i.isChild():
                attr = i.getParent()
            orderDict[str(attr)] = n
        orderList = sorted(orderDict.items(),key = lambda k : k[1])
        attrList = [i[0].split('.')[1] for i in orderList]
        return  attrList
    #
    def reorderAttr(self,obj, attr, direction=1):
        allAttrs = self.orderAttrList(object=obj)
        fullAttr = pm.PyNode('{}.{}'.format(obj,attr))
        if fullAttr.isChild():
            attr = fullAttr.getParent().split('.')[1]
        index = allAttrs.index(attr)
        operations = len(allAttrs) - (index + direction) % len(allAttrs)
        for n in range(operations):
            with restoreSelection(), undo():
                pm.deleteAttr(obj, at=allAttrs[index])
                if n == 0:
                    index += direction
                    index %= len(allAttrs)
            allAttrs = self.orderAttrList(object=obj)
    #
    def attrMove(self,direction ='upper'):
        attrList = self.getAtrName()
        if len(attrList) != 1:
            return
        obj = attrList[0].split('.')[0]
        attr = attrList[0].split('.')[1]
        if direction =='upper':
            direction =-1
        elif direction =='lower':
            direction = 1
        self.reorderAttr(obj, attr, direction=direction)
#
if __name__ == '__main__':
    attr = ReOrderAttr()
    attr.attrMove(direction='upper') # 'lower'
```



