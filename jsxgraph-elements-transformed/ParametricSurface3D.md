

# ParametricSurface3D



## 描述

A 3D parametric surface visualizes a map (u, v) → [X(u, v), Y(u, v), Z(u, v)].   
  
*Defined in:*  [surface3d.js](./src/src_3d_surface3d.js.md).   
Extends [Curve](./Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Curve](./Curve.md)**  
            ↳ **ParametricSurface3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[ParametricSurface3D](./ParametricSurface3D.md#constructor)**  A 3D parametric surface is defined by a function *F: R2 → R3*. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "parametricsurface3d".  
  

Possible parent array combinations are:

{Function} **FX** {Function} **FY** {Function} **FZ** {Array|Function} **rangeU** {Array|Function} **rangeV**
:   FX(u,v), FY(u,v), FZ(u,v) are functions returning a number, rangeU is the array containing lower and upper bound for the range of parameter u, rangeV is the array containing lower and upper bound for the range of parameter v. rangeU and rangeV may also be functions returning an array of length two.
  
  

{Function} **F** {Array|Function} **rangeU** {Array|Function} **rangeV**
:   Alternatively: F[X,Y,Z](u,v) a function returning an array [x,y,z] of numbers, rangeU and rangeV as above.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var view = board.create('view3d',
		        [[-6, -3], [8, 8],
		        [[-5, 5], [-5, 5], [-5, 5]]]);

// Sphere
var c = view.create('parametricsurface3d', [
    (u, v) => 2 * Math.sin(u) * Math.cos(v),
    (u, v) => 2 * Math.sin(u) * Math.sin(v),
    (u, v) => 2 * Math.cos(u),
    [0, 2 * Math.PI],
    [0, Math.PI]
], {
    strokeColor: '#ff0000',
    stepsU: 30,
    stepsV: 30
});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[stepsU](./ParametricSurface3D.md#stepsU)**  Number of intervals the mesh is divided into in direction of parameter u. |
|  | **[stepsV](./ParametricSurface3D.md#stepsV)**  Number of intervals the mesh is divided into in direction of parameter v. |




### {Number} **stepsU**

Number of intervals the mesh is divided into in direction of parameter u.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {Number} **stepsV**

Number of intervals the mesh is divided into in direction of parameter v.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).
