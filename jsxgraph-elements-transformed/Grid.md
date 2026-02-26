

# Grid



## 描述

A grid is a mesh consisting of vertical and horizontal lines or other geometrical objects.   
  
*Defined in:*  [grid.js](./src/src_element_grid.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Grid**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Grid](./Grid.md#constructor)**  A grid is a set of vertical and horizontal lines or other geometrical objects (faces) to support the user with element placement or to improve determination of position. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "grid".  
  

Possible parent array combinations are:

{JXG.Axis} **a1** {JXG.Axis} **a2**
:   Optional parent axis.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// standard grid
var g = board.create('grid', [], {});
```

```javascript
// more fancy grid
var g = board.create('grid', [], {
    major: {
        face: 'plus',
        size: 7,
        strokeColor: 'green',
        strokeOpacity: 1,
    },
    minor: {
        size: 4
    },
    minorElements: 3,
});
```

```javascript
// extreme fancy grid
var grid = board.create('grid', [], {
    major: {
        face: 'regularPolygon',
        size: 8,
        strokeColor: 'blue',
        fillColor: 'orange',
        strokeOpacity: 1,
    },
    minor: {
        face: 'diamond',
        size: 4,
        strokeColor: 'green',
        fillColor: 'grey',
    },
    minorElements: 1,
    includeBoundaries: false,
});
```

```javascript
// grid with parent axes
var axis1 = board.create('axis', [[-1, -2.5], [1, -2.5]], {
    ticks: {
        strokeColor: 'green',
        strokeWidth: 2,
        minorticks: 2,
        majorHeight: 10,
        drawZero: true
    }
});
var axis2 = board.create('axis', [[3, 0], [3, 2]], {
    ticks: {
        strokeColor: 'red',
        strokeWidth: 2,
        minorticks: 3,
        majorHeight: 10,
        drawZero: true
    }
});
var grid = board.create('grid', [axis1, axis2], {
    major: {
        face: 'line'
    },
    minor: {
        face: 'point',
        size: 3
    },
    minorElements: 'auto',
    includeBoundaries: false,
});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[drawZero](./Grid.md#drawZero)**  This attribute determines whether the grid elements located at x=0, y=0 and (for major grid only) at (0, 0) are displayed. |
|  | **[face](./Grid.md#face)**  Appearance of grid elements. |
|  | **[forceSquare](./Grid.md#forceSquare)**  To print a quadratic grid with same distance of major grid elements in x- and y-direction. |
|  | **[gridX](./Grid.md#gridX)**  Deprecated. |
|  | **[gridY](./Grid.md#gridY)**  Deprecated. |
|  | **[includeBoundaries](./Grid.md#includeBoundaries)**  To decide whether major or minor grid elements on boundaries of the boundingBox shall be shown, half-ones as well. |
|  | **[major](./Grid.md#major)**  This object contains the attributes for major grid elements. |
|  | **[majorStep](./Grid.md#majorStep)**  Distance of major grid elements. |
|  | **[margin](./Grid.md#margin)**  This number (pixel value) controls where grid elements end at the canvas edge. |
|  | **[minor](./Grid.md#minor)**  This object contains the attributes for minor grid elements. |
|  | **[minorElements](./Grid.md#minorElements)**  Number of elements in minor grid between elements of the major grid. |
|  | **[polygonVertices](./Grid.md#polygonVertices)**  Number of vertices for face 'polygon'. |
|  | **[size](./Grid.md#size)**  Size of grid elements. |
| <private> | **[themes](./Grid.md#themes)**  Array of theme attributes. |




### **drawZero**

This attribute determines whether the grid elements located at x=0, y=0
and (for major grid only) at (0, 0) are displayed.
The main reason to set this attribute to "false", might be in combination with axes.

* If false, then all these elements are hidden.
* If true, all these elements are shown.
* If an object of the following form is given, the three cases can be distinguished individually:  
  {x: true|false, y: true|false, origin: true|false}

***This attribute can be set individually for major and minor grid as a sub-entry of [Grid#major](../symbols/Grid.html#major) or [Grid#minor](./Grid.md#minor)***,
e.g. major: {drawZero: ...}
For default values have a look there.

  
*Defined in:*  [options.js](./src/src_options.js.md).


### **face**

Appearance of grid elements.
There are different styles which differ in appearance.
Possible values are (comparing to [Point#face](./Point.md#face)):

| Input | Output | Fillable by fillColor,... |
| --- | --- | --- |
| point, . | . | no |
| line | − | no |
| cross, x | x | no |
| circle, o | o | yes |
| square, [] | [] | yes |
| plus, + | + | no |
| minus, - | - | no |
| divide, | | | | no |
| diamond, <> | <> | yes |
| diamond2, <<>> | <> (bigger) | yes |
| triangleup, ^, a, A | ^ | no |
| triangledown, v | v | no |
| triangleleft, < | < | no |
| triangleright, > | > | no |
| regularPolygon, regpol | ⬡ | yes |

***This attribute can be set individually for major and minor grid as a sub-entry of [Grid#major](../symbols/Grid.html#major) or [Grid#minor](./Grid.md#minor)***,
e.g. major: {face: ...}
For default values have a look there.

  
*Defined in:*  [options.js](./src/src_options.js.md).


### **forceSquare**

To print a quadratic grid with same distance of major grid elements in x- and y-direction.
'min' or true will set both distances of major grid elements in x- and y-direction to the primarily lesser value,
'max' to the primarily greater value.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### **gridX**

Deprecated. Use [Grid#majorStep](./Grid.md#majorStep) instead.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   null


### **gridY**

Deprecated. Use [Grid#majorStep](./Grid.md#majorStep) instead.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   null


### **includeBoundaries**

To decide whether major or minor grid elements on boundaries of the boundingBox shall be shown, half-ones as well.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### **major**

This object contains the attributes for major grid elements.
You can override the following grid attributes individually here:

* [Grid#size](./Grid.md#size)
* [Grid#face](./Grid.md#face)
* [Grid#margin](./Grid.md#margin)
* [Grid#drawZero](./Grid.md#drawZero)
* [Grid#polygonVertices](./Grid.md#polygonVertices)

Default values are:

```
{
     size: 5,
     face: 'line',
     margin: 0,
     drawZero: true,
     polygonVertices: 6
 }
```

  
*Defined in:*  [options.js](./src/src_options.js.md).


### **majorStep**

Distance of major grid elements. There are three possibilities:

* If it is set to 'auto' the distance of the major grid equals the distance of majorTicks of the corresponding axis.
* Numbers or strings which are numbers (e.g. '10') are interpreted as distance in usrCoords.
* Strings with the unit 'px' are interpreted as distance in screen pixels.
* Strings with the unit '%' or 'fr' are interpreted as a ratio to the width/height of the board. (e.g. 50% = 0.5fr)

Instead of one value you can provide two values as an array [x, y] here.
These are used as distance in x- and y-direction.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [JXG.Ticks#getDistanceMajorTicks](./JXG.Ticks.md#getDistanceMajorTicks)


#### Default Value:

:   'auto'


### **margin**

This number (pixel value) controls where grid elements end at the canvas edge. If zero, the line
ends exactly at the end, if negative there is a margin to the inside, if positive the line
ends outside of the canvas (which is invisible).

***This attribute can be set individually for major and minor grid as a sub-entry of [Grid#major](../symbols/Grid.html#major) or [Grid#minor](./Grid.md#minor)***,
e.g. major: {margin: ...}
For default values have a look there.

  
*Defined in:*  [options.js](./src/src_options.js.md).


### **minor**

This object contains the attributes for minor grid elements.
You can override the following grid attributes individually here:

* [Grid#size](./Grid.md#size)
* [Grid#face](./Grid.md#face)
* [Grid#margin](./Grid.md#margin)
* [Grid#drawZero](./Grid.md#drawZero)
* [Grid#polygonVertices](./Grid.md#polygonVertices)

Default values are:

```
{
     size: 3,
     face: 'point',
     margin: 0,
     drawZero: true,
     polygonVertices: 6
 }
```

  
*Defined in:*  [options.js](./src/src_options.js.md).


### **minorElements**

Number of elements in minor grid between elements of the major grid. There are three possibilities:

* If set to 'auto', the number minor elements is equal to the number of minorTicks of the corresponding axis.
* Numbers or strings which are numbers (e.g. '10') are interpreted as quantity.

Instead of one value you can provide two values as an array [x, y] here.
These are used as number in x- and y-direction.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0


### **polygonVertices**

Number of vertices for face 'polygon'.

***This attribute can be set individually for major and minor grid as a sub-entry of [Grid#major](../symbols/Grid.html#major) or [Grid#minor](./Grid.md#minor)***,
e.g. major: {polygonVertices: ...}
For default values have a look there.

  
*Defined in:*  [options.js](./src/src_options.js.md).


### **size**

Size of grid elements. There are the following possibilities:

* Numbers or strings which are numbers (e.g. '10') are interpreted as size in pixels.
* Strings with additional '%' (e.g. '95%') are interpreted as the ratio of used space for one element.

Unused for 'line' which will use the value of strokeWidth.
Instead of one value you can provide two values as an array [x, y] here.
These are used as size in x- and y-direction.

***This attribute can be set individually for major and minor grid as a sub-entry of [Grid#major](../symbols/Grid.html#major) or [Grid#minor](./Grid.md#minor)***,
e.g. major: {size: ...}
For default values have a look there.

  
*Defined in:*  [options.js](./src/src_options.js.md).


### <private> **themes**

Array of theme attributes.
The index of the entry is the number of the theme.
  
*Defined in:*  [options.js](./src/src_options.js.md).
