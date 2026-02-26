

# Ticks



## 描述

Ticks are used as distance markers on a line or curve. They are mainly used for axis elements and slider elements. Ticks may stretch infinitely or finitely, which can be set with [Ticks#majorHeight](../symbols/Ticks.html#majorHeight) and [Ticks#minorHeight](./Ticks.md#minorHeight).

There are the following ways to position the tick lines:

For arbitrary lines (and not axes) a "zero coordinate" is determined which defines where the first tick is positioned. This zero coordinate can be altered with the attribute anchor. Possible values are "left", "middle", "right" or a number. The default value is "left".   
  
*Defined in:*  [ticks.js](./src/src_base_ticks.js.md).   
Extends [JXG.Ticks](./JXG.Ticks.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Ticks](./JXG.Ticks.md)**  
         ↳ **Ticks**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Ticks](./Ticks.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "ticks".  
  

Possible parent array combinations are:

{[JXG.Line](../symbols/JXG.Line.html)|[JXG.Curve](./JXG.Curve.md)} **line**
:   The parents consist of the line or curve the ticks are going to be attached to.
  
  

{Array} **ticks**
:   Optional array of numbers. If given, a fixed number of static ticks is created at these user-supplied positions.

    Deprecated: Alternatively, a number defining the distance between two major ticks can be specified. However, this is meanwhile ignored. Use attribute ticksDistance instead.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Add ticks to line 'l1' through 'p1' and 'p2'. The major ticks are
// two units apart and 40 px long.
  var p1 = board.create('point', [0, 3]);
  var p2 = board.create('point', [1, 3]);
  var l1 = board.create('line', [p1, p2]);
  var t = board.create('ticks', [l1], {
     ticksDistance: 2,
     majorHeight: 40
  });
```

```javascript
// Create ticks labels as fractions
board.create('axis', [[0,1], [1,1]], {
    ticks: {
        label: {
            toFraction: true,
            useMathjax: true,
            display: 'html',
            anchorX: 'middle',
            offset: [0, -10]
        }
    }
});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[anchor](./Ticks.md#anchor)**  Determine the position of the tick with value 0. |
|  | **[beautifulScientificTickLabels](./Ticks.md#beautifulScientificTickLabels)**  Format tick labels that were going to have scientific notation like 5.00e+6 to look like 5•10⁶. |
|  | **[digits](../symbols/Ticks.html#digits)**  If a label exceeds [Ticks#maxLabelLength](./Ticks.md#maxLabelLength) this determines the number of digits used to shorten the tick label. |
|  | **[drawLabels](./Ticks.md#drawLabels)**  Draw labels yes/no |
|  | **[drawZero](./Ticks.md#drawZero)**  Draw the zero tick, that lies at line.point1? |
|  | **[face](./Ticks.md#face)**  Tick face for major ticks of finite length. |
|  | **[generateLabelText](./Ticks.md#generateLabelText)**  A function that expects two [JXG.Coords](./JXG.Coords.md), the first one representing the coordinates of the tick that is to be labeled, the second one the coordinates of the center (the tick with position 0). |
| <deprecated> | **[generateLabelValue](./Ticks.md#generateLabelValue)**  A function that expects two [JXG.Coords](./JXG.Coords.md), the first one representing the coordinates of the tick that is to be labeled, the second one the coordinates of the center (the tick with position 0). |
|  | **[ignoreInfiniteTickEndings](./Ticks.md#ignoreInfiniteTickEndings)**  If true, ignore the tick endings attribute for infinite (full height) ticks. |
|  | **[includeBoundaries](./Ticks.md#includeBoundaries)**  Whether line boundaries should be included or not in the lower and upper bounds when creating ticks. |
|  | **[insertTicks](./Ticks.md#insertTicks)**  Let JSXGraph determine the distance between ticks automatically. |
|  | **[intl](./Ticks.md#intl)**  Internationalization support for ticks labels. |
|  | **[label](./Ticks.md#label)**  Attributes for the ticks labels. |
|  | **[labels](./Ticks.md#labels)**  User defined labels for special ticks. |
|  | **[majorHeight](./Ticks.md#majorHeight)**  Total height of a major tick. |
|  | **[majorTickEndings](./Ticks.md#majorTickEndings)**  Decides in which direction major ticks are visible. |
|  | **[maxLabelLength](./Ticks.md#maxLabelLength)**  The maximum number of characters a tick label can use. |
|  | **[minorHeight](./Ticks.md#minorHeight)**  Total height of a minor tick. |
|  | **[minorTicks](./Ticks.md#minorTicks)**  The number of minor ticks between two major ticks. |
|  | **[minTicksDistance](./Ticks.md#minTicksDistance)**  Minimum distance in pixel of equidistant ticks in case insertTicks==true. |
|  | **[precision](../symbols/Ticks.html#precision)**  If a label exceeds [Ticks#maxLabelLength](./Ticks.md#maxLabelLength) this determines the precision used to shorten the tick label. |
|  | **[scale](./Ticks.md#scale)**  Scale the ticks but not the tick labels. |
|  | **[scaleSymbol](../symbols/Ticks.html#scaleSymbol)**  A string that is appended to every tick, used to represent the scale factor given in [Ticks#scale](./Ticks.md#scale). |
|  | **[tickEndings](./Ticks.md#tickEndings)**  Decides in which direction minor ticks are visible. |
|  | **[ticksDistance](./Ticks.md#ticksDistance)**  The default distance (in user coordinates, not pixels) between two ticks. |
|  | **[ticksPerLabel](./Ticks.md#ticksPerLabel)**  By default, i.e. |
|  | **[type](./Ticks.md#type)**  Set the ticks type. |
|  | **[useUnicodeMinus](./Ticks.md#useUnicodeMinus)**  Use the unicode character 0x2212, i.e. |




### {String} **anchor**

Determine the position of the tick with value 0. 'left' means point1 of the line, 'right' means point2,
and 'middle' is equivalent to the midpoint of the defining points. This attribute is ignored if the parent
line is of type axis.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'left'


### {Boolean} **beautifulScientificTickLabels**

Format tick labels that were going to have scientific notation
like 5.00e+6 to look like 5•10⁶.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {Number} **digits**

If a label exceeds [Ticks#maxLabelLength](./Ticks.md#maxLabelLength) this determines the number of digits used to shorten the tick label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks#maxLabelLength](./Ticks.md#maxLabelLength)


#### Default Value:

:   3


### {Boolean} **drawLabels**

Draw labels yes/no
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {Boolean} **drawZero**

Draw the zero tick, that lies at line.point1?
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {String} **face**

Tick face for major ticks of finite length. By default (face: '|') this is a straight line.
Possible other values are '<' and '>'. These faces are used in
JXG.Hatch for hatch marking parallel lines.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   hatch


#### Default Value:

:   '|'


### {function} **generateLabelText**

A function that expects two [JXG.Coords](./JXG.Coords.md), the first one representing the coordinates of the
tick that is to be labeled, the second one the coordinates of the center (the tick with position 0).
The third parameter is a null, number or a string. In the latter two cases, this value is taken.
Returns a string.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {function} **generateLabelValue**

A function that expects two [JXG.Coords](./JXG.Coords.md), the first one representing the coordinates of the
tick that is to be labeled, the second one the coordinates of the center (the tick with position 0).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Deprecated:



### {Boolean} **ignoreInfiniteTickEndings**

If true, ignore the tick endings attribute for infinite (full height) ticks.
This affects major and minor ticks.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks#tickEndings](./Ticks.md#tickEndings)
:   [Ticks#majorTickEndings](./Ticks.md#majorTickEndings)


#### Default Value:

:   true


### {Boolean} **includeBoundaries**

Whether line boundaries should be included or not in the lower and upper bounds when
creating ticks. In mathematical terms: if a segment considered as interval is open (includeBoundaries:false)
or closed (includeBoundaries:true). In case of open interval, the interval is shortened by a small
ε.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {Boolean} **insertTicks**

Let JSXGraph determine the distance between ticks automatically.
If true, the attribute ticksDistance is ignored.
The distance between ticks is affected by the size of the board and
the attribute minTicksDistance (in pixel).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks#ticksDistance](./Ticks.md#ticksDistance)
:   [Ticks#minTicksDistance](./Ticks.md#minTicksDistance)


#### Default Value:

:   false


### **intl**

Internationalization support for ticks labels.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [JXG.Board#intl](./JXG.Board.md#intl)
:   [Text#intl](./Text.md#intl)


#### Default Value:

:   ```
    {
       enabled: 'inherit',
       options: {}
    }
    ```


### {Object} **label**

Attributes for the ticks labels.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   ```
    {
      tabindex: null,
      layer: 7, // line
      highlight: false
      }
    ```


### {Array} **labels**

User defined labels for special ticks. Instead of the i-th tick's position, the i-th string stored in this array
is shown. If the number of strings in this array is less than the number of special ticks, the tick's position is
shown as a fallback.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   []


### {Number} **majorHeight**

Total height of a major tick. If negative the full height of the board is taken.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   10


### {Array} **majorTickEndings**

Decides in which direction major ticks are visible. Possible values are either the constants
0=false or 1=true or a function returning 0 or 1.
In case of [0,1] the tick is only visible to the right of the line. In case of
[1,0] the tick is only visible to the left of the line.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks#tickEndings](./Ticks.md#tickEndings)
:   [Ticks#ignoreInfiniteTickEndings](./Ticks.md#ignoreInfiniteTickEndings)


#### Default Value:

:   [1, 1]


### {Number} **maxLabelLength**

The maximum number of characters a tick label can use.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks#digits](./Ticks.md#digits)


#### Default Value:

:   5


### {Number} **minorHeight**

Total height of a minor tick. If negative the full height of the board is taken.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   4


### {Number} **minorTicks**

The number of minor ticks between two major ticks.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   4


### {Number} **minTicksDistance**

Minimum distance in pixel of equidistant ticks in case insertTicks==true.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks#insertTicks](./Ticks.md#insertTicks)


#### Default Value:

:   10


### {Number} **precision**

If a label exceeds [Ticks#maxLabelLength](./Ticks.md#maxLabelLength) this determines the precision used to shorten the tick label.
Deprecated! Replaced by the attribute digits.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks#maxLabelLength](./Ticks.md#maxLabelLength)
:   [Ticks#digits](./Ticks.md#digits)


#### Default Value:

:   3


### {Number} **scale**

Scale the ticks but not the tick labels.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks#scaleSymbol](./Ticks.md#scaleSymbol)


#### Default Value:

:   1


### {String} **scaleSymbol**

A string that is appended to every tick, used to represent the scale
factor given in [Ticks#scale](./Ticks.md#scale).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks#scale](./Ticks.md#scale)


#### Default Value:

:   ''


### {Array} **tickEndings**

Decides in which direction minor ticks are visible. Possible values are either the constants
0=false or 1=true or a function returning 0 or 1.
In case of [0,1] the tick is only visible to the right of the line. In case of
[1,0] the tick is only visible to the left of the line.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks#majorTickEndings](./Ticks.md#majorTickEndings)


#### Default Value:

:   [1, 1]


### {Number} **ticksDistance**

The default distance (in user coordinates, not pixels) between two ticks. Please be aware that this value is overruled
if [Ticks#insertTicks](../symbols/Ticks.html#insertTicks) is set to true. In case, [Ticks#insertTicks](./Ticks.md#insertTicks) is false, the maximum number of ticks
is hard coded to be less than 2048.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks#insertTicks](./Ticks.md#insertTicks)


#### Default Value:

:   1


### **ticksPerLabel**

By default, i.e. if ticksPerLabel==false, labels are generated for major ticks, only.
If ticksPerLabel is set to a(n integer) number, this denotes the number of minor ticks
between two labels.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {String} **type**

Set the ticks type.
Possible values are 'linear' or 'polar'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'linear'


### {Boolean} **useUnicodeMinus**

Use the unicode character 0x2212, i.e. the HTML entity &minus; as minus sign.
That is −1 instead of -1.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true
