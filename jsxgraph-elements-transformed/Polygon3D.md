

# Polygon3D



## 描述

A polygon is a sequence of points connected by lines, with the last point connecting back to the first one. The points are given by:

JSXGraph does not require and does not check planarity of the polygon.   
  
*Defined in:*  [polygon3d.js](./src/src_3d_polygon3d.js.md).   
Extends [JXG.Polygon3D](./JXG.Polygon3D.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.GeometryElement3D**  
   ↳ **[JXG.Polygon3D](./JXG.Polygon3D.md)**  
         ↳ **Polygon3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Polygon3D](./Polygon3D.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "polygon3d".  
  

Possible parent array combinations are:

{Array} **vertices**
:   The polygon's vertices.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.
