

# Parallelpoint



## 描述

Given three point, a parallel point is the point such that the four points form a parallelogram.   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.Point](./JXG.Point.md).




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Point](./JXG.Point.md)**  
         ↳ **Parallelpoint**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Parallelpoint](./Parallelpoint.md#constructor)**  A parallel point is given by three points. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "parallelpoint".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p3**
:   Taking the Euclidean vector v=p2-p1 the parallel point is determined by p4 = p3+v
  
  

{[JXG.Line](../symbols/JXG.Line.html)} **l** {[JXG.Point](./JXG.Point.md)} **p**
:   The resulting point will together with p specify a line which is parallel to l.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [0.0, 2.0]);
var p2 = board.create('point', [2.0, 1.0]);
var p3 = board.create('point', [3.0, 3.0]);

var pp1 = board.create('parallelpoint', [p1, p2, p3]);
```
