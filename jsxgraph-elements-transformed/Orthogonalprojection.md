

# Orthogonalprojection



## 描述

A point that is the orthogonal projection of a point onto a line.   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.Point](./JXG.Point.md).




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Point](./JXG.Point.md)**  
         ↳ **Orthogonalprojection**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Orthogonalprojection](./Orthogonalprojection.md#constructor)**  An orthogonal projection is given by a point and a line. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "orthogonalprojection".  
  

Possible parent array combinations are:

{[JXG.Line](../symbols/JXG.Line.html)} **p** {[JXG.Point](./JXG.Point.md)} **l**
:   The constructed point is the orthogonal projection of p onto l.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [0.0, 4.0]);
var p2 = board.create('point', [6.0, 1.0]);
var l1 = board.create('line', [p1, p2]);
var p3 = board.create('point', [3.0, 3.0]);

var pp1 = board.create('orthogonalprojection', [p3, l1]);
```
