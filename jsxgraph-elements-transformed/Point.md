

# Point



## 描述

Construct a free or a fixed point. A free point is created if the given parent elements are all numbers and the property fixed is not set or set to false. If one or more parent elements is not a number but a string containing a GEONExT constraint or a function the point will be considered as constrained). That means that the user won't be able to change the point's position directly.   
  
*Defined in:*  [point.js](./src/src_base_point.js.md).   
Extends [JXG.Point](./JXG.Point.md).




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Point](./JXG.Point.md)**  
         ↳ **Point**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Point](./Point.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "point".  
  

Possible parent array combinations are:

{Number|string|function} **z**   *Optional* {Number|string|function} **x** {Number|string|function} **y**
:   Parent elements can be two or three elements of type number, a string containing a GEONExT constraint, or a function which takes no parameter and returns a number. Every parent element determines one coordinate. If a coordinate is given by a number, the number determines the initial position of a free point. If given by a string or a function that coordinate will be constrained that means the user won't be able to change the point's position directly by mouse because it will be calculated automatically depending on the string or the function's return value. If two parent elements are given the coordinates will be interpreted as 2D affine Euclidean coordinates, if three such parent elements are given they will be interpreted as homogeneous coordinates.
  
  
:   A point can also be created providing a transformation or an array of transformations. The resulting point is a clone of the base point transformed by the given Transformation. {@see JXG.Transformation}.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a free point using affine Euclidean coordinates
var p1 = board.create('point', [3.5, 2.0]);
```

```javascript
// Create a constrained point using anonymous function
var p2 = board.create('point', [3.5, function () { return p1.X(); }]);
```

```javascript
// Create a point using transformations
var trans = board.create('transform', [2, 0.5], {type:'scale'});
var p3 = board.create('point', [p2, trans]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[attractorDistance](./Point.md#attractorDistance)**  If the distance of the point to one of its attractors is less than this number the point will be a glider on this attracting element. |
|  | **[attractors](./Point.md#attractors)**  List of attractor elements. |
|  | **[attractorUnit](./Point.md#attractorUnit)**  Unit for attractorDistance and snatchDistance, used for magnetized points and for snapToPoints. |
|  | **[attractToGrid](../symbols/Point.html#attractToGrid)**  If set to true, the point will only snap to (possibly invisibly) grid points when within [Point#attractorDistance](./Point.md#attractorDistance) of such a grid point. |
|  | **[face](./Point.md#face)**  There are different point styles which differ in appearance. |
|  | **[ignoredSnapToPoints](./Point.md#ignoredSnapToPoints)**  List of elements which are ignored by snapToPoints. |
|  | **[infoboxDigits](./Point.md#infoboxDigits)**  Truncating rule for the digits in the infobox. |
|  | **[showInfobox](./Point.md#showInfobox)**  If true, the infobox is shown on mouse/pen over, if false not. |
|  | **[size](./Point.md#size)**  Size of a point, either in pixel or user coordinates. |
|  | **[sizeUnit](./Point.md#sizeUnit)**  Unit for size. |
|  | **[snapSizeX](../symbols/Point.html#snapSizeX)**  Defines together with [Point#snapSizeY](./Point.md#snapSizeY) the grid the point snaps on to. |
|  | **[snapSizeY](../symbols/Point.html#snapSizeY)**  Defines together with [Point#snapSizeX](./Point.md#snapSizeX) the grid the point snaps on to. |
|  | **[snapToGrid](../symbols/Point.html#snapToGrid)**  If set to true, the point will snap to a grid of integer multiples of [Point#snapSizeX](../symbols/Point.html#snapSizeX) and [Point#snapSizeY](./Point.md#snapSizeY) (in user coordinates). |
|  | **[snapToPoints](../symbols/Point.html#snapToPoints)**  If set to true, the point will snap to the nearest point in distance of [Point#attractorDistance](./Point.md#attractorDistance). |
|  | **[snatchDistance](./Point.md#snatchDistance)**  If the distance of the point to one of its attractors is at least this number the point will be released from being a glider on the attracting element. |
|  | **[style](./Point.md#style)**  This attribute was used to determined the point layout. |
|  | **[zoom](./Point.md#zoom)**  If true, the point size changes on zoom events. |




### {Number} **attractorDistance**

If the distance of the point to one of its attractors is less
than this number the point will be a glider on this
attracting element.
If set to zero nothing happens.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.0


### {Array} **attractors**

List of attractor elements. If the distance of the point is less than
attractorDistance the point is made to glider of this element.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   empty


### {String} **attractorUnit**

Unit for attractorDistance and snatchDistance, used for magnetized points and for snapToPoints.
Possible values are 'screen' and 'user'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#attractorDistance](./Point.md#attractorDistance)
:   [Point#snatchDistance](./Point.md#snatchDistance)
:   [Point#snapToPoints](./Point.md#snapToPoints)
:   [Point#attractors](./Point.md#attractors)


#### Default Value:

:   'user'


### {Boolean} **attractToGrid**

If set to true, the point will only snap to (possibly invisibly) grid points
when within [Point#attractorDistance](./Point.md#attractorDistance) of such a grid point.

The coordinates of the grid points are either integer multiples of snapSizeX and snapSizeY
(given in user coordinates, not pixels) or are the intersection points
of the major ticks of the boards default axes in case that snapSizeX, snapSizeY are negative.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#attractorDistance](./Point.md#attractorDistance)
:   [Point#attractorUnit](./Point.md#attractorUnit)
:   [Point#snapToGrid](./Point.md#snapToGrid)
:   [Point#snapSizeX](./Point.md#snapSizeX)
:   [Point#snapSizeY](./Point.md#snapSizeY)


#### Default Value:

:   false


### {String} **face**

There are different point styles which differ in appearance.
Posssible values are

| Input | Output |
| --- | --- |
| cross | x |
| circle | o |
| square, [] | [] |
| plus | + |
| minus | - |
| divide | | |
| diamond | <> |
| diamond2 | <> (bigger) |
| triangleup | ^, a, A |
| triangledown | v |
| triangleleft | < |
| triangleright | > |

  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [JXG.Point#setStyle](./JXG.Point.md#setStyle)


#### Default Value:

:   circle


### {Array} **ignoredSnapToPoints**

List of elements which are ignored by snapToPoints.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   empty


### {String| Number} **infoboxDigits**

Truncating rule for the digits in the infobox.

* 'auto': done automatically by JXG.autoDigits()
* 'none': no truncation
* number: truncate after "number digits" with JXG.toFixed()

  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   JXG#autoDigits
:   JXG#toFixed


#### Default Value:

:   'auto'


### {Boolean|String} **showInfobox**

If true, the infobox is shown on mouse/pen over, if false not.
If the value is 'inherit', the value of
[JXG.Board#showInfobox](./JXG.Board.md#showInfobox) is taken.
true | false | 'inherit'
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [JXG.Board#showInfobox](./JXG.Board.md#showInfobox)


#### Default Value:

:   true


### {Number} **size**

Size of a point, either in pixel or user coordinates.
Means radius resp. half the width of a point (depending on the face).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#face](./Point.md#face)
:   [JXG.Point#setStyle](./JXG.Point.md#setStyle)
:   [Point#sizeUnit](./Point.md#sizeUnit)


#### Default Value:

:   3


### {String} **sizeUnit**

Unit for size.
Possible values are 'screen' and 'user.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#size](./Point.md#size)


#### Default Value:

:   'screen'


### {Number} **snapSizeX**

Defines together with [Point#snapSizeY](./Point.md#snapSizeY) the grid the point snaps on to.
It is given in user coordinates, not in pixels.
The point will only snap on integer multiples to snapSizeX in x and snapSizeY in y direction.
If this value is equal to or less than 0, it will use the grid displayed by the major ticks
of the default ticks of the default x axes of the board.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#snapToGrid](./Point.md#snapToGrid)
:   [Point#snapSizeY](./Point.md#snapSizeY)
:   [JXG.Board#defaultAxes](./JXG.Board.md#defaultAxes)


#### Default Value:

:   1


### {Number} **snapSizeY**

Defines together with [Point#snapSizeX](./Point.md#snapSizeX) the grid the point snaps on to.
It is given in user coordinates, not in pixels.
The point will only snap on integer multiples to snapSizeX in x and snapSizeY in y direction.
If this value is equal to or less than 0, it will use the grid displayed by the major ticks
of the default ticks of the default y axes of the board.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#snapToGrid](./Point.md#snapToGrid)
:   [Point#snapSizeX](./Point.md#snapSizeX)
:   [JXG.Board#defaultAxes](./JXG.Board.md#defaultAxes)


#### Default Value:

:   1


### {Boolean} **snapToGrid**

If set to true, the point will snap to a grid of integer multiples of
[Point#snapSizeX](../symbols/Point.html#snapSizeX) and [Point#snapSizeY](./Point.md#snapSizeY) (in user coordinates).

The coordinates of the grid points are either integer multiples of snapSizeX and snapSizeY
(given in user coordinates, not pixels) or are the intersection points
of the major ticks of the boards default axes in case that snapSizeX, snapSizeY are negative.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#snapSizeX](./Point.md#snapSizeX)
:   [Point#snapSizeY](./Point.md#snapSizeY)


#### Default Value:

:   false


### {Boolean} **snapToPoints**

If set to true, the point will snap to the nearest point in distance of
[Point#attractorDistance](./Point.md#attractorDistance).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#attractorDistance](./Point.md#attractorDistance)


#### Default Value:

:   false


### {Number} **snatchDistance**

If the distance of the point to one of its attractors is at least
this number the point will be released from being a glider on the
attracting element.
If set to zero nothing happens.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.0


### {Number} **style**

This attribute was used to determined the point layout. It was derived from GEONExT and was
replaced by [Point#face](../symbols/Point.html#face) and [Point#size](./Point.md#size).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#face](./Point.md#face)
:   [Point#size](./Point.md#size)


#### Default Value:

:   5


### {Boolean} **zoom**

If true, the point size changes on zoom events.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false
