

# Conic



## 描述

Create a generic conic section either by five points or the coefficients of the general conic's equation. If the conic section is defined by the coefficients of the equation

*Ax2+ Bxy+Cy2 + Dx + Ey + F = 0*




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Conic**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Conic](./Conic.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "conic".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|Array} **a** {[JXG.Point](../symbols/JXG.Point.html)|Array} **b** {[JXG.Point](../symbols/JXG.Point.html)|Array} **c** {[JXG.Point](../symbols/JXG.Point.html)|Array} **d** {[JXG.Point](./JXG.Point.md)|Array} **e**
:   Parent elements are five points.
  
  

{Number} **a00** {Number} **a11** {Number} **a22** {Number} **a01** {Number} **a02** {Number} **a12**
:   6 numbers, i.e. A, C, F, B/2, D/2, E/2


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a conic section through the points A, B, C, D, and E.
 var A = board.create('point', [1,5]);
 var B = board.create('point', [1,2]);
 var C = board.create('point', [2,0]);
 var D = board.create('point', [0,0]);
 var E = board.create('point', [-1,5]);
 var conic = board.create('conic',[A,B,C,D,E]);
```

```javascript
// Parameters: A, C, F, B/2, D/2, E/2
var conic = board.create('conic', [1, 2, -4, 0, 0, 0]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[center](./Conic.md#center)**  Attributes for center point. |
|  | **[foci](./Conic.md#foci)**  Attributes for foci points. |
|  | **[line](./Conic.md#line)**  Attributes for parabola line in case the line is given by two points or coordinate pairs. |
|  | **[point](./Conic.md#point)**  Attributes for five points defining the conic, if some of them are given as coordinates. |




### {[Point](./Point.md)} **center**

Attributes for center point.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **foci**

Attributes for foci points.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Line](./Line.md)} **line**

Attributes for parabola line in case the line is given by two
points or coordinate pairs.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **point**

Attributes for five points defining the conic, if some of them are given as coordinates.
  
*Defined in:*  [options.js](./src/src_options.js.md).
