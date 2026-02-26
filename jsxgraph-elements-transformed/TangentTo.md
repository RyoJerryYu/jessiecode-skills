

# TangentTo



## 描述

One of the two tangent lines to a conic or a circle through an external point.   
  
*Defined in:*  [line.js](./src/src_base_line.js.md).   
Extends [JXG.Line](./JXG.Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
         ↳ **TangentTo**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[TangentTo](./TangentTo.md#constructor)**  Construct the tangent line through a point to a conic or a circle. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "tangentto".  
  

Possible parent array combinations are:

{JXG.Conic|[JXG.Circle](../symbols/JXG.Circle.html)} **conic** {[JXG.Point](./JXG.Point.md)} **point** {Number} **[number=0]**
:   The result will be the tangent line through the point with respect to the conic or circle.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var c = board.create('circle', [[3, 0], [3, 4]]);
 var p = board.create('point', [0, 6]);
 var t0 = board.create('tangentto', [c, p, 0], { color: 'black', polar: {visible: true}, point: {visible: true} });
 var t1 = board.create('tangentto', [c, p, 1], { color: 'black' });
```

```javascript
var p = board.create('point', [0, 6]);
 var ell = board.create('ellipse', [[-5, 1], [-2, -1], [-3, 2]]);
 var t0 = board.create('tangentto', [ell, p, 0]);
 var t1 = board.create('tangentto', [ell, p, 1]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[point](./TangentTo.md#point)**  Attributes for the intersection point of the conic/circle with the polar line of the tangentto construction. |
|  | **[polar](./TangentTo.md#polar)**  Attributes for the polar line of the tangentto construction. |




### {[JXG.Point](./JXG.Point.md)} **point**

Attributes for the intersection point of the conic/circle with the polar line of the tangentto construction.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[JXG.Line](./JXG.Line.md)} **polar**

Attributes for the polar line of the tangentto construction.
  
*Defined in:*  [options.js](./src/src_options.js.md).
