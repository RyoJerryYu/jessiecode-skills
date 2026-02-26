

# Tapemeasure



## 描述

A tape measure can be used to measure distances between points.

The two defining points of the tape measure (which is a segment) do not inherit by default the attribute "visible" from the segment. Otherwise the tape meassure would be inaccessible if the two points coincide and the segment is hidden.   
  
*Defined in:*  [measure.js](./src/src_element_measure.js.md).   
Extends [Segment](./Segment.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
      ↳ **[Segment](./Segment.md)**  
            ↳ **Tapemeasure**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Tapemeasure](./Tapemeasure.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "tapemeasure".  
  

Possible parent array combinations are:
:   The two arrays give the initial position where the tape measure is drawn on the board.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a tape measure
var p1 = board.create('point', [0,0]);
var p2 = board.create('point', [1,1]);
var p3 = board.create('point', [3,1]);
var tape = board.create('tapemeasure', [[1, 2], [4, 2]], {name:'dist'});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[digits](./Tapemeasure.md#digits)**  The precision of the tape measure value displayed in the optional text. |
|  | **[label](./Tapemeasure.md#label)**  Attributes for the tape measure label. |
|  | **[point1](./Tapemeasure.md#point1)**  Attributes for first helper point defining the tape measure position. |
|  | **[point2](./Tapemeasure.md#point2)**  Attributes for second helper point defining the tape measure position. |
|  | **[precision](./Tapemeasure.md#precision)**  The precision of the tape measure value displayed in the optional text. |
|  | **[rotate](./Tapemeasure.md#rotate)**  Text rotation in degrees. |
|  | **[ticks](./Tapemeasure.md#ticks)**  Attributes for the ticks of the tape measure. |
|  | **[withLabel](./Tapemeasure.md#withLabel)**  Show tape measure label. |
|  | **[withTicks](./Tapemeasure.md#withTicks)**  Show tape measure ticks. |




### {Number} **digits**

The precision of the tape measure value displayed in the optional text.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   2


### {[Label](./Label.md)} **label**

Attributes for the tape measure label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **point1**

Attributes for first helper point defining the tape measure position.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **point2**

Attributes for second helper point defining the tape measure position.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {Number} **precision**

The precision of the tape measure value displayed in the optional text.
Replaced by the attribute digits
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Tapemeasure#digits](./Tapemeasure.md#digits)


#### Default Value:

:   2


### {Number} **rotate**

Text rotation in degrees.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0


### {[Ticks](./Ticks.md)} **ticks**

Attributes for the ticks of the tape measure.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {Boolean} **withLabel**

Show tape measure label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true


### {Boolean} **withTicks**

Show tape measure ticks.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[Value](./Tapemeasure.md#Value)**()  Returns the length of the tape measure. |




### {Number} **Value**()

Returns the length of the tape measure.


#### Returns:

:   {Number} length of tape measure.
