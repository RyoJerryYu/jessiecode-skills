

# Integral



## 描述

The graph of the integral function of a given function in a given interval.   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Integral**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Integral](./Integral.md#constructor)**  The Integral element is used to visualize the area under a given curve over a given interval and to calculate the area's value. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "integral".  
  

Possible parent array combinations are:

{Array} **i** {[JXG.Curve](./JXG.Curve.md)} **c**
:   The constructed element covers the area between the curve c and the x-axis within the interval i.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var c1 = board.create('functiongraph', [function (t) { return Math.cos(t)*t; }]);
var i1 = board.create('integral', [[-2.0, 2.0], c1]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[baseLeft](./Integral.md#baseLeft)**  Attributes of the (left) base point of the integral. |
|  | **[baseRight](./Integral.md#baseRight)**  Attributes of the (right) base point of the integral. |
|  | **[curveLeft](./Integral.md#curveLeft)**  Attributes of the (left) starting point of the integral. |
|  | **[curveRight](./Integral.md#curveRight)**  Attributes of the (right) end point of the integral. |
|  | **[label](./Integral.md#label)**  Attributes for integral label. |




### {[Point](./Point.md)} **baseLeft**

Attributes of the (left) base point of the integral.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Integral#curveLeft](./Integral.md#curveLeft)


### {[Point](./Point.md)} **baseRight**

Attributes of the (right) base point of the integral.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Integral#curveRight](./Integral.md#curveRight)


### {[Point](./Point.md)} **curveLeft**

Attributes of the (left) starting point of the integral.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Integral#baseLeft](./Integral.md#baseLeft)


### {[Point](./Point.md)} **curveRight**

Attributes of the (right) end point of the integral.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Integral#baseRight](./Integral.md#baseRight)


### {[Label](./Label.md)} **label**

Attributes for integral label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   ```
    {
         fontSize: 20,
         digits: 4,
         intl: {
             enabled: false,
             options: {}
         }
       }
    ```


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
| <static> | Integral.**[baseLeft](./Integral.md#.baseLeft)**  The point on the axis initially corresponding to the lower value of the interval. |
| <static> | Integral.**[baseRight](./Integral.md#.baseRight)**  The point on the axis initially corresponding to the higher value of the interval. |
| <static> | Integral.**[curveLeft](./Integral.md#.curveLeft)**  The glider on the curve corresponding to the lower value of the interval. |
| <static> | Integral.**[curveRight](./Integral.md#.curveRight)**  The glider on the axis corresponding to the higher value of the interval. |




### <static> {[JXG.Point](./JXG.Point.md)} Integral.**baseLeft**

The point on the axis initially corresponding to the lower value of the interval.


### <static> {[JXG.Point](./JXG.Point.md)} Integral.**baseRight**

The point on the axis initially corresponding to the higher value of the interval.


### <static> {[Glider](./Glider.md)} Integral.**curveLeft**

The glider on the curve corresponding to the lower value of the interval.


### <static> {[Glider](./Glider.md)} Integral.**curveRight**

The glider on the axis corresponding to the higher value of the interval.


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
| <static> | Integral.**[Value](./Integral.md#.Value)**()  Returns the current value of the integral. |




### <static> {Number} Integral.**Value**()

Returns the current value of the integral.


#### Returns:

:   {Number}
