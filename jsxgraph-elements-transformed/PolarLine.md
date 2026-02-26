

# PolarLine



## 描述

The polar line of a point with respect to a conic or a circle.   
  
*Defined in:*  [line.js](./src/src_base_line.js.md).   
Extends [JXG.Line](./JXG.Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
         ↳ **PolarLine**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[PolarLine](./PolarLine.md#constructor)**  The polar line is the unique reciprocal relationship of a point with respect to a conic. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "polarline".  
  

Possible parent array combinations are:

{JXG.Conic|[JXG.Circle](../symbols/JXG.Circle.html)} **el1** {[JXG.Point](./JXG.Point.md)} **el2**
:   or
  
  

{[JXG.Point](../symbols/JXG.Point.html)} **el1** {JXG.Conic|[JXG.Circle](./JXG.Circle.md)} **el2**
:   The result will be the polar line of the point with respect to the conic or the circle.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create the polar line of a point with respect to a conic
var p1 = board.create('point', [-1, 2]);
var p2 = board.create('point', [ 1, 4]);
var p3 = board.create('point', [-1,-2]);
var p4 = board.create('point', [ 0, 0]);
var p5 = board.create('point', [ 4,-2]);
var c1 = board.create('conic',[p1,p2,p3,p4,p5]);
var p6 = board.create('point', [-1, 1]);
var l1 = board.create('polarline', [c1, p6]);
```

```javascript
// Create the polar line of a point with respect to a circle.
var p1 = board.create('point', [ 1, 1]);
var p2 = board.create('point', [ 2, 3]);
var c1 = board.create('circle',[p1,p2]);
var p3 = board.create('point', [ 6, 6]);
var l1 = board.create('polarline', [c1, p3]);
```
