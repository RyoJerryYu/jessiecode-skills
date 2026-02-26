

# Normal



## 描述

A normal is the line perpendicular to a line or to a tangent of a circle or curve.   
  
*Defined in:*  [line.js](./src/src_base_line.js.md).   
Extends [JXG.Line](./JXG.Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
         ↳ **Normal**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Normal](./Normal.md#constructor)**  A normal is a line through a given point on an element of type line, circle, curve, or turtle and orthogonal to that object. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "normal".  
  

Possible parent array combinations are:

{[JXG.Line](../symbols/JXG.Line.html)|[JXG.Circle](../symbols/JXG.Circle.html)|[JXG.Curve](../symbols/JXG.Curve.html)|[JXG.Turtle](../symbols/JXG.Turtle.html)} **o** {[JXG.Point](./JXG.Point.md)} **p**
:   The constructed line contains p which lies on the object and is orthogonal to the tangent to the object in the given point.
  
  

{[Glider](./Glider.md)} **p**
:   Works like above, however the object is given by [JXG.CoordsElement#slideObject](./JXG.CoordsElement.md#slideObject).


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a normal to a circle.
var p1 = board.create('point', [2.0, 2.0]);
var p2 = board.create('point', [3.0, 2.0]);
var c1 = board.create('circle', [p1, p2]);

var norm1 = board.create('normal', [c1, p2]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[point](./Normal.md#point)**  Attributes of helper point of normal. |




### {[Point](./Point.md)} **point**

Attributes of helper point of normal.
  
*Defined in:*  [options.js](./src/src_options.js.md).
