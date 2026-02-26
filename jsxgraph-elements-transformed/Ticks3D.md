

# Ticks3D



## 描述

Ticks are used as distance markers on a line in a 3D view.   
  
*Defined in:*  [ticks3d.js](./src/src_3d_ticks3d.js.md).   
Extends [Curve](./Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Curve](./Curve.md)**  
            ↳ **Ticks3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Ticks3D](./Ticks3D.md#constructor)**  Create 3D ticks. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "ticks3d".  
  

Possible parent array combinations are:

{Array} **point** {Array} **direction1** {Number} **length** {Array} **direction2**
:   point is an array of length 3 determining the starting point of the grid. direction1 and direction2 are arrays of length 3. Here, direction1 is the direction of the 3D line, direction2 is the direction of the ticks. "length" is the length of the line. All parameters can be supplied as functions returning an appropriate data type.

    The step width of the ticks is determined by the attribute "ticksDistance".


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.
