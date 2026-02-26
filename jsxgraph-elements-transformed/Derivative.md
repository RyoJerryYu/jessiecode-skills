

# Derivative



## 描述

A curve visualizing the function graph of the (numerical) derivative of a given curve.   
  
*Defined in:*  [curve.js](./src/src_base_curve.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Derivative**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Derivative](./Derivative.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "derivative".  
  

Possible parent array combinations are:

{[JXG.Curve](./JXG.Curve.md)} **Parent**
:   Curve for which the derivative is generated.


### 示例

```javascript
var cu = board.create('cardinalspline', [[[-3,0], [-1,2], [0,1], [2,0], [3,1]], 0.5, 'centripetal'], {createPoints: false});
var d = board.create('derivative', [cu], {dash: 2});
```
