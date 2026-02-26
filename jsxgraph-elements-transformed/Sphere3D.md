

# Sphere3D



## 描述

A sphere in a 3D view. A sphere consists of all points with a given distance from a given point. The given point is called the center, and the given distance is called the radius. A sphere can be constructed by providing a center and a point on the sphere or a center and a radius (given as a number or function). If the radius is a negative value, its absolute value is taken.   
  
*Defined in:*  [sphere3d.js](./src/src_3d_sphere3d.js.md).   
Extends [JXG.Sphere3D](./JXG.Sphere3D.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.GeometryElement3D**  
   ↳ **[JXG.Sphere3D](./JXG.Sphere3D.md)**  
         ↳ **Sphere3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Sphere3D](./Sphere3D.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "sphere3d".  
  

Possible parent array combinations are:

{[JXG.Point3D](../symbols/JXG.Point3D.html)} **center** {number|[JXG.Point3D](./JXG.Point3D.md)} **radius**
:   The center must be given as a [JXG.Point3D](../symbols/JXG.Point3D.html) (see [JXG.providePoints3D](./JXG.md#.providePoints3D)), but the radius can be given as a number (which will create a sphere with a fixed radius) or another [JXG.Point3D](./JXG.Point3D.md).

    If the radius is supplied as number or the output of a function, its absolute value is taken.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
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

// Two points
var center = view.create(
    'point3d',
    [1.5, 1.5, 1.5],
    {
        withLabel: false,
        size: 5,
   }
);
var point = view.create(
    'point3d',
    [2, 1.5, 1.5],
    {
        withLabel: false,
        size: 5
   }
);

// Sphere
var sphere = view.create(
    'sphere3d',
    [center, point],
    {}
);
```

```javascript
// Glider on sphere
    var view = board.create(
        'view3d',
        [[-6, -3], [8, 8],
        [[-3, 3], [-3, 3], [-3, 3]]],
        {
            depthOrder: {
                enabled: true
            },
            projection: 'central',
            xPlaneRear: {fillOpacity: 0.2, gradient: null},
            yPlaneRear: {fillOpacity: 0.2, gradient: null},
            zPlaneRear: {fillOpacity: 0.2, gradient: null}
        }
    );

    // Two points
    var center = view.create('point3d', [0, 0, 0], {withLabel: false, size: 2});
    var point = view.create('point3d', [2, 0, 0], {withLabel: false, size: 2});

    // Sphere
    var sphere = view.create('sphere3d', [center, point], {fillOpacity: 0.8});

    // Glider on sphere
    var glide = view.create('point3d', [2, 2, 0, sphere], {withLabel: false, color: 'red', size: 4});
    var l1 = view.create('line3d', [glide, center], { strokeWidth: 2, dash: 2 });
```
