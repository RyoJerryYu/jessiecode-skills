

# Sector



## 描述

A circular sector is a subarea of the area enclosed by a circle. It is enclosed by two radii and an arc.

The sector as curve consists of two legs and an arc. The curve length is 6. That means, a point with coordinates [sector.X(t), sector.Y(t)] is on




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Sector**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Sector](./Sector.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "sector".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p3**
:   A sector is defined by three points: The sector's center p1, a second point p2 defining the radius and a third point p3 defining the angle of the sector. The Sector is always drawn counter clockwise from p2 to p3.

    In this case, the sector will have an arc as sub-object.

    Second possibility of input parameters are:
  
  
:   line2, coords1 or direction1, coords2 or direction2, radius The sector is defined by two lines. The two legs which define the sector are given by two coordinates arrays which are projected initially to the two lines or by two directions (+/- 1). If the two lines are parallel, two of the defining points on different lines have to coincide. This will be the center of the sector. The last parameter is the radius of the sector.

    In this case, the sector will **not** have an arc as sub-object.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.

First possibility of input parameters are:


### 示例

```javascript
// Create a sector out of three free points
var p1 = board.create('point', [1.5, 5.0]),
    p2 = board.create('point', [1.0, 0.5]),
    p3 = board.create('point', [5.0, 3.0]),

    a = board.create('sector', [p1, p2, p3]);
```

```javascript
// Create a sector out of two lines, two directions and a radius
var p1 = board.create('point', [-1, 4]),
 p2 = board.create('point', [4, 1]),
 q1 = board.create('point', [-2, -3]),
 q2 = board.create('point', [4,3]),

 li1 = board.create('line', [p1,p2], {strokeColor:'black', lastArrow:true}),
 li2 = board.create('line', [q1,q2], {lastArrow:true}),

 sec1 = board.create('sector', [li1, li2, [5.5, 0], [4, 3], 3]),
 sec2 = board.create('sector', [li1, li2, 1, -1, 4]);
```

```javascript
var t = board.create('transform', [2, 1.5], {type: 'scale'});
var s1 = board.create('sector', [[-3.5,-3], [-3.5, -2], [-3.5,-4]], {
                anglePoint: {visible:true}, center: {visible: true}, radiusPoint: {visible: true},
                fillColor: 'yellow', strokeColor: 'black'});
var s2 = board.create('curve', [s1, t], {fillColor: 'yellow', strokeColor: 'black'});
```

```javascript
var A = board.create('point', [3, -2]),
    B = board.create('point', [-2, -2]),
    C = board.create('point', [0, 4]);

var angle = board.create('sector', [B, A, C], {
        strokeWidth: 0,
        arc: {
        	visible: true,
        	strokeWidth: 3,
          lastArrow: {size: 4},
          firstArrow: {size: 4}
        }
      });
//angle.arc.setAttribute({firstArrow: false});
angle.arc.setAttribute({lastArrow: false});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[anglePoint](./Sector.md#anglePoint)**  Attributes for helper point anglepoint in case it is provided by coordinates. |
|  | **[arc](./Sector.md#arc)**  Attributes for sub-element arc. |
|  | **[center](./Sector.md#center)**  Attributes for helper point center in case it is provided by coordinates. |
|  | **[label](./Sector.md#label)**  Attributes for the sector label. |
|  | **[radiusPoint](./Sector.md#radiusPoint)**  Attributes for helper point radiuspoint in case it is provided by coordinates. |
|  | **[selection](./Sector.md#selection)**  Type of sector. |




### {[Point](./Point.md)} **anglePoint**

Attributes for helper point anglepoint in case it is provided by coordinates.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Arc](./Arc.md)} **arc**

Attributes for sub-element arc. It is only available, if the sector is defined by three points.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   '{visible:false}'


### {[Point](./Point.md)} **center**

Attributes for helper point center in case it is provided by coordinates.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Label](./Label.md)} **label**

Attributes for the sector label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **radiusPoint**

Attributes for helper point radiuspoint in case it is provided by coordinates.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {String} **selection**

Type of sector. Possible values are 'minor', 'major', and 'auto'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'auto'


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[point1](./Sector.md#point1)**  Midpoint of the sector. |
|  | **[point2](../symbols/Sector.html#point2)**  This point together with [Sector#point1](./Sector.md#point1) defines the radius. |
|  | **[point3](./Sector.md#point3)**  Defines the sector's angle. |
|  | **[point4](./Sector.md#point4)**  Defines the sectors orientation in case of circumCircleSectors. |




### {[JXG.Point](./JXG.Point.md)} **point1**

Midpoint of the sector.


### {[JXG.Point](./JXG.Point.md)} **point2**

This point together with [Sector#point1](./Sector.md#point1) defines the radius.


### {[JXG.Point](./JXG.Point.md)} **point3**

Defines the sector's angle.


### {[JXG.Point](./JXG.Point.md)} **point4**

Defines the sectors orientation in case of circumCircleSectors.


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[Area](./Sector.md#Area)**()  Area of the sector. |
| <private> | **[autoRadius](./Sector.md#autoRadius)**()  Sets radius if the attribute `radius` has value 'auto'. |
|  | **[hasPointSector](./Sector.md#hasPointSector)**(x, y)  Checks whether (x,y) is within the area defined by the sector. |
|  | **[L](./Sector.md#L)**()  Arc length. |
|  | **[Perimeter](./Sector.md#Perimeter)**()  Sector perimeter, i.e. |
|  | **[Radius](./Sector.md#Radius)**()  Returns the radius of the sector. |
| <private> | **[setPositionDirectly](./Sector.md#setPositionDirectly)**(method, coords, oldcoords)  Moves the sector by the difference of two coordinates. |
|  | **[setRadius](./Sector.md#setRadius)**(value)  Overwrite the Radius method of the sector. |
|  | **[Value](../symbols/Sector.html#Value)**(unit)  Length of the sector's arc or the angle in various units, see [Arc#Value](./Arc.md#Value). |




### {Number} **Area**()

Area of the sector.


#### Returns:

:   {Number} The area of the sector.


### <private> {Number} **autoRadius**()

Sets radius if the attribute `radius` has value 'auto'.
Sets a radius between 20 and 50 points, depending on the distance
between the center and the radius point.
This function is used in [Angle](./Angle.md).


#### Returns:

:   {Number} returns a radius value in user coordinates.


### {Boolean} **hasPointSector**(x, y)

Checks whether (x,y) is within the area defined by the sector.


#### Parameters:

:   Coordinate in x direction, screen coordinates.
:   Coordinate in y direction, screen coordinates.


#### Returns:

:   {Boolean} True if (x,y) is within the sector defined by the arc, False otherwise.


### {Number} **L**()

Arc length.


#### Returns:

:   {Number} Length of the sector's arc.


#### See:

:   [Arc#L](./Arc.md#L)


### {Number} **Perimeter**()

Sector perimeter, i.e. arc length plus 2 \* radius.


#### Returns:

:   {Number} Perimeter of sector.


### {Number} **Radius**()

Returns the radius of the sector.


#### Returns:

:   {Number} The distance between [Sector#point1](../symbols/Sector.html#point1) and [Sector#point2](./Sector.md#point2).


### <private> {[JXG.Curve](./JXG.Curve.md)} **setPositionDirectly**(method, coords, oldcoords)

Moves the sector by the difference of two coordinates.


#### Parameters:

:   The type of coordinates used here. Possible values are [JXG.COORDS\_BY\_USER](../symbols/JXG.html#.COORDS_BY_USER) and [JXG.COORDS\_BY\_SCREEN](./JXG.md#.COORDS_BY_SCREEN).
:   coordinates in screen/user units
:   previous coordinates in screen/user units


#### Returns:

:   {[JXG.Curve](./JXG.Curve.md)} this element


### **setRadius**(value)

Overwrite the Radius method of the sector.
Used in GeometryElement#setAttribute.


#### Parameters:

:   New radius.


### {Number} **Value**(unit)

Length of the sector's arc or the angle in various units, see [Arc#Value](./Arc.md#Value).


#### Parameters:




#### Returns:

:   {Number} The arc length or the angle value in various units.


#### See:

:   [Arc#Value](./Arc.md#Value)
