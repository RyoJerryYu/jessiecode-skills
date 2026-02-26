

# Axis3D



## 描述

A 3D axis element is a line together with optional ticks and labels.   
  
*Defined in:*  [box3d.js](./src/src_3d_box3d.js.md).   
Extends [Arrow](./Arrow.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
      ↳ **[Arrow](./Arrow.md)**  
            ↳ **Axis3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Axis3D](./Axis3D.md#constructor)**  Simple element 3d axis as used with "axesPosition:center". |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "axis3d".  
  

Possible parent array combinations are:

{Array} **start** {Array} **end**
:   Two arrays of length 3 for the start point and the end point of the axis.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.
