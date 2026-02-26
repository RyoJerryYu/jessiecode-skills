

# Face3D



## 描述

This element creates a 3D face.   
  
*Defined in:*  [face3d.js](./src/src_3d_face3d.js.md).   
Extends [Curve](./Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Curve](./Curve.md)**  
            ↳ **Face3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Face3D](./Face3D.md#constructor)**  A 3D faces is TODO |




### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[shader](./Face3D.md#shader)**  Shading of faces. |




### {Object} **shader**

Shading of faces. For this, the HSL color scheme is used.
Two types are possible: either by 'angle' or by 'zIndex'.
By default (i.e. type:'angle'), the angle between the camera axis and the normal of the
face determines the lightness value of the HSL color. Otherwise, the
zIndex of the face determines the lightness value of the HSL color.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### See:

:   [View3D#depthOrder](./View3D.md#depthOrder)


#### Default Value:

:   ```
    {
     enabled: false,
     type: 'angle',   // 'angle', otherwise zIndex
     hue: 60,         // yellow
     saturation: 90,
     minLightness: 30,
     maxLightness: 90
    }
    ```


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[d](./Face3D.md#d)**  Hesse right hand side of the plane that contains the face. |
|  | **[faceNumber](./Face3D.md#faceNumber)**  Index of the face in the list of faces of the polyhedron |
|  | **[normal](./Face3D.md#normal)**  Normal vector for the face. |
|  | **[polyhedron](./Face3D.md#polyhedron)**  Link to the defining data of the parent polyhedron3d. |
|  | **[vec1](./Face3D.md#vec1)**  First basis vector of the face. |
|  | **[vec2](./Face3D.md#vec2)**  Second basis vector of the face. |




### {Number} **d**

Hesse right hand side of the plane that contains the face.


### {Number} **faceNumber**

Index of the face in the list of faces of the polyhedron


### {array} **normal**

Normal vector for the face. Array of length 4.


### {Object} **polyhedron**

Link to the defining data of the parent polyhedron3d.


#### See:

:   [Polyhedron3D#def](./Polyhedron3D.md#def)


### {Array} **vec1**

First basis vector of the face. Vector of length 4.


### {Array} **vec2**

Second basis vector of the face. Vector of length 4.


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
| <static> | Face3D.**[shader](./Face3D.md#.shader)**()  Determines the lightness of the face (in the HSL color scheme). |
|  | **[updateCoords](./Face3D.md#updateCoords)**()  Update the coordinates of all vertices of the polyhedron |
|  | **[updateDataArray2D](./Face3D.md#updateDataArray2D)**()  Update the 2D coordinates of the face and determine it's z-index. |




### <static> {Number} Face3D.**shader**()

Determines the lightness of the face (in the HSL color scheme).

Sets the fillColor of the adjoint 2D curve.


#### Returns:

:   {Number} zIndex of the face


### {[Face3D](./Face3D.md)} **updateCoords**()

Update the coordinates of all vertices of the polyhedron


#### Returns:

:   {[Face3D](./Face3D.md)} reference to itself


### {Object} **updateDataArray2D**()

Update the 2D coordinates of the face and determine it's z-index.


#### Returns:

:   {Object} {X:[], Y:[]}
