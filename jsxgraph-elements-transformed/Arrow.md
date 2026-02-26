

# Arrow



## 描述

A segment with an arrow head. This element is just a wrapper for element [Line](./Line.md) with [Line#straightFirst](../symbols/Line.html#straightFirst) and [Line#straightLast](../symbols/Line.html#straightLast) properties set to false and [Line#lastArrow](./Line.md#lastArrow) set to true.   
  
*Defined in:*  [line.js](./src/src_base_line.js.md).   
Extends [JXG.Line](./JXG.Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
         ↳ **Arrow**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Arrow](./Arrow.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "arrow".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|array} **point1** {[JXG.Point](./JXG.Point.md)|array} **point2**
:   Parent elements can be two elements either of type [JXG.Point](./JXG.Point.md) or array of numbers describing the coordinates of a point. In the latter case the point will be constructed automatically as a fixed invisible point.
  
  

{Number} **a** {Number} **b** {Number} **c**
:   A line can also be created providing three numbers. The line is then described by the set of solutions of the equation a\*x+b\*y+c\*z = 0.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create an arrow providing two points.
  var p1 = board.create('point', [4.5, 2.0]);
  var p2 = board.create('point', [1.0, 1.0]);
  var l1 = board.create('arrow', [p1, p2]);
```
