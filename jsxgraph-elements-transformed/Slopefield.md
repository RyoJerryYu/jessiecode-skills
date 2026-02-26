

# Slopefield



## 描述

A slope field is a graphical representation of the solutions to a first-order differential equation of a scalar function.

Plot a slope field given by a function f(x, y) returning a number.   
  
*Defined in:*  [vectorfield.js](./src/src_element_vectorfield.js.md).   
Extends [Vectorfield](./Vectorfield.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Vectorfield](./Vectorfield.md)**  
            ↳ **Slopefield**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Slopefield](./Slopefield.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "slopefield".  
  

Possible parent array combinations are:

{Function|String} **F**
:   Function f(x, y) returning a number.
  
  

{Array} **xData**
:   Array of length 3 containing start value for x, number of steps, end value of x. The slope field will contain (number of steps) + 1 vectors in direction of x.
  
  

{Array} **yData**
:   Array of length 3 containing start value for y, number of steps, end value of y. The slope field will contain (number of steps) + 1 vectors in direction of y.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.
Parameter options:


### 示例

```javascript
var field = board.create('slopefield', [
    (x, y) => x * x - x - 2,
    [-6, 25, 6], // Horizontal mesh
    [-5, 20, 5]  // Vertical mesh
]);
```

```javascript
// Slider to control length of vectors
var s = board.create('slider', [[-3, 7], [3, 7], [0, 0.33, 1]], {name: 'length'});
// Slider to control number of steps
var stepsize = board.create('slider', [[-3, 6], [3, 6], [1, 20, 100]], {name: 'steps', snapWidth: 1});

var field = board.create('slopefield', [
    (x, y) => x * x - y * y,
    [-6, () => stepsize.Value(), 6],
    [-5, () => stepsize.Value(), 5]],
    {
        strokeWidth: 1.5,
        highlightStrokeWidth: 0.5,
        highlightStrokeColor: JXG.palette.blue,

        scale: () => s.Value(),

        arrowHead: {
            enabled: false,
            size: 8,
            angle: Math.PI / 16
        }
    });
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[arrowhead](./Slopefield.md#arrowhead)**  Customize arrow heads of vectors. |
|  | **[scale](./Slopefield.md#scale)**  Set length of the vectors in user coordinates. |




### **arrowhead**

Customize arrow heads of vectors. Be careful! If enabled this will slow down the performance.
Fields are:

* enabled: Boolean
* size: length of the arrow head legs (in pixel)
* angle: angle of the arrow head legs In radians.

  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   {enabled: false, size: 5, angle: Math.PI \* 0.125}


### **scale**

Set length of the vectors in user coordinates. This in contrast to vector fields, where this attribute just scales the vector.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   Vectorfield.scale


#### Default Value:

:   1


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[setF](./Slopefield.md#setF)**(func)  Set the defining functions of slope field. |




### {Object} **setF**(func)

Set the defining functions of slope field.


#### Parameters:

:   Function f(x, y) returning a number.


#### Returns:

:   {Object} Reference to the slope field object.


#### 示例

```javascript
field.setF((x, y) => x * x + y * y);
board.update();
```
