

# Slider



## 描述

A slider can be used to choose values from a given range of numbers.   
  
*Defined in:*  [slider.js](./src/src_element_slider.js.md).   
Extends [Glider](./Glider.md).




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Point](./JXG.Point.md)**  
      ↳ **[Glider](./Glider.md)**  
            ↳ **Slider**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Slider](./Slider.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "slider".  
  

Possible parent array combinations are:

{Array} **start** {Array} **end** {Array} **range**
:   The first two arrays give the start and the end where the slider is drawn on the board. The third array gives the start and the end of the range the slider operates as the first resp. the third component of the array. The second component of the third array gives its start value.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a slider with values between 1 and 10, initial position is 5.
var s = board.create('slider', [[1, 2], [3, 2], [1, 5, 10]]);
```

```javascript
// Create a slider taking integer values between 1 and 5. Initial value is 3.
var s = board.create('slider', [[1, 3], [3, 1], [0, 3, 5]], {
    snapWidth: 1,
    minTicksDistance: 60,
    drawLabels: false
});
```

```javascript
// Draggable slider
    var s1 = board.create('slider', [[-3, 1], [2, 1],[-10, 1, 10]], {
        visible: true,
        snapWidth: 2,
        point1: {fixed: false},
        point2: {fixed: false},
        baseline: {fixed: false, needsRegularUpdate: true}
    });
```

```javascript
// Set the slider by clicking on the base line: attribute 'moveOnUp'
    var s1 = board.create('slider', [[-3,1], [2,1],[-10,1,10]], {
        snapWidth: 2,
        moveOnUp: true // default value
    });
```

```javascript
// Set colors
var sl = board.create('slider', [[-3, 1], [1, 1], [-10, 1, 10]], {

  baseline: { strokeColor: 'blue'},
  highline: { strokeColor: 'red'},
  fillColor: 'yellow',
  label: {fontSize: 24, strokeColor: 'orange'},
  name: 'xyz', // Not shown, if suffixLabel is set
  suffixLabel: 'x = ',
  postLabel: ' u'

});
```

```javascript
// Create a "frozen" slider
var sli = board.create('slider', [[-4, 4], [-1.5, 4], [-10, 1, 10]], {
    name:'a',
    frozen: true
});
```

```javascript
// Use MathJax for slider label (don't forget to load MathJax)
var s = board.create('slider', [[-3, 2], [2, 2], [-10, 1, 10]], {
    name: 'A^{(2)}',
    suffixLabel: '\\(A^{(2)} = ',
    unitLabel: ' \\;km/h ',
    postLabel: '\\)',
    label: {useMathJax: true}
});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[baseline](./Slider.md#baseline)**  Attributes for the base line of the slider. |
|  | **[digits](./Slider.md#digits)**  The number of digits of the slider value displayed in the optional text. |
|  | **[highline](./Slider.md#highline)**  Attributes for the highlighting line of the slider. |
|  | **[intl](./Slider.md#intl)**  Internationalization support for slider labels. |
|  | **[label](./Slider.md#label)**  Attributes for the slider label. |
|  | **[moveOnUp](./Slider.md#moveOnUp)**  If true, 'up' events on the baseline will trigger slider moves. |
|  | **[point1](./Slider.md#point1)**  Attributes for first (left) helper point defining the slider position. |
|  | **[point2](./Slider.md#point2)**  Attributes for second (right) helper point defining the slider position. |
|  | **[postLabel](./Slider.md#postLabel)**  If not null, this is appended to the value and to unitLabel in the slider label. |
|  | **[precision](./Slider.md#precision)**  The precision of the slider value displayed in the optional text. |
|  | **[size](./Slider.md#size)**  Size of slider point. |
|  | **[snapValueDistance](./Slider.md#snapValueDistance)**  If the difference between the slider value and one of the elements of snapValues is less than this number (in user coordinate units), the slider will snap to that value. |
|  | **[snapValues](./Slider.md#snapValues)**  List of values to snap to. |
|  | **[snapWidth](./Slider.md#snapWidth)**  The slider only returns integer multiples of this value, e.g. |
|  | **[suffixLabel](./Slider.md#suffixLabel)**  If not null, this replaces the part "name = " in the slider label. |
|  | **[ticks](./Slider.md#ticks)**  Attributes for the ticks of the base line of the slider. |
|  | **[unitLabel](./Slider.md#unitLabel)**  If not null, this is appended to the value in the slider label. |
|  | **[withLabel](./Slider.md#withLabel)**  Show slider label. |
|  | **[withTicks](./Slider.md#withTicks)**  Show slider ticks. |




### {[Line](./Line.md)} **baseline**

Attributes for the base line of the slider.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {Number} **digits**

The number of digits of the slider value displayed in the optional text.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   2


### {[Line](./Line.md)} **highline**

Attributes for the highlighting line of the slider.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {object} **intl**

Internationalization support for slider labels.
  
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


### {[Label](./Label.md)} **label**

Attributes for the slider label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {Boolean} **moveOnUp**

If true, 'up' events on the baseline will trigger slider moves.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true


### {[Point](./Point.md)} **point1**

Attributes for first (left) helper point defining the slider position.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **point2**

Attributes for second (right) helper point defining the slider position.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {String} **postLabel**

If not null, this is appended to the value and to unitLabel in the slider label.
Possible types: string, number or function.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   JXG.Slider#suffixLabel
:   JXG.Slider#unitLabel


#### Default Value:

:   null


### {Number} **precision**

The precision of the slider value displayed in the optional text.
Replaced by the attribute "digits".
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Slider#digits](./Slider.md#digits)


#### Default Value:

:   2


### {Number} **size**

Size of slider point.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Point#size](./Point.md#size)


#### Default Value:

:   6


### {Number} **snapValueDistance**

If the difference between the slider value and one of the elements of snapValues is less
than this number (in user coordinate units), the slider will snap to that value.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Slider#snapValues](./Slider.md#snapValues)


#### Default Value:

:   0.0


### {Array} **snapValues**

List of values to snap to. If the glider is within snapValueDistance
(in user coordinate units) of one of these points,
then the glider snaps to that point.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Slider#snapValueDistance](./Slider.md#snapValueDistance)


#### Default Value:

:   empty


### {Number} **snapWidth**

The slider only returns integer multiples of this value, e.g. for discrete values set this property to 1. For
continuous results set this to -1.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {String} **suffixLabel**

If not null, this replaces the part "name = " in the slider label.
Possible types: string, number or function.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   JXG.Slider#unitLabel
:   JXG.Slider#postLabel


#### Default Value:

:   null


### {[Ticks](./Ticks.md)} **ticks**

Attributes for the ticks of the base line of the slider.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {String} **unitLabel**

If not null, this is appended to the value in the slider label.
Possible types: string, number or function.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   JXG.Slider#suffixLabel
:   JXG.Slider#postLabel


#### Default Value:

:   null


### {Boolean} **withLabel**

Show slider label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true


### {Boolean} **withTicks**

Show slider ticks.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[\_smax](./Slider.md#_smax)**  End value of the slider range. |
|  | **[\_smin](./Slider.md#_smin)**  Start value of the slider range. |




### {Number} **\_smax**

End value of the slider range.


### {Number} **\_smin**

Start value of the slider range.


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[setMax](./Slider.md#setMax)**(val)  Sets the maximum value of the slider. |
|  | **[setMin](./Slider.md#setMin)**(val)  Sets the minimum value of the slider. |
|  | **[setValue](./Slider.md#setValue)**(val)  Sets the value of the slider. |
|  | **[Value](./Slider.md#Value)**()  Returns the current slider value. |




### {Object} **setMax**(val)

Sets the maximum value of the slider.


#### Parameters:

:   New maximum value


#### Returns:

:   {Object} this object


### {Object} **setMin**(val)

Sets the minimum value of the slider.


#### Parameters:

:   New minimum value


#### Returns:

:   {Object} this object


### {Object} **setValue**(val)

Sets the value of the slider. This call must be followed
by a board update call.


#### Parameters:

:   New value


#### Returns:

:   {Object} this object


### {Number} **Value**()

Returns the current slider value.


#### Returns:

:   {Number}
