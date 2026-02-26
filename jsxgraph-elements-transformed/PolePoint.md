

# PolePoint



## 描述

This element is used to provide a constructor for the pole point of a line with respect to a conic or a circle.   
  
*Defined in:*  [point.js](./src/src_base_point.js.md).   
Extends [JXG.Point](./JXG.Point.md).




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Point](./JXG.Point.md)**  
         ↳ **PolePoint**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[PolePoint](./PolePoint.md#constructor)**  The pole point is the unique reciprocal relationship of a line with respect to a conic. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "polepoint".  
  

Possible parent array combinations are:

{JXG.Conic|[JXG.Circle](../symbols/JXG.Circle.html)} **el1** {[JXG.Point](./JXG.Point.md)} **el2**
:   or
  
  

{[JXG.Point](../symbols/JXG.Point.html)} **el1** {JXG.Conic|[JXG.Circle](./JXG.Circle.md)} **el2**
:   The result will be the pole point of the line with respect to the conic or the circle.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create the pole point of a line with respect to a conic
var p1 = board.create('point', [-1, 2]);
var p2 = board.create('point', [ 1, 4]);
var p3 = board.create('point', [-1,-2]);
var p4 = board.create('point', [ 0, 0]);
var p5 = board.create('point', [ 4,-2]);
var c1 = board.create('conic',[p1,p2,p3,p4,p5]);
var p6 = board.create('point', [-1, 4]);
var p7 = board.create('point', [2, -2]);
var l1 = board.create('line', [p6, p7]);
var p8 = board.create('polepoint', [c1, l1]);
```

```javascript
// Create the pole point of a line with respect to a circle
var p1 = board.create('point', [1, 1]);
var p2 = board.create('point', [2, 3]);
var c1 = board.create('circle',[p1,p2]);
var p3 = board.create('point', [-1, 4]);
var p4 = board.create('point', [4, -1]);
var l1 = board.create('line', [p3, p4]);
var p5 = board.create('polepoint', [c1, l1]);
```
