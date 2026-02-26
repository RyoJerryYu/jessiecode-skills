

# Perpendicular



## 描述

A perpendicular is a line orthogonal to a given line, through a given point not on the line,   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [Segment](./Segment.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
      ↳ **[Segment](./Segment.md)**  
            ↳ **Perpendicular**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Perpendicular](./Perpendicular.md#constructor)**  A perpendicular is a composition of two elements: a line and a point. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "perpendicular".  
  

Possible parent array combinations are:

{[JXG.Line](../symbols/JXG.Line.html)} **l** {[JXG.Point](./JXG.Point.md)} **p**
:   The perpendicular line will be orthogonal to l and will contain p.


### Throws

- Throws: {Error} If the elements cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a perpendicular
var p1 = board.create('point', [0.0, 2.0]);
var p2 = board.create('point', [2.0, 1.0]);
var l1 = board.create('line', [p1, p2]);

var p3 = board.create('point', [3.0, 3.0]);
var perp1 = board.create('perpendicular', [l1, p3]);
```
