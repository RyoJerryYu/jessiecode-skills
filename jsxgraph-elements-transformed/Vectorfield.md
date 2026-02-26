

# Vectorfield



## 描述

A vector field on a plane can be visualized as a collection of arrows with given magnitudes and directions, each attached to a point on the plane.

Plot a vector field either given by two functions f1(x, y) and f2(x,y) or by a function f(x, y) returning an array of size 2.   
  
*Defined in:*  [vectorfield.js](./src/src_element_vectorfield.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Vectorfield**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Vectorfield](./Vectorfield.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "vectorfield".  
  

Possible parent array combinations are:

{Array|Function|String} **F**
:   Either an array containing two functions f1(x, y) and f2(x, y) or function f(x, y) returning an array of length 2.
  
  

{Array} **xData**
:   Array of length 3 containing start value for x, number of steps, end value of x. The vector field will contain (number of steps) + 1 vectors in direction of x.
  
  

{Array} **yData**
:   Array of length 3 containing start value for y, number of steps, end value of y. The vector field will contain (number of steps) + 1 vectors in direction of y.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.
Parameter options:


### 示例

```javascript
// Defining functions
var fx = (x, y) => Math.sin(y);
var fy = (x, y) => Math.cos(x);

var field = board.create('vectorfield', [
        [fx, fy],    // Defining function
        [-6, 25, 6], // Horizontal mesh
        [-5, 20, 5], // Vertical mesh
    ]);
```

```javascript
// Slider to control length of vectors
var s = board.create('slider', [[-3, 7], [3, 7], [0, 0.33, 1]], {name: 'length'});
// Slider to control number of steps
var stepsize = board.create('slider', [[-3, 6], [3, 6], [1, 20, 100]], {name: 'steps', snapWidth: 1});

// Defining functions
var fx = (x, y) => 0.2 * y;
var fy = (x, y) => 0.2 * (Math.cos(x) - 2) * Math.sin(x);

var field = board.create('vectorfield', [
        [fx, fy],        // Defining function
        [-6, () => stepsize.Value(), 6], // Horizontal mesh
        [-5, () => stepsize.Value(), 5], // Vertical mesh
    ], {
        highlightStrokeColor: JXG.palette.blue, // Make highlighting invisible

        scale: () => s.Value(), // Scaling of vectors

        arrowHead: {
            enabled: true,
            size: 8,  // Pixel length of arrow head
            angle: Math.PI / 16
        }
});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[arrowhead](./Vectorfield.md#arrowhead)**  Customize arrow heads of vectors. |
|  | **[scale](./Vectorfield.md#scale)**  Scaling factor of the vectors. |




### **arrowhead**

Customize arrow heads of vectors. Be careful! If enabled this will slow down the performance.
Fields are:

* enabled: Boolean
* size: length of the arrow head legs (in pixel)
* angle: angle of the arrow head legs In radians.

  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   {enabled: true, size: 5, angle: Math.PI \* 0.125}


### **scale**

Scaling factor of the vectors. This in contrast to slope fields, where this attribute sets the vector to the given length.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   Slopefield.scale


#### Default Value:

:   1


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
| <static> | Vectorfield.**[setF](./Vectorfield.md#.setF)**(func)  Set the defining functions of vector field. |




### <static> {Object} Vectorfield.**setF**(func)

Set the defining functions of vector field.


#### Parameters:

:   Either an array containing two functions f1(x, y) and f2(x, y) or function f(x, y) returning an array of length 2.


#### Returns:

:   {Object} Reference to the vector field object.


#### 示例

```javascript
field.setF([(x, y) => Math.sin(y), (x, y) => Math.cos(x)]);
board.update();
```
