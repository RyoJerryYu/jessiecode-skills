

# Comb



## 描述

A marker to display domains of inequalities. The comb element is defined by two points.   
  
*Defined in:*  [comb.js](./src/src_element_comb.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Comb**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Comb](./Comb.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "comb".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|array|function} **point1** {[JXG.Point](./JXG.Point.md)|array|function} **point2**
:   Parent elements can be two elements either of type [JXG.Point](./JXG.Point.md) or array of numbers describing the coordinates of a point. In the latter case the point will be constructed automatically as a fixed invisible point. It is possible to provide a function returning an array or a point, instead of providing an array or a point.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent
 objects an exception is thrown.
Parameter options:


### 示例

```javascript
// Create a simple horizontal comb with invisible endpoints
var c = board.create('comb', [[1, 0], [3, 0]]);
```

```javascript
var p1 = board.create('glider', [-3, 0, board.defaultAxes.x]);
var p2 = board.create('glider', [-1, 0, board.defaultAxes.x]);
var c1 = board.create('comb', [p1, p2], {width: 0.2, frequency: 0.1, angle: Math.PI / 4});
```

```javascript
var s = board.create('slider', [[1,3], [4,3], [0.1, 0.3, 0.8]]);
var p1 = board.create('glider', [-3, 0, board.defaultAxes.x]);
var p2 = board.create('glider', [-1, 0, board.defaultAxes.x]);
var c1 = board.create('comb', [p1, p2], {
    width: function(){ return 4*s.Value(); },
    reverse: function(){ return (s.Value()<0.5) ? false : true; },
    frequency: function(){ return s.Value(); },
    angle: function(){ return s.Value() * Math.PI / 2; },
    curve: {
        strokeColor: 'red'
    }
});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[angle](./Comb.md#angle)**  Angle - given in radians - under which comb elements are positioned. |
|  | **[frequency](./Comb.md#frequency)**  Frequency of comb elements. |
|  | **[point1](./Comb.md#point1)**  Attributes for first defining point of the comb. |
|  | **[point2](./Comb.md#point2)**  Attributes for second defining point of the comb. |
|  | **[reverse](./Comb.md#reverse)**  Should the comb go right to left instead of left to right. |
|  | **[width](./Comb.md#width)**  Width of the comb. |




### {Number} **angle**

Angle - given in radians - under which comb elements are positioned.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   Math.PI / 3 (i.e. π /3 or 60^° degrees)


### {Number} **frequency**

Frequency of comb elements.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.2


### {[Point](./Point.md)} **point1**

Attributes for first defining point of the comb.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **point2**

Attributes for second defining point of the comb.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {Boolean} **reverse**

Should the comb go right to left instead of left to right.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {Number} **width**

Width of the comb.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.4
