

# IntersectionCircle3D



## 描述

The circle that is the intersection of two elements (plane3d or sphere3d) in 3D.   
  
*Defined in:*  [circle3d.js](./src/src_3d_circle3d.js.md).   
Extends [JXG.Circle3D](./JXG.Circle3D.md).




## 继承关系

**[JXG.Curve3D](./JXG.Curve3D.md),JXG.GeometryElement**  
   ↳ **[JXG.Circle3D](./JXG.Circle3D.md)**  
         ↳ **IntersectionCircle3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[IntersectionCircle3D](./IntersectionCircle3D.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "intersectioncircle3d".  
  

Possible parent array combinations are:

{[JXG.Sphere3D](../symbols/JXG.Sphere3D.html)} **el1** {[JXG.Sphere3D](../symbols/JXG.Sphere3D.html)|[JXG.Plane3D](./JXG.Plane3D.md)} **el2**
:   The result will be the intersection of el1 and el2.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create the intersection circle of two spheres
var view = board.create(
    'view3d',
    [[-6, -3], [8, 8],
    [[0, 3], [0, 3], [0, 3]]],
    {
        xPlaneRear: {fillOpacity: 0.2, gradient: null},
        yPlaneRear: {fillOpacity: 0.2, gradient: null},
        zPlaneRear: {fillOpacity: 0.2, gradient: null}
    }
);
var a1 = view.create('point3d', [-1, 0, 0]);
var a2 = view.create('point3d', [1, 0, 0]);

var s1 = view.create(
   'sphere3d',
    [a1, 2],
    {fillColor: '#00ff80'}
);
var s2 = view.create(
   'sphere3d',
    [a2, 2],
    {fillColor: '#ff0000'}
);

var i = view.create('intersectioncircle3d', [s1, s2]);
```
