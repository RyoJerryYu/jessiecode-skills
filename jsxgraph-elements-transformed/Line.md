

# Line



## 描述

A general line is given by two points or three coordinates. By setting additional properties a line can be used as an arrow and/or axis.   
  
*Defined in:*  [line.js](./src/src_base_line.js.md).   
Extends [JXG.Line](./JXG.Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
         ↳ **Line**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Line](./Line.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "line".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|array|function} **point1** {[JXG.Point](./JXG.Point.md)|array|function} **point2**
:   Parent elements can be two elements either of type [JXG.Point](./JXG.Point.md) or array of numbers describing the coordinates of a point. In the latter case the point will be constructed automatically as a fixed invisible point. It is possible to provide a function returning an array or a point, instead of providing an array or a point.
  
  

{Number|function} **a** {Number|function} **b** {Number|function} **c**
:   A line can also be created providing three numbers. The line is then described by the set of solutions of the equation a\*z+b\*x+c\*y = 0. For all finite points, z is normalized to the value 1. It is possible to provide three functions returning numbers, too.
  
  

{function} **f**
:   This function must return an array containing three numbers forming the line's homogeneous coordinates.

    Additionally, a line can be created by providing a line and a transformation (or an array of transformations). Then, the result is a line which is the transformation of the supplied line.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a line using point and coordinates/
// The second point will be fixed and invisible.
var p1 = board.create('point', [4.5, 2.0]);
var l1 = board.create('line', [p1, [1.0, 1.0]]);
```

```javascript
// Create a line using three coordinates
var l1 = board.create('line', [1.0, -2.0, 3.0]);
```

```javascript
// Create a line (l2) as reflection of another line (l1)
        // reflection line
        var li = board.create('line', [1,1,1], {strokeColor: '#aaaaaa'});
        var reflect = board.create('transform', [li], {type: 'reflect'});

        var l1 = board.create('line', [1,-5,1]);
        var l2 = board.create('line', [l1, reflect]);
