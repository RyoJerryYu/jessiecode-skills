

# Label



## 描述

Labels are text objects tied to other elements like points, lines and curves. Labels are handled internally by JSXGraph, only. There is NO constructor "board.create('label', ...)".   
  
*Defined in:*  [text.js](./src/src_base_text.js.md).   
Extends [JXG.Text](./JXG.Text.md).




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Text](./JXG.Text.md)**  
         ↳ **Label**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|Text#anchorX, [Text#anchorX](../symbols/Text.html#anchorX) and [Label#offset](../symbols/Label.html#offset).">  | **[Label](../symbols/Label.html#constructor)**  Labels for points are positioned with the attributes [Text#anchorX](../symbols/Text.html#anchorX), [Text#anchorX](../symbols/Text.html#anchorX) and [Label#offset](./Label.md#offset). |




## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[autoPosition](./Label.md#autoPosition)**  Automatic position of label text. |
|  | **[autoPositionMaxDistance](./Label.md#autoPositionMaxDistance)**  The auto position algorithm tries to put a label to a conflict-free position around it's anchor element. |
|  | **[autoPositionMinDistance](./Label.md#autoPositionMinDistance)**  The auto position algorithm tries to put a label to a conflict-free position around it's anchor element. |
|  | **[autoPositionWhitelist](./Label.md#autoPositionWhitelist)**  List of object ids which should be ignored on setting automatic position of label text. |
|  | **[distance](./Label.md#distance)**  Distance of the label from a path element, like line, circle, curve. |
|  | **[offset](./Label.md#offset)**  Label offset from label anchor. |
|  | **[position](../symbols/Label.html#position)**  Point labels are positioned by setting Point#anchorX, Point#anchorY and [Label#offset](./Label.md#offset). |




### {Boolean} **autoPosition**

Automatic position of label text. When called first, the positioning algorithm
starts at the position defined by offset.
The algorithm tries to find a position with the least number of
overlappings with other elements, while retaining the distance
to the anchor element.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Label#offset](./Label.md#offset)
:   GeometryElement#ignoreForLabelAutoposition
:   [Label#autoPositionMinDistance](./Label.md#autoPositionMinDistance)
:   [Label#autoPositionMaxDistance](./Label.md#autoPositionMaxDistance)
:   [Label#autoPositionWhitelist](./Label.md#autoPositionWhitelist)


#### Default Value:

:   false


### {Number} **autoPositionMaxDistance**

The auto position algorithm tries to put a label to a conflict-free
position around it's anchor element. For this, the algorithm tests 12 positions
around the anchor element up to a distance from the anchor
defined here (in pixel).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Label#autoPosition](./Label.md#autoPosition)
:   [Label#autoPositionMinDistance](./Label.md#autoPositionMinDistance)
:   [Label#autoPositionWhitelist](./Label.md#autoPositionWhitelist)


#### Default Value:

:   28


### {Number} **autoPositionMinDistance**

The auto position algorithm tries to put a label to a conflict-free
position around it's anchor element. For this, the algorithm tests 12 positions
around the anchor element starting at a distance from the anchor
defined here (in pixel).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Label#autoPosition](./Label.md#autoPosition)
:   [Label#autoPositionMaxDistance](./Label.md#autoPositionMaxDistance)
:   [Label#autoPositionWhitelist](./Label.md#autoPositionWhitelist)


#### Default Value:

:   12


### {Array} **autoPositionWhitelist**

List of object ids which should be ignored on setting automatic position of label text.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Label#autoPosition](./Label.md#autoPosition)
:   [Label#autoPositionMinDistance](./Label.md#autoPositionMinDistance)
:   [Label#autoPositionMaxDistance](./Label.md#autoPositionMaxDistance)


#### Default Value:

:   []


### {Number} **distance**

Distance of the label from a path element, like line, circle, curve.
The true distance is this value multiplied by 0.5 times the size of the bounding box of the label text.
That means, with a value of 1 the label will touch the path element.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Label#position](./Label.md#position)


#### Default Value:

:   1.5


### {Array} **offset**

Label offset from label anchor.
The label anchor is determined by [Label#position](./Label.md#position)
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Label#position](./Label.md#position)


#### Default Value:

:   [10,10]


### {String} **position**

Point labels are positioned by setting Point#anchorX, Point#anchorY
and [Label#offset](./Label.md#offset).
For line, circle and curve elements (and their derived objects)
there are two possibilities to position labels.

* The first (old) possibility uses the [MetaPost](https://www.tug.org/metapost.html) system:
  Possible string values for the position of a label for
  label anchor points are:
  + 'first' (lines only)
  + 'last' (lines only)
  + 'lft'
  + 'rt'
  + 'top'
  + 'bot'
  + 'ulft'
  + 'urt'
  + 'llft'
  + 'lrt'
* the second (preferred) possibility (since v1.9.0) is:
  with position: 'len side' the label can be positioned exactly along the
  element's path. Here,
  + 'len' is an expression of the form
    - xfr, denoting a fraction of the whole. x is expected to be a number between 0 and 1.
    - x%, a percentage. x is expected to be a number between 0 and 100.
    - x, a number: only possible for line elements and circles. For lines, the label is positioned x
      user units from the starting point. For circles, the number is interpreted as degree, e.g. 45°.
      For everything else, 0 is taken instead.
    - xpx, a pixel value: only possible for line elements.
      The label is positioned x pixels from the starting point.
      For non-lines, 0% is taken instead.If the domain of a curve is not connected, a position of the label close to the line
    between the first and last point of the curve is chosen.
  + 'side' is either 'left' or 'right'. The label is positioned to the left or right of the path, when moving from the
    first point to the last. For circles, 'left' means inside of the circle, 'right' means outside of the circle.
    The distance of the label from the path can be controlled by [Label#distance](./Label.md#distance).Recommended for this second possibility is to use anchorX: 'middle' and 'anchorY: 'middle'.

  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Label#distance](./Label.md#distance)
:   [Label#offset](./Label.md#offset)


#### Default Value:

:   'urt'
