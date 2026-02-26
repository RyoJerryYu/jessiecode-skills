

# Tracecurve



## 描述

A trace curve is simple locus curve showing the orbit of a point that depends on a glider point.   
  
*Defined in:*  [curve.js](./src/src_base_curve.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Tracecurve**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Tracecurve](./Tracecurve.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "tracecurve".  
  

Possible parent array combinations are:

{[Point](./Point.md)} **Parent**
:   elements of Tracecurve are a glider point and a point whose locus is traced.
  
  

{point}


### 示例

```javascript
// Create trace curve.
var c1 = board.create('circle',[[0, 0], [2, 0]]),
p1 = board.create('point',[-3, 1]),
g1 = board.create('glider',[2, 1, c1]),
s1 = board.create('segment',[g1, p1]),
p2 = board.create('midpoint',[s1]),
curve = board.create('tracecurve', [g1, p2]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[numberPoints](./Tracecurve.md#numberPoints)**  The number of evaluated data points. |




### {Number} **numberPoints**

The number of evaluated data points.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   100
