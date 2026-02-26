

# Vectorfield3D



## 描述

A vector field is an assignment of a vector to each point in 3D space.

Plot a vector field either given by three functions f1(x, y, z), f2(x, y, z), and f3(x, y, z) or by a function f(x, y, z) returning an array of size 3.   
  
*Defined in:*  [curve3d.js](./src/src_3d_curve3d.js.md).   
Extends [JXG.Curve3D](./JXG.Curve3D.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.GeometryElement3D**  
   ↳ **[JXG.Curve3D](./JXG.Curve3D.md)**  
         ↳ **Vectorfield3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Vectorfield3D](./Vectorfield3D.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "vectorfield3d".  
  

Possible parent array combinations are:

{Array|Function|String} **F**
:   Either an array containing three functions f1(x, y, z), f2(x, y, z), and f3(x, y) or function f(x, y, z) returning an array of length 3.
  
  

{Array} **xData**
:   Array of length 3 containing start value for x, number of steps, end value of x. The vector field will contain (number of steps) + 1 vectors in direction of x.
  
  

{Array} **yData**
:   Array of length 3 containing start value for y, number of steps, end value of y. The vector field will contain (number of steps) + 1 vectors in direction of y.
  
  

{Array} **zData**
:   Array of length 3 containing start value for z, number of steps, end value of z. The vector field will contain (number of steps) + 1 vectors in direction of z.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.
Parameter options:


### 示例

```javascript
const view = board.create('view3d',
    [
        [-6, -3],
        [8, 8],
        [[-3, 3], [-3, 3], [-3, 3]]
    ], {});

var vf = view.create('vectorfield3d', [
    [(x, y, z) => Math.cos(y), (x, y, z) => Math.sin(x), (x, y, z) => z],
    [-2, 5, 2], // x from -2 to 2 in 5 steps
    [-2, 5, 2], // y
    [-2, 5, 2] // z
], {
    strokeColor: 'red',
    scale: 0.5
});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[arrowhead](./Vectorfield3D.md#arrowhead)**  Customize arrow heads of vectors. |
|  | **[scale](./Vectorfield3D.md#scale)**  Scaling factor of the vectors. |




### **arrowhead**

Customize arrow heads of vectors. Be careful! If enabled this will slow down the performance.
Fields are:

* enabled: Boolean
* size: length of the arrow head legs (in pixel)
* angle: angle of the arrow head legs In radians.

  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   {enabled: true, size: 5, angle: Math.PI \* 0.125}


### **scale**

Scaling factor of the vectors. This in contrast to slope fields, where this attribute sets the vector to the given length.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### See:

:   Slopefield.scale


#### Default Value:

:   1


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
| <static> | Vectorfield3D.**[setF](./Vectorfield3D.md#.setF)**(func)  Set the defining functions of 3D vector field. |




### <static> {Object} Vectorfield3D.**setF**(func)

Set the defining functions of 3D vector field.


#### Parameters:

:   Either an array containing three functions f1(x, y, z),
    f2(x, y, z), and f3(x, y, z) or function f(x, y, z) returning an array of length 3.


#### Returns:

:   {Object} Reference to the 3D vector field object.


#### 示例

```javascript
field.setF([(x, y, z) => Math.sin(y), (x, y, z) => Math.cos(x), (x, y, z) => z]);
board.update();
```