```

```javascript
var t = board.create('transform', [2, 1.5], {type: 'scale'});
var l1 = board.create('line', [1, -5, 1]);
var l2 = board.create('line', [l1, t]);
```

```javascript
//create line between two points
var p1 = board.create('point', [0,0]);
var p2 = board.create('point', [2,2]);
var l1 = board.create('line', [p1,p2], {straightFirst:false, straightLast:false});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[firstArrow](./Line.md#firstArrow)**  Configure the arrow head at the position of its first point or the corresponding intersection with the canvas border The attribute firstArrow can be a Boolean or an object with the following sub-attributes:  ``` {      type: 1, // possible values are 1, 2, . ``` |
|  | **[label](./Line.md#label)**  Attributes for the line label. |
|  | **[lastArrow](./Line.md#lastArrow)**  Configure the arrow head at the position of its second point or the corresponding intersection with the canvas border. |
|  | **[margin](./Line.md#margin)**  This number (pixel value) controls where infinite lines end at the canvas border. |
|  | **[point1](./Line.md#point1)**  Attributes for first defining point of the line. |
|  | **[point2](./Line.md#point2)**  Attributes for second defining point of the line. |
|  | **[snapSizeX](../symbols/Line.html#snapSizeX)**  Defines together with [Point#snapSizeY](./Point.md#snapSizeY) the grid the point snaps on to. |
|  | **[snapSizeY](../symbols/Line.html#snapSizeY)**  Defines together with [Point#snapSizeX](./Point.md#snapSizeX) the grid the point snaps on to. |
|  | **[snapToGrid](../symbols/Line.html#snapToGrid)**  If set to true, the point will snap to a grid defined by [Point#snapSizeX](../symbols/Point.html#snapSizeX) and [Point#snapSizeY](./Point.md#snapSizeY). |
|  | **[straightFirst](./Line.md#straightFirst)**  If true, line stretches infinitely in direction of its first point. |
|  | **[straightLast](./Line.md#straightLast)**  If true, line stretches infinitely in direction of its second point. |
|  | **[ticks](./Line.md#ticks)**  Attributes for ticks of the line. |
|  | **[touchFirstPoint](../symbols/Line.html#touchFirstPoint)**  If set to true, [Line#firstArrow](./Line.md#firstArrow) is set to true and the point is visible, the arrow head will just touch the circle line of the start point of the line. |
|  | **[touchLastPoint](../symbols/Line.html#touchLastPoint)**  If set to true, [Line#lastArrow](./Line.md#lastArrow) is set to true and the point is visible, the arrow head will just touch the circle line of the start point of the line. |




### {Boolean | Object} **firstArrow**

Configure the arrow head at the position of its first point or the corresponding
intersection with the canvas border
The attribute firstArrow can be a Boolean or an object with the following sub-attributes:

```
{
     type: 1, // possible values are 1, 2, ..., 7. Default value is 1.
     size: 6, // size of the arrow head. Default value is 6.
              // This value is multiplied with the strokeWidth of the line
              // Exception: for type=7 size is ignored
     highlightSize: 6, // size of the arrow head in case the element is highlighted. Default value
}
```

type=7 is the default for curves if firstArrow: true

An arrow head can be turned off with line.setAttribute({firstArrow: false}).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Line#lastArrow](./Line.md#lastArrow)
:   [Line#touchFirstPoint](./Line.md#touchFirstPoint)


#### Default Value:

:   false


### {Object} **label**

Attributes for the line label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Label](./Label.md)


### {Boolean | Object} **lastArrow**

Configure the arrow head at the position of its second point or the corresponding
intersection with the canvas border.
The attribute lastArrow can be a Boolean or an object with the following sub-attributes:

```
{
     type: 1, // possible values are 1, 2, ..., 7. Default value is 1.
     size: 6, // size of the arrow head. Default value is 6.
              // This value is multiplied with the strokeWidth of the line.
              // Exception: for type=7 size is ignored
     highlightSize: 6, // size of the arrow head in case the element is highlighted. Default value is 6.
}
```

type=7 is the default for curves if lastArrow: true

An arrow head can be turned off with line.setAttribute({lastArrow: false}).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Line#firstArrow](./Line.md#firstArrow)
:   [Line#touchLastPoint](./Line.md#touchLastPoint)


#### Default Value:

:   false


### {Number} **margin**

This number (pixel value) controls where infinite lines end at the canvas border. If zero, the line
ends exactly at the border, if negative there is a margin to the inside, if positive the line
ends outside of the canvas (which is invisible).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0


### {[Point](./Point.md)} **point1**

Attributes for first defining point of the line.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **point2**

Attributes for second defining point of the line.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {Number} **snapSizeX**

Defines together with [Point#snapSizeY](./Point.md#snapSizeY) the grid the point snaps on to.
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

If set to true, the point will snap to a grid defined by
[Point#snapSizeX](../symbols/Point.html#snapSizeX) and [Point#snapSizeY](./Point.md#snapSizeY).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#snapSizeX](./Point.md#snapSizeX)
:   [Point#snapSizeY](./Point.md#snapSizeY)


#### Default Value:

:   false


### {Boolean} **straightFirst**

If true, line stretches infinitely in direction of its first point.
Otherwise it ends at point1.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Line#straightLast](./Line.md#straightLast)


#### Default Value:

:   true


### {Boolean} **straightLast**

If true, line stretches infinitely in direction of its second point.
Otherwise it ends at point2.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Line#straightFirst](./Line.md#straightFirst)


#### Default Value:

:   true


### {Object} **ticks**

Attributes for ticks of the line.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Ticks](./Ticks.md)


### {Boolean} **touchFirstPoint**

If set to true, [Line#firstArrow](./Line.md#firstArrow) is set to true and the point is visible,
the arrow head will just touch the circle line of the start point of the line.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Line#firstArrow](./Line.md#firstArrow)


#### Default Value:

:   false


### {Boolean} **touchLastPoint**

If set to true, [Line#lastArrow](./Line.md#lastArrow) is set to true and the point is visible,
the arrow head will just touch the circle line of the start point of the line.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Line#firstArrow](./Line.md#firstArrow)


#### Default Value:

:   false
