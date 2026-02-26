

# Point3D



## 描述

A Point3D object is defined by three coordinates [x,y,z], or a function returning an array with three numbers. Alternatively, all numbers can also be provided as functions returning a number.   
  
*Defined in:*  [point3d.js](./src/src_3d_point3d.js.md).   
Extends [JXG.Point3D](./JXG.Point3D.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.GeometryElement3D**  
   ↳ **[JXG.Point3D](./JXG.Point3D.md)**  
         ↳ **Point3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Point3D](./Point3D.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "point3d".  
  

Possible parent array combinations are:

{number|function} **x** {number|function} **y** {number|function} **z** {[JXG.GeometryElement3D](./JXG.GeometryElement3D.md)} **[slide=undefined]**
:   The coordinates are given as x, y, z consisting of numbers or functions. If an optional 3D element "slide" is supplied, the point is a glider on that element. At the time of version v1.11, only elements of type line3d are supperted as glider hosts.
  
  

{array|function} **F** {[JXG.GeometryElement3D](./JXG.GeometryElement3D.md)} **[slide=null]**
:   Alternatively, the coordinates can be supplied as

    * function returning an array [x,y,z] of length 3 of numbers or
    * array arr=[x,y,z] of length 3 consisting of numbers

    If an optional 3D element "slide" is supplied, the point is a glider on that element.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent
objects an exception is thrown.


### 示例

```javascript
var bound = [-5, 5];
   var view = board.create('view3d',
       [[-6, -3], [8, 8],
       [bound, bound, bound]],
       {});
   var p = view.create('point3d', [1, 2, 2], { name:'A', size: 5 });
   var q = view.create('point3d', function() { return [p.X(), p.Y(), p.Z() - 3]; }, { name:'B', size: 3, fixed: true });
   var w = view.create('point3d', [ () => p.X() + 3, () => p.Y(), () => p.Z() - 2], { name:'C', size: 3, fixed: true });
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



## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
| <private> | **[coords](./Point3D.md#coords)**  Homogeneous coordinates of a Point3D, i.e. |
| <private> | **[slide](./Point3D.md#slide)**  Optional slide element, i.e. |




### <private> {Array} **coords**

Homogeneous coordinates of a Point3D, i.e. array of length 4 containing numbers: [w, x, y, z].
Usually, w=1 for finite points and w=0 for points which are infinitely far.
If coordinates of the point are supplied as functions, they are resolved in Point3D#updateCoords into numbers.


### <private> {[JXG.GeometryElement3D](./JXG.GeometryElement3D.md)} **slide**

Optional slide element, i.e. element the Point3D lives on.


#### Default Value:

:   null


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
| <private> | **[F](./Point3D.md#F)**()  Function or array of functions or array of numbers defining the coordinates of the point, used in updateCoords. |
| <private> <static> | Point3D.**[normalizeCoords](./Point3D.md#.normalizeCoords)**()  Normalize homogeneous coordinates such the the first coordinate (the w-coordinate is equal to 1 or 0)- |
| <static> | Point3D.**[setPosition](./Point3D.md#.setPosition)**(coords, noevent)  Set the position of a 3D point. |
| <private> <static> | Point3D.**[updateCoords](./Point3D.md#.updateCoords)**()  Update the array JXG.Point3D#coords containing the homogeneous coords. |
| <static> | Point3D.**[W](./Point3D.md#.W)**()  Get w-coordinate of a 3D point. |
| <static> | Point3D.**[X](./Point3D.md#.X)**()  Get x-coordinate of a 3D point. |
| <static> | Point3D.**[Y](./Point3D.md#.Y)**()  Get y-coordinate of a 3D point. |
| <static> | Point3D.**[Z](./Point3D.md#.Z)**()  Get z-coordinate of a 3D point. |




### <private> **F**()

Function or array of functions or array of numbers defining the coordinates of the point, used in updateCoords.


#### See:

:   updateCoords


### <private> <static> {Object} Point3D.**normalizeCoords**()

Normalize homogeneous coordinates such the the first coordinate (the w-coordinate is equal to 1 or 0)-


#### Returns:

:   {Object} Reference to the Point3D object


#### 示例

```javascript
p.normalizeCoords();
```



### <static> {Object} Point3D.**setPosition**(coords, noevent)

Set the position of a 3D point.


#### Parameters:

:   3D coordinates. Either of the form [x,y,z] (Euclidean) or [w,x,y,z] (homogeneous).
:   If true, no events are triggered (TODO)


#### Returns:

:   {Object} Reference to the Point3D object


#### 示例

```javascript
p.setPosition([1, 3, 4]);
```



### <private> <static> {Object} Point3D.**updateCoords**()

Update the array JXG.Point3D#coords containing the homogeneous coords.


#### Returns:

:   {Object} Reference to the Point3D object


#### See:

:   GeometryElement3D#update()


#### 示例

```javascript
p.updateCoords();
```



### <static> Point3D.**W**()

Get w-coordinate of a 3D point.


#### Returns:

:   Number


#### 示例

```javascript
p.W();
```



### <static> {Number} Point3D.**X**()

Get x-coordinate of a 3D point.


#### Returns:

:   {Number}


#### 示例

```javascript
p.X();
```



### <static> Point3D.**Y**()

Get y-coordinate of a 3D point.


#### Returns:

:   Number


#### 示例

```javascript
p.Y();
```



### <static> Point3D.**Z**()

Get z-coordinate of a 3D point.


#### Returns:

:   Number


#### 示例

```javascript
p.Z();
```
