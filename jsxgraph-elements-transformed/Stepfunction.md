

# Stepfunction



## 描述

A step function is a function graph that is piecewise constant. In case the data points should be updated after creation time, they can be accessed by curve.xterm and curve.yterm.   
  
*Defined in:*  [curve.js](./src/src_base_curve.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Stepfunction**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Stepfunction](./Stepfunction.md#constructor)**  JXG.Curve |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "stepfunction".  
  

Possible parent array combinations are:

{Array|Function} **Parent1**
:   elements of Stepfunction are two arrays containing the coordinates.
  
  

{Array|Function} **Parent2**


### 示例

```javascript
// Create step function.
     var curve = board.create('stepfunction', [[0,1,2,3,4,5], [1,3,0,2,2,1]]);
```
