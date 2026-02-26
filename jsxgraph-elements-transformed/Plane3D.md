

# Plane3D



## 描述

A 3D plane is defined either by a point and two linearly independent vectors, or by three points.   
  
*Defined in:*  [linspace3d.js](./src/src_3d_linspace3d.js.md).   
Extends [JXG.GeometryElement3D](./JXG.GeometryElement3D.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.GeometryElement3D](./JXG.GeometryElement3D.md)**  
         ↳ **Plane3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Plane3D](./Plane3D.md#constructor)**  A 3D plane is defined either by a point and two linearly independent vectors, or by three points. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "plane3d".  
  

Possible parent array combinations are:

{[JXG.Point3D](../symbols/JXG.Point3D.html)|array|function} **point** {[JXG.Line3D](../symbols/JXG.Line3D.html)|array|function} **direction1** {[JXG.Line3D](./JXG.Line3D.md)|array|function} **direction2** {array|function} **[range1]** {array|function} **[range2]**
:   The plane is defined by point, direction1, direction2, range1, and range2.

    * point: Point3D or array of length 3
    * direction1: line3d element or array of length 3 or function returning an array of numbers or function returning an array
    * direction2: line3d element or array of length 3 or function returning an array of numbers or function returning an array
    * range1: array of length 2, elements can also be functions. Use [-Infinity, Infinity] for infinite lines.
    * range2: array of length 2, elements can also be functions. Use [-Infinity, Infinity] for infinite lines.
  
  

{[JXG.Point3D](../symbols/JXG.Point3D.html)|array|function} **point1** {[JXG.Point3D](../symbols/JXG.Point3D.html)|array|function} **point2** {[JXG.Point3D](./JXG.Point3D.md)|array|function} **point3**
:   The plane is defined by three points.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent
objects an exception is thrown.


### 示例

```javascript
var view = board.create(
        'view3d',
        [[-6, -3], [8, 8],
        [[-3, 3], [-3, 3], [-3, 3]]],
        {
            depthOrder: {
                enabled: true
            },
            projection: 'central',
            xPlaneRear: {fillOpacity: 0.2},
            yPlaneRear: {fillOpacity: 0.2},
            zPlaneRear: {fillOpacity: 0.2}
        }
    );

    var A = view.create('point3d', [-2, 0, 1], {size: 2});

    // Infinite Plane by point and two directions
    var plane = view.create('plane3d', [A, [1, 0, 0], [0, 1, 0], [-Infinity, Infinity], [-Infinity, Infinity]]);
```

```javascript
var view = board.create(
        'view3d',
        [[-6, -3], [8, 8],
        [[-3, 3], [-3, 3], [-3, 3]]],
        {
            depthOrder: {
                enabled: true
            },
            projection: 'central',
            xPlaneRear: {fillOpacity: 0.2},
            yPlaneRear: {fillOpacity: 0.2},
            zPlaneRear: {fillOpacity: 0.2}
        }
    );

    var A = view.create('point3d', [-2, 0, 1], {size: 2});

    // Finite Plane by point and two directions
    var plane1 = view.create('plane3d', [A, [1, 0, 0], [0, 1, 0], [-2, 2], [-2, 2]]);
    var plane2 = view.create('plane3d', [[0, 0, -1], [1, 0, 0], [0, 1, 0], [-2, 2], [-2, 2]], {
        mesh3d: { visible: true },
        point: {visible: true, name: "B", fixed: false}
    });
```

```javascript
var view = board.create(
                'view3d',
                [[-6, -3], [8, 8],
                [[-3, 3], [-3, 3], [-3, 3]]],
                {
                    depthOrder: {
                        enabled: true
                    },
                    projection: 'central',
                    xPlaneRear: { visible: false, fillOpacity: 0.2 },
                    yPlaneRear: { visible: false, fillOpacity: 0.2 },
                    zPlaneRear: { fillOpacity: 0.2 }
                }
            );

            var A = view.create('point3d', [-2, 0, 1], { size: 2 });

            var line1 = view.create('line3d', [A, [0, 0, 1], [-Infinity, Infinity]], { strokeColor: 'blue' });
            var line2 = view.create('line3d', [A, [1, 1, 0], [-Infinity, Infinity]], { strokeColor: 'blue' });

            // Plane by point and two lines
            var plane2 = view.create('plane3d', [A, line1, line2], {
                fillColor: 'blue'
            });
```

```javascript
var view = board.create(
        'view3d',
        [[-6, -3], [8, 8],
        [[-3, 3], [-3, 3], [-3, 3]]],
        {
            depthOrder: {
                enabled: true
            },
            projection: 'central',
            xPlaneRear: {fillOpacity: 0.2},
            yPlaneRear: {fillOpacity: 0.2},
            zPlaneRear: {fillOpacity: 0.2}
        }
    );

    var A = view.create('point3d', [0, 0, 1], {size: 2});
    var B = view.create('point3d', [2, 2, 1], {size: 2});
    var C = view.create('point3d', [-2, 0, 1], {size: 2});

    // Plane by three points
    var plane = view.create('plane3d', [A, B, C], {
        fillColor: 'blue'
    });
```

```javascript
var view = board.create(
        'view3d',
        [[-6, -3], [8, 8],
        [[-3, 3], [-3, 3], [-3, 3]]],
        {
            depthOrder: {
                enabled: true
            },
            projection: 'central',
            xPlaneRear: {fillOpacity: 0.2},
            yPlaneRear: {fillOpacity: 0.2},
            zPlaneRear: {fillOpacity: 0.2}
        }
    );

    var A = view.create('point3d', [-2, 0, 1], {size: 2});

    // Infinite Plane by two directions,
    // range1 = range2 = [-Infinity, Infinity]
    var plane1 = view.create('plane3d', [A, [1, 0, 0], [0, 1, 0]], {
        fillColor: 'blue',
    });

    // Infinite Plane by three points,
    var plane2 = view.create('plane3d', [A, [1, 0, 0], [0, 1, 0]], {
        threePoints: true,
        fillColor: 'red',
        point2: {visible: true},
        point3: {visible: true}
    });
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[mesh3d](./Plane3D.md#mesh3d)**  Optional 3D mesh of a finite plane. |
|  | **[point](./Plane3D.md#point)**  Attributes of the defining point in case the plane is defined by [point, direction1, direction2, [range1, [range2]]]. |
|  | **[point1](./Plane3D.md#point1)**  Attributes of the first point in case the plane is defined by [point, point, point]. |
|  | **[point2](./Plane3D.md#point2)**  Attributes of the second point in case the plane is defined by [point, point, point]. |
|  | **[point3](./Plane3D.md#point3)**  Attributes of the third point in case the plane is defined by [point, point, point]. |
|  | **[threePoints](./Plane3D.md#threePoints)**  If the second parameter and the third parameter are given as arrays or functions and threePoints:true then the second and third parameter are interpreted as point coordinates and not as directions, i.e. |




### {[Mesh3D](./Mesh3D.md)} **mesh3d**

Optional 3D mesh of a finite plane.
It is not available if the plane is infinite (at initialization time) in any direction.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   see [Mesh3D](./Mesh3D.md)


### {[Point3D](./Point3D.md)} **point**

Attributes of the defining point in case the plane is defined by [point, direction1, direction2, [range1, [range2]]].
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    visible: false, name: "", fixed: true
    ```


### {[Point3D](./Point3D.md)} **point1**

Attributes of the first point in case the plane is defined by [point, point, point].
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    visible: false, name: ""
    ```


### {[Point3D](./Point3D.md)} **point2**

Attributes of the second point in case the plane is defined by [point, point, point].
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    visible: false, name: ""
    ```


### {[Point3D](./Point3D.md)} **point3**

Attributes of the third point in case the plane is defined by [point, point, point].
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    visible: false, name: ""
    ```


### {Boolean} **threePoints**

If the second parameter and the third parameter are given as arrays or functions and threePoints:true
then the second and third parameter are interpreted as point coordinates and not as directions, i.e.
the plane is defined by three points.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   false


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
| <private> | **[d](./Plane3D.md#d)**  Right hand side of the Hesse normal form. |
|  | **[direction1](./Plane3D.md#direction1)**  Two linearly independent vectors - together with a point - define the plane. |
|  | **[direction2](./Plane3D.md#direction2)**  Two linearly independent vectors - together with a point - define the plane. |
| <private> | **[normal](./Plane3D.md#normal)**  Normal vector of the plane. |
| <static> | Plane3D.**[point](./Plane3D.md#.point)**  3D point which - together with two direction vectors - defines the plane. |
|  | **[range\_u](./Plane3D.md#range_u)**  Range [r1, r2] of direction1. |
|  | **[range\_v](./Plane3D.md#range_v)**  Range [r1, r2] of direction2. |
| <private> | **[vec1](./Plane3D.md#vec1)**  Spanning vector 1 of the 3D plane. |
| <private> | **[vec2](./Plane3D.md#vec2)**  Spanning vector 2 of the 3D plane. |




### <private> {Array} **d**

Right hand side of the Hesse normal form.


#### See:

:   Plane3D.updateNormal


### {Array|Function} **direction1**

Two linearly independent vectors - together with a point - define the plane. Each of these direction vectors is an
array of numbers or functions (either of length 3 or 4) or function returning array of length 3 or 4.
Homogeneous coordinates of directions have the form [0, x, y, z].


#### See:

:   [Plane3D.point](./Plane3D.md#.point)
:   [Plane3D#direction2](./Plane3D.md#direction2)


### {Array|Function} **direction2**

Two linearly independent vectors - together with a point - define the plane. Each of these direction vectors is an
array of numbers or functions (either of length 3 or 4) or function returning array of length 3 or 4.
Homogeneous coordinates of directions have the form [0, x, y, z].


#### See:

:   [Plane3D.point](./Plane3D.md#.point)
:   [Plane3D#direction1](./Plane3D.md#direction1)


### <private> {Array} **normal**

Normal vector of the plane. Left hand side of the Hesse normal form.


#### See:

:   Plane3D.updateNormal


### <static> {[JXG.Point3D](./JXG.Point3D.md)} Plane3D.**point**

3D point which - together with two direction vectors - defines the plane.


#### See:

:   [Plane3D#direction1](./Plane3D.md#direction1)
:   [Plane3D#direction2](./Plane3D.md#direction2)


### **range\_u**

Range [r1, r2] of direction1. The 3D line goes from (point + r1 \* direction1) to (point + r2 \* direction1)


#### Default Value:

:   [-Infinity, Infinity]


### **range\_v**

Range [r1, r2] of direction2. The 3D line goes from (point + r1 \* direction2) to (point + r2 \* direction2)


#### Default Value:

:   [-Infinity, Infinity]


### <private> {Array} **vec1**

Spanning vector 1 of the 3D plane. Contains the evaluated coordinates from direction1 and range1.
and is of length 4, the first entry being 0, i.e. homogenous coordinates.


#### See:

:   [Plane3D#updateCoords](./Plane3D.md#updateCoords)


### <private> {Array} **vec2**

Spanning vector 2 of the 3D plane. Contains the evaluated coordinates from [Plane3D#direction2](./Plane3D.md#direction2) and Plane3D#range2
and is of length 4, the first entry being 0, i.e. homogenous coordinates.


#### See:

:   [Plane3D#updateCoords](./Plane3D.md#updateCoords)


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[F](./Plane3D.md#F)**(u, v)  Get coordinate array [x, y, z] of a point on the plane for parameters (u, v). |
| <private> | **[updateCoords](./Plane3D.md#updateCoords)**()  Update the arrays JXG.Plane3D#vec1 and JXG.Plane3D#vec1 containing the homogeneous coords of the spanning vectors. |
| <private> | **[updateNormal](./Plane3D.md#updateNormal)**()  Update the Hesse normal form of the plane, i.e. |
|  | **[X](./Plane3D.md#X)**(u, v)  Get x-coordinate of a point on the plane for parameters (u, v). |
|  | **[Y](./Plane3D.md#Y)**(u, v)  Get y-coordinate of a point on the plane for parameters (u, v). |
|  | **[Z](./Plane3D.md#Z)**(u, v)  Get z-coordinate of a point on the plane for parameters (u, v). |




### **F**(u, v)

Get coordinate array [x, y, z] of a point on the plane for parameters (u, v).


#### Parameters:





#### Returns:

:   Array of length 3.


### <private> {Object} **updateCoords**()

Update the arrays JXG.Plane3D#vec1 and JXG.Plane3D#vec1 containing the homogeneous coords of the spanning vectors.


#### Returns:

:   {Object} Reference to Plane3D object


### <private> {Object} **updateNormal**()

Update the Hesse normal form of the plane, i.e. update normal vector and right hand side.
Updates also vec1 and vec2.


#### Returns:

:   {Object} Reference to the Plane3D object


#### 示例

```javascript
plane.updateNormal();
```



### **X**(u, v)

Get x-coordinate of a point on the plane for parameters (u, v).


#### Parameters:





#### Returns:

:   Number


### **Y**(u, v)

Get y-coordinate of a point on the plane for parameters (u, v).


#### Parameters:





#### Returns:

:   Number


### **Z**(u, v)

Get z-coordinate of a point on the plane for parameters (u, v).


#### Parameters:





#### Returns:

:   Number
