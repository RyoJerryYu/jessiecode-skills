

# IntersectionLine3D



## 描述

The line that is the intersection of two (infinite) plane elements in 3D.   
  
*Defined in:*  [linspace3d.js](./src/src_3d_linspace3d.js.md).   
Extends [JXG.Line3D](./JXG.Line3D.md).




## 继承关系

**[JXG.GeometryElement3D](./JXG.GeometryElement3D.md),JXG.GeometryElement**  
   ↳ **[JXG.Line3D](./JXG.Line3D.md)**  
         ↳ **IntersectionLine3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[IntersectionLine3D](./IntersectionLine3D.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "intersectionline3d".  
  

Possible parent array combinations are:

{[JXG.Plane3D](../symbols/JXG.Plane3D.html)} **el1** {[JXG.Plane3D](./JXG.Plane3D.md)} **el2**
:   The result will be the intersection of el1 and el2.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create the intersection line of two planes
var view = board.create(
    'view3d',
    [[-6, -3], [8, 8],
    [[-1, 3], [-1, 3], [-1, 3]]],
    {
        xPlaneRear: {visible:false},
        yPlaneRear: {visible:false},
        zPlaneRear: {fillOpacity: 0.2, gradient: null}
    }
);
var a = view.create('point3d', [2, 2, 0]);

var p1 = view.create(
   'plane3d',
    [a, [1, 0, 0], [0, 1, 0]],
    {fillColor: '#00ff80'}
);
var p2 = view.create(
   'plane3d',
    [a, [-2, 1, 1], [1, -2, 1]],
    {fillColor: '#ff0000'}
);

var i = view.create('intersectionline3d', [p1, p2]);
```
