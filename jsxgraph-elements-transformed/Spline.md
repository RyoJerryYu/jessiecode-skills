

# Spline



## 描述

The (natural) cubic spline curves (function graph) interpolating a set of points. Create a dynamic spline interpolated curve given by sample points p\_1 to p\_n.   
  
*Defined in:*  [curve.js](./src/src_base_curve.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Spline**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Spline](./Spline.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "spline".  
  

Possible parent array combinations are:

{[JXG.Board](./JXG.Board.md)} **board**
:   Reference to the board the spline is drawn on.
  
  

{Array} **parents**
:   Array of points the spline interpolates. This can be

    * an array of JSXGraph points
    * an array of coordinate pairs
    * an array of functions returning coordinate pairs
    * an array consisting of an array with x-coordinates and an array of y-coordinates

    All individual entries of coordinates arrays may be numbers or functions returning numbers.
  
  

{Object} **attributes**
:   Define color, width, ... of the spline


### 示例

```javascript
var p = [];
p[0] = board.create('point', [-2,2], {size: 4, face: 'o'});
p[1] = board.create('point', [0,-1], {size: 4, face: 'o'});
p[2] = board.create('point', [2,0], {size: 4, face: 'o'});
p[3] = board.create('point', [4,1], {size: 4, face: 'o'});

var c = board.create('spline', p, {strokeWidth:3});
```
