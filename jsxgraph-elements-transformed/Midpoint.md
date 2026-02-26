

# Midpoint



## 描述

Midpoint of two points.   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.Point](./JXG.Point.md).




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Point](./JXG.Point.md)**  
         ↳ **Midpoint**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Midpoint](./Midpoint.md#constructor)**  A midpoint is given by two points. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "midpoint".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](./JXG.Point.md)} **p2**
:   The constructed point will be in the middle of p1 and p2.
  
  

{[JXG.Line](./JXG.Line.md)} **l**
:   The midpoint will be in the middle of [JXG.Line#point1](../symbols/JXG.Line.html#point1) and [JXG.Line#point2](./JXG.Line.md#point2) of the given line l.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create base elements: 2 points and 1 line
var p1 = board.create('point', [0.0, 2.0]);
var p2 = board.create('point', [2.0, 1.0]);
var l1 = board.create('segment', [[0.0, 3.0], [3.0, 3.0]]);

var mp1 = board.create('midpoint', [p1, p2]);
var mp2 = board.create('midpoint', [l1]);
```
