

# Line3D



## 描述

A line in 3D is given by two points, or one point and a direction vector.   
  
*Defined in:*  [linspace3d.js](./src/src_3d_linspace3d.js.md).   
Extends [JXG.GeometryElement3D](./JXG.GeometryElement3D.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.GeometryElement3D](./JXG.GeometryElement3D.md)**  
         ↳ **Line3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Line3D](./Line3D.md#constructor)**  A line in 3D is given by two points, or one point and a direction vector. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "line3d".  
  

Possible parent array combinations are:

{[JXG.Point3D](../symbols/JXG.Point3D.html)|array|function} **point1** {[JXG.Point3D](./JXG.Point3D.md)|array|function} **point2**
:   First and second defining point of the line. The attributes [Line3D#straightFirst](../symbols/Line3D.html#straightFirst) and [Line3D#straightLast](./Line3D.md#straightLast) control if the line is displayed as segment, ray or infinite line.
  
  

{[JXG.Point3D](../symbols/JXG.Point3D.html)|array|function} **point** {[JXG.Line3D](./JXG.Line3D.md)|array|function} **direction** {array|function} **range**
:   The line is defined by point, direction and range.

    * point: Point3D or array of length 3
    * direction: array of length 3 or function returning an array of numbers or function returning an array
    * range: array of length 2, elements can also be functions. Use [-Infinity, Infinity] for infinite lines.


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
    // Lines through 2 points
    var l1 = view.create('line3d', [[1, 3, 3], [-3, -3, -3]], {point1: {visible: true}, point2: {visible: true} });
    var l2 = view.create('line3d', [p, l1.point1]);

    // Line by point, direction, range
    var l3 = view.create('line3d', [p, [0, 0, 1], [-2, 4]]);
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

    var A = view.create('point3d', [0, 0, 0], {size: 2});
    var B = view.create('point3d', [2, 1, 1], {size: 2});
    var C = view.create('point3d', [-2.5, 2.5, 1.5], {size: 2});

    // Draggable line by two points
    var line1 = view.create('line3d', [A, B], {
        fixed: false,
        straightFirst: true,
        straightLast: true,
        dash: 2
    });

    // Line by point, direction, and range
    var line2 = view.create('line3d', [C, [1, 0, 0], [-1, Infinity]], {
        strokeColor: 'blue'
    });

    // Line by point and array
    var line3 = view.create('line3d', [C, [-2.5, -1, 1.5]], {
        point2: { visible: true},
        strokeColor: 'red'
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
         projection: 'parallel',
         xPlaneRear: { fillOpacity: 0.2 },
         yPlaneRear: { fillOpacity: 0.2 },
         zPlaneRear: { fillOpacity: 0.2 }
     }
 );


var A = view.create('point3d', [-2, 0, 1], { size: 2 });
var B = view.create('point3d', [-2, 0, 2], { size: 2 });
var line1 = view.create('line3d', [A, B], {
    fixed: false,
    strokeColor: 'blue',
    straightFirst: true,
    straightLast: true
});

var C = view.create('point3d', [2, 0, 1], { size: 2 });
var line2 = view.create('line3d', [C, line1, [-Infinity, Infinity]], { strokeColor: 'red' });
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[point](./Line3D.md#point)**  Attributes of the defining point in case the line is defined by [point, vector, [range]] |
|  | **[point1](./Line3D.md#point1)**  Attributes of the first point in case the line is defined by [point, point]. |
|  | **[point2](./Line3D.md#point2)**  Attributes of the second point in case the line is defined by [point, point]. |
|  | **[straightFirst](./Line3D.md#straightFirst)**  If the 3D line is defined by two points and if this attribute is true, the 3D line stretches infinitely in direction of its first point. |
|  | **[straightLast](./Line3D.md#straightLast)**  If the 3D line is defined by two points and if this attribute is true, the 3D line stretches infinitely in direction of its second point. |




### {[Point3D](./Point3D.md)} **point**

Attributes of the defining point in case the line is defined by [point, vector, [range]]
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    visible: false, name: ""
    ```


### {[Point3D](./Point3D.md)} **point1**

Attributes of the first point in case the line is defined by [point, point].
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    visible: false, name: ""
    ```


### {[Point3D](./Point3D.md)} **point2**

Attributes of the second point in case the line is defined by [point, point].
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    visible: false, name: ""
    ```


### {Boolean} **straightFirst**

If the 3D line is defined by two points and if this attribute is true,
the 3D line stretches infinitely in direction of its first point.
Otherwise it ends at point1.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### See:

:   [Line3D#straightLast](./Line3D.md#straightLast)


#### Default Value:

:   false


### {Boolean} **straightLast**

If the 3D line is defined by two points and if this attribute is true,
the 3D line stretches infinitely in direction of its second point.
Otherwise it ends at point2.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### See:

:   [Line3D#straightFirst](./Line3D.md#straightFirst)


#### Default Value:

:   false


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[direction](./Line3D.md#direction)**  Direction which - together with a point - defines the line. |
|  | **[endpoints](./Line3D.md#endpoints)**  Array of length 2 containing the endings of the Line3D element. |
| <private> | **[getPointCoords](./Line3D.md#getPointCoords)**  Determine one end point of a 3D line from point, direction and range). |
| <static> | Line3D.**[point](./Line3D.md#.point)**  3D point which - together with a direction - defines the line. |
|  | **[range](./Line3D.md#range)**  Range [r1, r2] of the line. |
|  | **[vec](./Line3D.md#vec)**  Spanning vector of the 3D line. |




### {Array|Function} **direction**

Direction which - together with a point - defines the line. Array of numbers or functions (of length 3) or function
returning array of length 3.


#### See:

:   [Line3D.point](./Line3D.md#.point)


### **endpoints**

Array of length 2 containing the endings of the Line3D element. These are the defining points,
the intersections of the line with the bounding box, or the endings defined by the range.


### <private> {Array} **getPointCoords**

Determine one end point of a 3D line from point, direction and range).


### <static> {[Point3D](./Point3D.md)} Line3D.**point**

3D point which - together with a direction - defines the line.


#### See:

:   [Line3D#direction](./Line3D.md#direction)


### {Array} **range**

Range [r1, r2] of the line. r1, r2 can be numbers or functions.
The 3D line goes from (point + r1 \* direction) to (point + r2 \* direction)


#### Default Value:

:   [-Infinity, Infinity]


### **vec**

Spanning vector of the 3D line. Contains the evaluated coordinates from direction
and range.
The array has length 4, the first entry being 0.


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
| <private> | **[setPosition2D](./Line3D.md#setPosition2D)**(t)  Set the 2D position of the defining points. |
| <private> | **[updateCoords](../symbols/Line3D.html#updateCoords)**()  Update the array [Line3D#vec](./Line3D.md#vec) containing the homogeneous coords of the spanning vector. |
|  | **[updateZIndex](./Line3D.md#updateZIndex)**()  Update the z-index of the line, i.e. |




### <private> **setPosition2D**(t)

Set the 2D position of the defining points.


#### Parameters:

:   projective 2D transformation


### <private> {Object} **updateCoords**()

Update the array [Line3D#vec](./Line3D.md#vec) containing the homogeneous coords of the spanning vector.


#### Returns:

:   {Object} Reference to Line3D object


### {Object} **updateZIndex**()

Update the z-index of the line, i.e. the z-index of its midpoint.


#### Returns:

:   {Object} Reference to Line3D object
