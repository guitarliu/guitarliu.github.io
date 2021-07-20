---
Layout:post

title：＂Python开发AUTOCAD插件过程中利用AUTOCAD函数参数注意事项

date:2021-07-20

excerpt:"Cautions for Autocad Functions's paraneters during developing a PLugin with Python

tags:[AutoCAD,Software,PLugi,Cautions,Function Parameters,Python]

comments: ture
---

#### 注意事项——Python传参类型不同于VBA

```
RetVal ＝ object．IntersectWith（IntersectObject，ExtendOption)
```

此处函数一般用于求两条线或线与弧线的交点，其中Intersectobject为另一条直线段或弧线对象，ExtendOption为两直线交点的模式，具体有：

- acExtendNone:Does not extendeither object
  
  > 即两者在不延伸情况下的交点、

- acExtendThisEntity:Extends tle base object
  
  > 即基线延伸、另一条不延伸情况下的交点

- acExtendOtherEntity:Extends the object passed as an argument
  
  > 即除基线外的另一条线延伸，基线不延伸情况下的交点

- acExtendBoth：Extends both oblects
  
  > 即两条线均延伸情况下的交点
  
Python开发过程中，按照AUTOCAD自述文件ActiveX Reference Guide中的上述说明，如果给ExtendOption传递上述三个字符串参数，会出现无法捕捉两条线交点的情况，原因是上述函数适用于VBA开发；而Python开发中，ExtendOption的值对应上述三种情况依次为0，1，2，3而非字符串，具体代码如下：

```
From pyautocad import Autocad,APoint
acad = Autocad(create_if_not_exstsTrue)
startPt = APoint(x1, y1)
endPt = APoint(x2, y2)
LineObject =acad.ActiveDocument.AddLine(startPt,endPt)
centerPt = APoint(x3, y3)
radius = r
CircleObject = acad.ActiveDocument.AddCircle(centerPt, radius)
intPoints = LineObject.IntersectWith(CircleObject, 0)
print(intPoints)
```
