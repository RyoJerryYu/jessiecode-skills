

# Mesh3D



## 描述

Display a rectangular mesh on a 3D plane element.   
  
*Defined in:*  [box3d.js](./src/src_3d_box3d.js.md).   
Extends [Curve](./Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Curve](./Curve.md)**  
            ↳ **Mesh3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Mesh3D](./Mesh3D.md#constructor)**  Create a (rectangular) mesh - i.e. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "mesh3d".  
  

Possible parent array combinations are:

{Array} **point** {Array} **direction1** {Array} **direction2** {Array} **range1** {Array} **range2**
:   point is an array of length 3 determining the starting point of the grid. direction1 and direction2 are arrays of length 3 for the directions of the grid. range1 and range2 (arrays of length 2) give the respective ranges. All parameters can be supplied as functions returning an appropriate data type.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[stepWidthU](./Mesh3D.md#stepWidthU)**  Step width of the mesh in the direction of the first spanning vector. |
|  | **[stepWidthV](./Mesh3D.md#stepWidthV)**  Step width of the mesh in the direction of the second spanning vector. |




### **stepWidthU**

Step width of the mesh in the direction of the first spanning vector.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   1


### **stepWidthV**

Step width of the mesh in the direction of the second spanning vector.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   1
