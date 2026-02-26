

# Slopetriangle



## 描述

Slope triangle to visualize the slope of a tangent to a curve, circle or line.   
  
*Defined in:*  [slopetriangle.js](./src/src_element_slopetriangle.js.md).   
Extends [JXG.Line](./JXG.Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
         ↳ **Slopetriangle**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Slopetriangle](./Slopetriangle.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "slopetriangle".  
  

Possible parent array combinations are:

{[JXG.Line](./JXG.Line.md)} **t**
:   A tangent based on a glider on some object, e.g. curve, circle, line or turtle.
  
  

{[JXG.Line](../symbols/JXG.Line.html)} **li** {[JXG.Point](./JXG.Point.md)}
:   p A line and a point on that line. The user has to take care that the point is a member of the line.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.
Parameter options:


### 示例

```javascript
// Create a slopetriangle on a tangent
var f = board.create('plot', ['sin(x)']),
    g = board.create('glider', [1, 2, f]),
    t = board.create('tangent', [g]),

    st = board.create('slopetriangle', [t]);
```

```javascript
// Create a on a line and a point on that line
var p1 = board.create('point', [-2, 3]),
    p2 = board.create('point', [2, -3]),
    li = board.create('line', [p1, p2]),
    p = board.create('glider', [0, 0, li]),

    st = board.create('slopetriangle', [li, p]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[baseline](./Slopetriangle.md#baseline)**  Attributes for the base line. |
|  | **[basepoint](./Slopetriangle.md#basepoint)**  Attributes for the base point. |
|  | **[glider](./Slopetriangle.md#glider)**  Attributes for the gliding helper point. |
|  | **[label](./Slopetriangle.md#label)**  Attributes for the slope triangle label. |
|  | **[tangent](./Slopetriangle.md#tangent)**  Attributes for the tangent. |
|  | **[toppoint](./Slopetriangle.md#toppoint)**  Attributes for the top point. |




### {[Line](./Line.md)} **baseline**

Attributes for the base line.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **basepoint**

Attributes for the base point.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **glider**

Attributes for the gliding helper point.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Label](./Label.md)} **label**

Attributes for the slope triangle label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Line](./Line.md)} **tangent**

Attributes for the tangent.
The tangent is constructed by slop triangle if the construction
is based on a glider, solely.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **toppoint**

Attributes for the top point.
  
*Defined in:*  [options.js](./src/src_options.js.md).


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[Direction](./Slopetriangle.md#Direction)**()  Returns the direction of the slope triangle, that is the direction of the tangent. |
|  | **[Value](./Slopetriangle.md#Value)**()  Returns the value of the slope triangle, that is the slope of the tangent. |




### {Number} **Direction**()

Returns the direction of the slope triangle, that is the direction of the tangent.


#### Returns:

:   {Number} slope of the tangent.


#### See:

:   Line#Direction


### {Number} **Value**()

Returns the value of the slope triangle, that is the slope of the tangent.


#### Returns:

:   {Number} slope of the tangent.
