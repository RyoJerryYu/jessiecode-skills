

# Text



## 描述

Constructs a text element. The coordinates can either be absolute (i.e. respective to the coordinate system of the board) or be relative to the coordinates of an element given in [Text#anchor](./Text.md#anchor).

HTML, MathJaX, KaTeX and GEONExT syntax can be handled.

There are two ways to display texts:




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Text](./JXG.Text.md)**  
         ↳ **Text**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Text](./Text.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "text".  
  

Possible parent array combinations are:

{number|function} **z**   *Optional* {number|function} **x** {number|function} **y** {String|function} **str**
:   Parent elements for text elements.

    Parent elements can be two or three elements of type number, a string containing a GEONExT constraint, or a function which takes no parameter and returns a number. Every parent element beside the last determines one coordinate. If a coordinate is given by a number, the number determines the initial position of a free text. If given by a string or a function that coordinate will be constrained that means the user won't be able to change the texts's position directly by mouse because it will be calculated automatically depending on the string or the function's return value. If two parent elements are given the coordinates will be interpreted as 2D affine Euclidean coordinates, if three such parent elements are given they will be interpreted as homogeneous coordinates.

    The text to display may be given as string or as function returning a string. There is the attribute 'display' which takes the values 'html' or 'internal'. In case of 'html' an HTML division tag is created to display the text. In this case it is also possible to use MathJax, KaTeX, or ASCIIMathML. If neither of these is used, basic Math rendering is applied.

    In case of 'internal', an SVG text element is used to display the text.


### 示例

```javascript
// Create a fixed text at position [0,1].
  var t1 = board.create('text',[0,1,"Hello World"]);
```

```javascript
// Create a variable text at a variable position.
  var s = board.create('slider',[[0,4],[3,4],[-2,0,2]]);
  var graph = board.create('text',
                       [function(x){ return s.Value();}, 1,
                        function(){return "The value of s is"+JXG.toFixed(s.Value(), 2);}
                       ]
                    );
```

```javascript
// Create a text bound to the point A
var p = board.create('point',[0, 1]),
    t = board.create('text',[0, -1,"Hello World"], {anchor: p});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[anchor](./Text.md#anchor)**  Anchor element [Point](../symbols/Point.html), [Text](../symbols/Text.html) or [Image](./Image.md) of the text. |
|  | **[anchorX](./Text.md#anchorX)**  The horizontal alignment of the text. |
|  | **[anchorY](./Text.md#anchorY)**  The vertical alignment of the text. |
|  | **[attractors](./Text.md#attractors)**  List of attractor elements. |
|  | **[cssClass](./Text.md#cssClass)**  Apply CSS classes to the text in non-highlighted view. |
|  | **[cssDefaultStyle](./Text.md#cssDefaultStyle)**  Default CSS properties of the HTML text element. |
|  | **[cssStyle](./Text.md#cssStyle)**  CSS properties of the HTML text element. |
|  | **[digits](./Text.md#digits)**  Used to round texts given by a number. |
|  | **[display](./Text.md#display)**  Determines the rendering method of the text. |
|  | **[dragArea](./Text.md#dragArea)**  Sensitive area for dragging the text. |
|  | **[fontSize](./Text.md#fontSize)**  The font size in pixels. |
|  | **[fontUnit](./Text.md#fontUnit)**  CSS unit for the font size of a text element. |
|  | **[formatNumber](./Text.md#formatNumber)**  If the text content is solely a number and this attribute is true (default) then the number is either formatted according to the number of digits given by the attribute 'digits' or converted into a fraction if 'toFraction' is true. |
|  | **[highlightCssClass](./Text.md#highlightCssClass)**  Apply CSS classes to the text in highlighted view. |
|  | **[highlightCssDefaultStyle](./Text.md#highlightCssDefaultStyle)**  Default CSS properties of the HTML text element in case of highlighting. |
|  | **[highlightCssStyle](./Text.md#highlightCssStyle)**  CSS properties of the HTML text element in case of highlighting. |
|  | **[intl](./Text.md#intl)**  Internationalization support for texts consisting of a number only. |
|  | **[isLabel](./Text.md#isLabel)**  If enabled, the text will be handled as label. |
|  | **[katexMacros](./Text.md#katexMacros)**  Object or function returning an object that contains macros for KaTeX. |
|  | **[parse](./Text.md#parse)**  If set to true, the text is parsed and evaluated. |
|  | **[rotate](./Text.md#rotate)**  Text rotation in degrees. |
|  | **[snapSizeX](../symbols/Text.html#snapSizeX)**  Defines together with [Text#snapSizeY](./Text.md#snapSizeY) the grid the text snaps on to. |
|  | **[snapSizeY](../symbols/Text.html#snapSizeY)**  Defines together with [Text#snapSizeX](./Text.md#snapSizeX) the grid the text snaps on to. |
|  | **[toFraction](./Text.md#toFraction)**  Display number as integer + nominator / denominator. |
|  | **[useASCIIMathML](./Text.md#useASCIIMathML)**  If true, the input will be given to ASCIIMathML before rendering. |
|  | **[useCaja](./Text.md#useCaja)**  If set to true and caja's sanitizeHTML function can be found it will be used to sanitize text output. |
|  | **[useKatex](./Text.md#useKatex)**  If true, KaTeX will be used to render the input string. |
|  | **[useMathJax](./Text.md#useMathJax)**  If true, MathJax will be used to render the input string. |
|  | **[visible](./Text.md#visible)** |




### {Object} **anchor**

Anchor element [Point](../symbols/Point.html), [Text](../symbols/Text.html) or [Image](./Image.md) of the text.
If it exists, the coordinates of the text are relative
to this anchor element. In this case, only numbers are possible coordinates,
functions are not supported.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   null


### {String} **anchorX**

The horizontal alignment of the text. Possible values include 'auto', 'left',
'middle', and 'right'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'left'


### {String} **anchorY**

The vertical alignment of the text. Possible values include 'auto, 'top', 'middle', and
'bottom'.
For MathJax or KaTeX, 'top' is recommended.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'middle'


### {Array} **attractors**

List of attractor elements. If the distance of the text is less than
attractorDistance the text is made to glider of this element.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   empty


### {String} **cssClass**

Apply CSS classes to the text in non-highlighted view. It is possible to supply one or more
CSS classes separated by blanks.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Text#highlightCssClass](./Text.md#highlightCssClass)
:   [Image#cssClass](./Image.md#cssClass)
:   [JXG.GeometryElement#cssClass](./JXG.GeometryElement.md#cssClass)


#### Default Value:

:   'JXGtext'


### {String} **cssDefaultStyle**

Default CSS properties of the HTML text element.

The CSS properties which are set here, are handed over to the style property
of the HTML text element. That means, they have higher property than any
CSS class.

If a property which is set here should be overruled by a CSS class
then this property should be removed here.

The reason, why this attribute should be kept to its default value at all,
is that screen dumps of SVG boards with board.renderer.dumpToCanvas()
will ignore the font-family if it is set in a CSS class.
It has to be set explicitly as style attribute.

In summary, the order of priorities (specificity) from high to low is

1. JXG.Options.text.cssStyle
2. JXG.Options.text.cssDefaultStyle
3. JXG.Options.text.cssClass

  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Text#highlightCssDefaultStyle](./Text.md#highlightCssDefaultStyle)
:   [Text#cssStyle](./Text.md#cssStyle)
:   [Text#highlightCssStyle](./Text.md#highlightCssStyle)


#### Default Value:

:   'font-family: Arial, Helvetica, Geneva, sans-serif;'


### {String} **cssStyle**

CSS properties of the HTML text element.

The CSS properties which are set here, are handed over to the style property
of the HTML text element. That means, they have higher property (specificity) han any
CSS class.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Text#cssDefaultStyle](./Text.md#cssDefaultStyle)
:   [Text#highlightCssDefaultStyle](./Text.md#highlightCssDefaultStyle)
:   [Text#highlightCssStyle](./Text.md#highlightCssStyle)


#### Default Value:

:   ''


### {Number} **digits**

Used to round texts given by a number.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   2


### {String} **display**

Determines the rendering method of the text. Possible values
include 'html' and 'internal.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'html'


### {String} **dragArea**

Sensitive area for dragging the text.
Possible values are 'all', or something else.
If set to 'small', a sensitivity margin at the right and left border is taken.
This may be extended to left, right, ... in the future.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'all'


### {Number} **fontSize**

The font size in pixels.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Text#fontUnit](./Text.md#fontUnit)


#### Default Value:

:   12


### {String} **fontUnit**

CSS unit for the font size of a text element. Usually, this will be the default value 'px' but
for responsive application, also 'vw', 'vh', vmax', 'vmin' or 'rem' might be useful.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Text#fontSize](./Text.md#fontSize)


#### Default Value:

:   'px'


### {Boolean} **formatNumber**

If the text content is solely a number and
this attribute is true (default) then the number is either formatted
according to the number of digits
given by the attribute 'digits' or converted into a fraction if 'toFraction'
is true.

Otherwise, display the raw number.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {String} **highlightCssClass**

Apply CSS classes to the text in highlighted view. It is possible to supply one or more
CSS classes separated by blanks.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Text#cssClass](./Text.md#cssClass)
:   [Image#highlightCssClass](./Image.md#highlightCssClass)
:   [JXG.GeometryElement#highlightCssClass](./JXG.GeometryElement.md#highlightCssClass)


#### Default Value:

:   'JXGtext'


### {String} **highlightCssDefaultStyle**

Default CSS properties of the HTML text element in case of highlighting.

The CSS properties which are set here, are handed over to the style property
of the HTML text element. That means, they have higher property than any
CSS class.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Text#cssDefaultStyle](./Text.md#cssDefaultStyle)
:   [Text#cssStyle](./Text.md#cssStyle)
:   [Text#highlightCssStyle](./Text.md#highlightCssStyle)


#### Default Value:

:   'font-family: Arial, Helvetica, Geneva, sans-serif;'


### {String} **highlightCssStyle**

CSS properties of the HTML text element in case of highlighting.

The CSS properties which are set here, are handed over to the style property
of the HTML text element. That means, they have higher property (specificity) than any
CSS class.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Text#cssDefaultStyle](./Text.md#cssDefaultStyle)
:   [Text#highlightCssDefaultStyle](./Text.md#highlightCssDefaultStyle)
:   [Text#cssStyle](./Text.md#cssStyle)


#### Default Value:

:   ''


### {object} **intl**

Internationalization support for texts consisting of a number only.

Setting the local overwrites the board-wide locale set in the board attributes.
The JSXGraph attribute digits is overruled by the
Intl attributes "minimumFractionDigits" and "maximumFractionDigits".
See <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat>
for more information about possible options.

See below for an example where the text is composed from a string and a locale formatted number.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [JXG.Board#intl](./JXG.Board.md#intl)


#### Default Value:

:   ```
    {
       enabled: 'inherit',
       options: {
         minimumFractionDigits: 0,
         maximumFractionDigits: 2
       }
    }
    ```


### {Boolean} **isLabel**

If enabled, the text will be handled as label. Intended for internal use.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {Object} **katexMacros**

Object or function returning an object that contains macros for KaTeX.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   {}


### {Boolean} **parse**

If set to true, the text is parsed and evaluated.
For labels parse==true results in converting names of the form k\_a to subscripts.
If the text is given by string and parse==true, the string is parsed as
JessieCode expression.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true


### {Number} **rotate**

Text rotation in degrees.
Works for non-zero values only in combination with display=='internal'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0


### {Number} **snapSizeX**

Defines together with [Text#snapSizeY](./Text.md#snapSizeY) the grid the text snaps on to.
The text will only snap on integer multiples to snapSizeX in x and snapSizeY in y direction.
If this value is equal to or less than 0, it will use the grid displayed by the major ticks
of the default ticks of the default x axes of the board.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#snapToGrid](./Point.md#snapToGrid)
:   [Text#snapSizeY](./Text.md#snapSizeY)
:   [JXG.Board#defaultAxes](./JXG.Board.md#defaultAxes)


#### Default Value:

:   1


### {Number} **snapSizeY**

Defines together with [Text#snapSizeX](./Text.md#snapSizeX) the grid the text snaps on to.
The text will only snap on integer multiples to snapSizeX in x and snapSizeY in y direction.
If this value is equal to or less than 0, it will use the grid displayed by the major ticks
of the default ticks of the default y axes of the board.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#snapToGrid](./Point.md#snapToGrid)
:   [Text#snapSizeX](./Text.md#snapSizeX)
:   [JXG.Board#defaultAxes](./JXG.Board.md#defaultAxes)


#### Default Value:

:   1


### {Boolean} **toFraction**

Display number as integer + nominator / denominator. Works together
with MathJax, KaTex or as plain text.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   JXG#toFraction


#### Default Value:

:   false


### {Boolean} **useASCIIMathML**

If true, the input will be given to ASCIIMathML before rendering.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {Boolean} **useCaja**

If set to true and caja's sanitizeHTML function can be found it
will be used to sanitize text output.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {Boolean} **useKatex**

If true, KaTeX will be used to render the input string.
For this feature, katex.min.js and katex.min.css have to be included.

The example below does not work, because there is a conflict with
the MathJax library which is used below.

  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {Boolean} **useMathJax**

If true, MathJax will be used to render the input string.
Supports MathJax 2 as well as Mathjax 3.
It is recommended to use this option together with the option
"parse: false". Otherwise, 4 backslashes (e.g. \\\\alpha) are needed
instead of two (e.g. \\alpha).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Text#parse](./Text.md#parse)


#### Default Value:

:   false


### {Boolean} **visible**

*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true
