

# Image



## 描述

Display of an external image.   
  
*Defined in:*  [image.js](./src/src_base_image.js.md).   
Extends [JXG.Image](./JXG.Image.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.CoordsElement**  
   ↳ **[JXG.Image](./JXG.Image.md)**  
         ↳ **Image**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Image](./Image.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "image".  
  

Possible parent array combinations are:

{string|function} **url** {Array} **coords** {Array} **size**
:   url defines the location of the image data. The array coords contains the user coordinates of the lower left corner of the image. It can consist of two or three elements of type number, a string containing a GEONExT constraint, or a function which takes no parameter and returns a number. Every element determines one coordinate. If a coordinate is given by a number, the number determines the initial position of a free image. If given by a string or a function that coordinate will be constrained that means the user won't be able to change the image's position directly by mouse because it will be calculated automatically depending on the string or the function's return value. If two parent elements are given the coordinates will be interpreted as 2D affine Euclidean coordinates, if three such parent elements are given they will be interpreted as homogeneous coordinates.

    The array size defines the image's width and height in user coordinates.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var im = board.create('image', ['https://jsxgraph.org/jsxgraph/distrib/images/uccellino.jpg', [-3,-2], [3,3]]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[attractors](./Image.md#attractors)**  List of attractor elements. |
|  | **[cssClass](./Image.md#cssClass)**  Defines the CSS class used by the image. |
|  | **[highlightCssClass](./Image.md#highlightCssClass)**  Defines the CSS class used by the image when highlighted. |
|  | **[rotate](./Image.md#rotate)**  Image rotation in degrees. |
|  | **[snapSizeX](../symbols/Image.html#snapSizeX)**  Defines together with [Image#snapSizeY](./Image.md#snapSizeY) the grid the image snaps on to. |
|  | **[snapSizeY](../symbols/Image.html#snapSizeY)**  Defines together with [Image#snapSizeX](./Image.md#snapSizeX) the grid the image snaps on to. |




### {Array} **attractors**

List of attractor elements. If the distance of the image is less than
attractorDistance the image is made to glider of this element.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   empty


### {String} **cssClass**

Defines the CSS class used by the image. CSS attributes defined in
this class will overwrite the corresponding JSXGraph attributes, e.g.
opacity.
The default CSS class is defined in jsxgraph.css.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Image#highlightCssClass](./Image.md#highlightCssClass)
:   [Image#highlightCssClass](./Image.md#highlightCssClass)
:   [Text#cssClass](./Text.md#cssClass)
:   [JXG.GeometryElement#cssClass](./JXG.GeometryElement.md#cssClass)


#### Default Value:

:   'JXGimage'


### {String} **highlightCssClass**

Defines the CSS class used by the image when highlighted.
CSS attributes defined in this class will overwrite the
corresponding JSXGraph attributes, e.g. highlightFillOpacity.
The default CSS class is defined in jsxgraph.css.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Image#cssClass](./Image.md#cssClass)
:   [Image#cssClass](./Image.md#cssClass)
:   [Image#highlightCssClass](./Image.md#highlightCssClass)
:   [JXG.GeometryElement#highlightCssClass](./JXG.GeometryElement.md#highlightCssClass)


#### Default Value:

:   'JXGimageHighlight'


### {Number} **rotate**

Image rotation in degrees.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0


### {Number} **snapSizeX**

Defines together with [Image#snapSizeY](./Image.md#snapSizeY) the grid the image snaps on to.
The image will only snap on user coordinates which are
integer multiples to snapSizeX in x and snapSizeY in y direction.
If this value is equal to or less than 0, it will use the grid displayed by the major ticks
of the default ticks of the default x axes of the board.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#snapToGrid](./Point.md#snapToGrid)
:   [Image#snapSizeY](./Image.md#snapSizeY)
:   [JXG.Board#defaultAxes](./JXG.Board.md#defaultAxes)


#### Default Value:

:   1


### {Number} **snapSizeY**

Defines together with [Image#snapSizeX](./Image.md#snapSizeX) the grid the image snaps on to.
The image will only snap on integer multiples to snapSizeX in x and snapSizeY in y direction.
If this value is equal to or less than 0, it will use the grid displayed by the major ticks
of the default ticks of the default y axes of the board.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#snapToGrid](./Point.md#snapToGrid)
:   [Image#snapSizeX](./Image.md#snapSizeX)
:   [JXG.Board#defaultAxes](./JXG.Board.md#defaultAxes)


#### Default Value:

:   1
