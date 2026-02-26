

# Axis



## 描述

Axis is a line with optional ticks and labels. It's strictly spoken just a wrapper for element [Line](../symbols/Line.html) with [Line#straightFirst](../symbols/Line.html#straightFirst) and [Line#straightLast](../symbols/Line.html#straightLast) properties set to true. Additionally [Line#lastArrow](./Line.md#lastArrow) is set to true and default [Ticks](./Ticks.md) will be created.   
  
*Defined in:*  [line.js](./src/src_base_line.js.md).   
Extends [JXG.Line](./JXG.Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
         ↳ **Axis**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Axis](./Axis.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "axis".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|array} **point1** {[JXG.Point](./JXG.Point.md)|array} **point2**
:   Parent elements can be two elements either of type [JXG.Point](./JXG.Point.md) or array of numbers describing the coordinates of a point. In the latter case, the point will be constructed automatically as a fixed invisible point.
  
  

{Number} **a** {Number} **b** {Number} **c**
:   A line can also be created providing three numbers. The line is then described by the set of solutions of the equation a\*x+b\*y+c\*z = 0.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create an axis providing two coords pairs.
  var l1 = board.create('axis', [[0.0, 1.0], [1.0, 1.3]]);
```

```javascript
// Create ticks labels as fractions
 board.create('axis', [[0,1], [1,1]], {
     ticks: {
         label: {
             toFraction: true,
             useMathjax: false,
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
|  | **[anchor](./Axis.md#anchor)**  Position is used in cases: position=='sticky' or position=='fixed'. |
|  | **[anchorDist](./Axis.md#anchorDist)**  Used to define at which distance to the edge of the board the axis should stick or be fixed. |
|  | **[label](./Axis.md#label)**  Attributes for the axis label. |
|  | **[point1](./Axis.md#point1)**  Attributes for first point the axis. |
|  | **[point2](./Axis.md#point2)**  Attributes for second point the axis. |
|  | **[position](./Axis.md#position)**  Is used to define the behaviour of the axis. |
|  | **[ticks](./Axis.md#ticks)**  Attributes for ticks of the axis. |
|  | **[ticksAutoPos](./Axis.md#ticksAutoPos)**  If set to true, the tick labels of the axis are automatically positioned in the narrower area between the axis and the side of the board. |
|  | **[ticksAutoPosThreshold](./Axis.md#ticksAutoPosThreshold)**  Defines, when ticksAutoPos takes effect. |
|  | **[withTicks](./Axis.md#withTicks)**  Show / hide ticks. |




### **anchor**

Position is used in cases: position=='sticky' or position=='fixed'.
Possible values are 'right', 'left', 'right left'. Left and right indicate the side as seen from the axis.
It is used in combination with the attribute position to decide on which side of the board the axis should stick or be fixed.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   ''


### **anchorDist**

Used to define at which distance to the edge of the board the axis should stick or be fixed.
This only has an effect if position=='sticky' or position=='fixed'.
There are the following possibilities:

* Numbers or strings which are numbers (e.g. '10') are interpreted as usrCoords.
* Strings with the unit 'px' are interpreted as screen pixels.
* Strings with the unit '%' or 'fr' are interpreted as a ratio to the width/height of the board. (e.g. 50% = 0.5fr)

  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   '10%'


### {[Label](./Label.md)} **label**

Attributes for the axis label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **point1**

Attributes for first point the axis.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **point2**

Attributes for second point the axis.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### **position**

Is used to define the behaviour of the axis.
Settings in this attribute only have an effect if the axis is exactly horizontal or vertical.
Possible values are:

* 'static': Standard behavior of the axes as know in JSXGraph.
* 'fixed': The axis is placed in a fixed position. Depending on the attribute anchor, it is positioned to the right or left of the edge of the board as seen from the axis with a distance defined in distanceBoarder. The axis will stay at the given position, when the user navigates through the board.
* 'sticky': This mixes the two settings static and fixed. When the user navigates in the board, the axis remains in the visible area (taking into account anchor and anchorDist). If the axis itself is in the visible area, the axis can be moved by navigation.

  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Axis#anchor](./Axis.md#anchor)
:   [Axis#anchorDist](./Axis.md#anchorDist)


#### Default Value:

:   'static'


### {[Ticks](./Ticks.md)} **ticks**

Attributes for ticks of the axis.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### **ticksAutoPos**

If set to true, the tick labels of the axis are automatically positioned in the narrower area between the axis and the side of the board.
Settings in this attribute only have an effect if the axis is exactly horizontal or vertical.
This option overrides offset, anchorX and anchorY of axis tick labels.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### **ticksAutoPosThreshold**

Defines, when ticksAutoPos takes effect.
There are the following possibilities:

* Numbers or strings which are numbers (e.g. '10') are interpreted as usrCoords.
* Strings with the unit 'px' are interpreted as screen pixels.
* Strings with the unit '%' or 'fr' are interpreted as a ratio to the width/height of the board. (e.g. 50% = 0.5fr)

  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   '5%'


### {Boolean} **withTicks**

Show / hide ticks.
Deprecated. Suggested alternative is "ticks: {visible: false}"
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[defaultTicks](./Axis.md#defaultTicks)**  The ticks attached to the axis. |




### {[JXG.Ticks](./JXG.Ticks.md)} **defaultTicks**

The ticks attached to the axis.
