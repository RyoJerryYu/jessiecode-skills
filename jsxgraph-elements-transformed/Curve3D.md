

# Curve3D



## 描述

3D Curves can be defined by mappings or by discrete data sets. In general, a 3D curve is a mapping from R to R^3, where t maps to (x(t),y(t),z(t)). The graph is drawn for t in the interval [a,b].   
  
*Defined in:*  [curve3d.js](./src/src_3d_curve3d.js.md).   
Extends [Curve](./Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Curve](./Curve.md)**  
            ↳ **Curve3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Curve3D](./Curve3D.md#constructor)**  A 3D parametric curve is defined by a function *F: R1 → R3*. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "curve3d".  
  

Possible parent array combinations are:

{Function} **FX** {Function} **FY** {Function} **FZ** {Array|Function} **range**
:   FX(u), FY(u), FZ(u) are functions returning a number, range is the array containing lower and upper bound for the range of the parameter u. range may also be a function returning an array of length two.
  
  

{Function} **F** {Array|Function} **range**
:   Alternatively: F[X,Y,Z](u) a function returning an array [x,y,z] of numbers, range as above.
  
  

{Array} **X** {Array} **Y** {Array} **Z**
:   Three arrays containing the coordinate points which define the curve.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// create a simple curve in 3d
var bound = [-1.5, 1.5];
var view=board.create('view3d',
    [[-4, -4],[8, 8],
    [bound, bound, bound]],
    {});
var curve = view.create('curve3d', [(u)=>Math.cos(u), (u)=>Math.sin(u), (u)=>(u/Math.PI)-1,[0,2*Math.PI] ]);
```
