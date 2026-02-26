

# Circle3D



## 描述

A circle in 3D can be defined by various combinations of points and numbers.   
  
*Defined in:*  [circle3d.js](./src/src_3d_circle3d.js.md).   
Extends [JXG.Circle3D](./JXG.Circle3D.md).




## 继承关系

**[JXG.Curve3D](./JXG.Curve3D.md),JXG.GeometryElement**  
   ↳ **[JXG.Circle3D](./JXG.Circle3D.md)**  
         ↳ **Circle3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Circle3D](./Circle3D.md#constructor)**  In 3D space, a circle consists of all points on a given plane with a given distance from a given point. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "circle3d".  
  

Possible parent array combinations are:

{[JXG.Point](./JXG.Point.md)|Array|Function} **center** {Array|Function} **normal** {Number|Function} **radius**
:   The center must be given as a [JXG.Point](./JXG.Point.md), array or function (see [JXG.providePoints](./JXG.md#.providePoints)). The normal vector can be given as an array of four numbers (i.e. homogeneous coordinates [0, x, y, z]) or a function returning an array of length 4 and the radius can be given as a number (which will create a circle with a fixed radius) or a function.

    If the radius is supplied as a number or the output of a function, its absolute value is taken. When the radius evaluates to NaN, the circle does not display.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.
