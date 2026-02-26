

# Arc



## 描述

An arc is a partial circumference line of a circle. It is defined by a center, one point that defines the radius, and a third point that defines the angle of the arc.

As a curve the arc has curve length 6.   
  
*Defined in:*  [arc.js](./src/src_element_arc.js.md).   
Extends [Curve](./Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Curve](./Curve.md)**  
            ↳ **Arc**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Arc](./Arc.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "arc".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p3**
:   The result will be an arc of a circle around p1 through p2. The arc is drawn counter-clockwise from p2 to p3.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create an arc out of three free points
var p1 = board.create('point', [2.0, 2.0]);
var p2 = board.create('point', [1.0, 0.5]);
var p3 = board.create('point', [3.5, 1.0]);

var a = board.create('arc', [p1, p2, p3]);
board.create('text',[1,6,function(){return 'arclength: '+Math.round(a.Value()*100)/100}])
```

```javascript
var t = board.create('transform', [2, 1.5], {type: 'scale'});
var a1 = board.create('arc', [[1, 1], [0, 1], [1, 0]], {strokeColor: 'red'});
var a2 = board.create('curve', [a1, t], {strokeColor: 'red'});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[anglePoint](./Arc.md#anglePoint)**  Attributes for angle point. |
|  | **[center](./Arc.md#center)**  Attributes for center point. |
|  | **[hasInnerPoints](./Arc.md#hasInnerPoints)**  If true, moving the mouse over inner points triggers hasPoint. |
|  | **[radiusPoint](./Arc.md#radiusPoint)**  Attributes for radius point. |
|  | **[selection](./Arc.md#selection)**  Type of arc. |
| <private> | **[useDirection](./Arc.md#useDirection)**  If true, there is a fourth parent point, i.e. |




### {[Point](./Point.md)} **anglePoint**

Attributes for angle point.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **center**

Attributes for center point.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {Boolean} **hasInnerPoints**

If true, moving the mouse over inner points triggers hasPoint.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [JXG.GeometryElement#hasPoint](./JXG.GeometryElement.md#hasPoint)


#### Default Value:

:   false


### {[Point](./Point.md)} **radiusPoint**

Attributes for radius point.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {String} **selection**

Type of arc. Possible values are 'minor', 'major', and 'auto'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'auto'


### <private> {Boolean} **useDirection**

If true, there is a fourth parent point, i.e. the parents are [center, p1, p2, p3].
p1 is still the radius point, p2 the angle point. The arc will be that part of the
the circle with center 'center' which starts at p1, ends at the ray between center
and p2, and passes p3.

This attribute is immutable (by purpose).
This attribute is necessary for circumCircleArcs
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[anglepoint](./Arc.md#anglepoint)**  The point defining the arc's angle. |
|  | **[L](./Arc.md#L)**  Arc length. |
|  | **[radiuspoint](./Arc.md#radiuspoint)**  Point defining the arc's radius. |




### {[JXG.Point](./JXG.Point.md)} **anglepoint**

The point defining the arc's angle.


### {Number} **L**

Arc length.


#### See:

:   [Arc#Value](./Arc.md#Value)


### {[JXG.Point](./JXG.Point.md)} **radiuspoint**

Point defining the arc's radius.


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
| <deprecated> | **[getRadius](./Arc.md#getRadius)**() |
|  | **[hasPointSector](./Arc.md#hasPointSector)**(x, y)  Checks whether (x,y) is within the sector defined by the arc. |
|  | **[Radius](./Arc.md#Radius)**()  Determines the arc's current radius. |
|  | **[Value](./Arc.md#Value)**(unit, rad)  Returns the length of the arc or the value of the angle spanned by the arc. |




### {Number} **getRadius**()




#### Deprecated:



#### Returns:

:   {Number}


### {Boolean} **hasPointSector**(x, y)

Checks whether (x,y) is within the sector defined by the arc.


#### Parameters:

:   Coordinate in x direction, screen coordinates.
:   Coordinate in y direction, screen coordinates.


#### Returns:

:   {Boolean} True if (x,y) is within the sector defined by the arc, False otherwise.


### {Number} **Radius**()

Determines the arc's current radius. I.e. the distance between [Arc#center](../symbols/Arc.html#center) and [Arc#radiuspoint](./Arc.md#radiuspoint).


#### Returns:

:   {Number} The arc's radius


### {Number} **Value**(unit, rad)

Returns the length of the arc or the value of the angle spanned by the arc.


#### Parameters:

:   Unit of the returned values. Possible units are

    * 'length' (default): length of the arc line
    * 'radians': angle spanned by the arc in radians
    * 'degrees': angle spanned by the arc in degrees
    * 'semicircle': angle spanned by the arc in radians as a multiple of π, e.g. if the angle is 1.5π, 1.5 will be returned.
    * 'circle': angle spanned by the arc in radians as a multiple of 2π

    It is sufficient to supply the first three characters of the unit, e.g. 'len'.
:   Value of angle which can be used instead of the generic one.


#### Returns:

:   {Number} The arc length or the angle value in various units.
