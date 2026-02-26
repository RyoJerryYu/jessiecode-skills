

# Measurement



## 描述

Display measurements of geometric elements and the arithmetic operations of measurements. Under the hood this is a text element which has a method Value. The text to be displayed is the result of the evaluation of a prefix expression, see [JXG.PrefixParser](./JXG.PrefixParser.md).

The purpose of this element is to display values of measurements of geometric objects, like the radius of a circle, as well as expressions consisting of measurements.   
  
*Defined in:*  [measure.js](./src/src_element_measure.js.md).   
Extends [Text](./Text.md).




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Text](./JXG.Text.md)**  
      ↳ **[Text](./Text.md)**  
            ↳ **Measurement**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Measurement](./Measurement.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "measurement".  
  

Possible parent array combinations are:

{[Point](../symbols/Point.html)|Array} **x** {[Point](./Point.md)|Array} **y** {Array} **expression**
:   Here, expression is a prefix expression, see [JXG.PrefixParser](./JXG.PrefixParser.md).


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [1, 1]);
var p2 = board.create('point', [1, 3]);
var ci1 = board.create('circle', [p1, p2]);

var m1 = board.create('measurement', [1, -2, ['Area', ci1]], {
    visible: true,
    prefix: 'area: ',
    baseUnit: 'cm'
});

var m2 = board.create('measurement', [1, -4, ['Radius', ci1]], {
    prefix: 'radius: ',
    baseUnit: 'cm'
});
```

```javascript
var p1 = board.create('point', [1, 1]);
var p2 = board.create('point', [1, 3]);
var ci1 = board.create('circle', [p1, p2]);
var seg = board.create('segment', [[-2,-3], [-2, 3]], { firstArrow: true, lastArrow: true});
var sli = board.create('slider', [[-4, 4], [-1.5, 4], [-10, 1, 10]], {name:'a'});

var m1 = board.create('measurement', [-6, -2, ['Radius', ci1]], {
    prefix: 'm1: ',
    baseUnit: 'cm'
});

var m2 = board.create('measurement', [-6, -4, ['L', seg]], {
    prefix: 'm2: ',
    baseUnit: 'cm'
});

var m3 = board.create('measurement', [-6, -6, ['V', sli]], {
    prefix: 'm3: ',
    baseUnit: 'cm',
    dim: 1
});

var m4 = board.create('measurement', [2, -6,
        ['+', ['V', m1], ['V', m2], ['V', m3]]
    ], {
    prefix: 'm4: ',
    baseUnit: 'cm'
});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[baseUnit](./Measurement.md#baseUnit)**  This specifies the unit of measurement in dimension 1 (e.g. |
|  | **[dim](./Measurement.md#dim)**  Dimension of the measured data. |
|  | **[formatCoords](./Measurement.md#formatCoords)**  Function to format coordinates. |
|  | **[formatDirection](./Measurement.md#formatDirection)**  Function to format direction vector. |
|  | **[prefix](./Measurement.md#prefix)**  String that is displayed before the measurement and its unit. |
|  | **[showPrefix](./Measurement.md#showPrefix)**  Determines whether a prefix is displayed before the measurement value and unit. |
|  | **[showSuffix](./Measurement.md#showSuffix)**  Determines whether a suffix is displayed after the measurement value and unit. |
|  | **[suffix](./Measurement.md#suffix)**  String that is displayed after the measurement and its unit. |
|  | **[units](./Measurement.md#units)**  This attribute expects an object that has the dimension numbers as keys (as integer or in the form of "dimxx") and assigns a string to each dimension. |




### {String} **baseUnit**

This specifies the unit of measurement in dimension 1 (e.g. length).
A power is automatically added to the string.
If you want to use different units for each dimension, see [Measurement#units](./Measurement.md#units).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Measurement#units](./Measurement.md#units)


#### Default Value:

:   ''


### {Number|'coords'|'direction'} **dim**

Dimension of the measured data. This measurement can only be combined with a measurement of a suitable dimension.
Overwrites the dimension returned by the Dimension() method.
Normally, the default value null is used here to automatically determine the dimension.
However, if the coordinates or a direction vector are measured, the value is usually returned as an array.
To tell the measurement that the function [Measurement#formatCoords](../symbols/Measurement.html#formatCoords) or [Measurement#formatDirection](./Measurement.md#formatDirection) should be used
to display the array properly, 'coords' or 'direction' must be specified here.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Measurement#formatCoords](./Measurement.md#formatCoords)
:   [Measurement#formatDirection](./Measurement.md#formatDirection)


#### Default Value:

:   null


### {Function} **formatCoords**

Function to format coordinates. Does only have an effect, if [Measurement#dim](./Measurement.md#dim) is set to 'coords'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Measurement#dim](./Measurement.md#dim)


### {Function} **formatDirection**

Function to format direction vector. Does only have an effect, if [Measurement#dim](./Measurement.md#dim) is set to 'direction'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {String} **prefix**

String that is displayed before the measurement and its unit.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Measurement#showPrefix](./Measurement.md#showPrefix)


#### Default Value:

:   ''


### {Boolean} **showPrefix**

Determines whether a prefix is displayed before the measurement value and unit.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Measurement#prefix](./Measurement.md#prefix)


#### Default Value:

:   true


### {Boolean} **showSuffix**

Determines whether a suffix is displayed after the measurement value and unit.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Measurement#suffix](./Measurement.md#suffix)


#### Default Value:

:   true


### {String} **suffix**

String that is displayed after the measurement and its unit.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Measurement#showSuffix](./Measurement.md#showSuffix)


#### Default Value:

:   ''


### {Object} **units**

This attribute expects an object that has the dimension numbers as keys (as integer or in the form of "dimxx")
and assigns a string to each dimension.
If a dimension has no specification, [Measurement#baseUnit](./Measurement.md#baseUnit) is used.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Measurement#baseUnit](./Measurement.md#baseUnit)
