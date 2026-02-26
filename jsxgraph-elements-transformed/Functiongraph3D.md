

# Functiongraph3D



## 描述

A 3D functiongraph visualizes a map (x, y) → f(x, y). The graph is a [Curve3D](./Curve3D.md) element.   
  
*Defined in:*  [surface3d.js](./src/src_3d_surface3d.js.md).   
Extends [ParametricSurface3D](./ParametricSurface3D.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Curve](./Curve.md)**  
         ↳ **[ParametricSurface3D](./ParametricSurface3D.md)**  
               ↳ **Functiongraph3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Functiongraph3D](./Functiongraph3D.md#constructor)**  A 3D function graph is defined by a function *F: R2 → R*. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "functiongraph3d".  
  

Possible parent array combinations are:

{Function|String} **F** {Array} **rangeX** {Array} **rangeY**
:   F(x,y) is a function returning a number (or a JessieCode string), rangeX is the array containing lower and upper bound for the range of x, rangeY is the array containing lower and upper bound for the range of y.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var box = [-5, 5];
var view = board.create('view3d',
    [
        [-6, -3], [8, 8],
        [box, box, box]
    ],
    {
        xPlaneRear: {visible: false},
        yPlaneRear: {visible: false},
    });

// Function F to be plotted
var F = (x, y) => Math.sin(x * y / 4);

// 3D surface
var c = view.create('functiongraph3d', [
    F,
    box, // () => [-s.Value()*5, s.Value() * 5],
    box, // () => [-s.Value()*5, s.Value() * 5],
], {
    strokeWidth: 0.5,
    stepsU: 70,
    stepsV: 70
});
```
