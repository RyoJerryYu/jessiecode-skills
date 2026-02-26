

# CurveUnion



## 描述

The path forming the union of two closed path elements. The elements may be of type curve, circle, polygon, inequality. If one element is a curve, it has to be closed. The resulting element is of type curve.   
  
*Defined in:*  [curve.js](./src/src_base_curve.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **CurveUnion**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[CurveUnion](./CurveUnion.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "curveunion".  
  

Possible parent array combinations are:

{[JXG.Curve](../symbols/JXG.Curve.html)|[JXG.Polygon](../symbols/JXG.Polygon.html)|[JXG.Circle](./JXG.Circle.md)} **curve1**
:   First element defining the union
  
  

{[JXG.Curve](../symbols/JXG.Curve.html)|[JXG.Polygon](../symbols/JXG.Polygon.html)|[JXG.Circle](./JXG.Circle.md)} **curve2**
:   Second element defining the union


### 示例

```javascript
var f = board.create('functiongraph', ['cos(x)']);
var ineq = board.create('inequality', [f], {inverse: true, fillOpacity: 0.1});
var circ = board.create('circle', [[0,0], 4]);
var clip = board.create('curveunion', [ineq, circ], {fillColor: 'yellow', fillOpacity: 0.6});
```
