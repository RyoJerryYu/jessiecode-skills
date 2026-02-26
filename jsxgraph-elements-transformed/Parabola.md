

# Parabola



## 描述

A parabola is a special conic section given by one point (the focus) and a line (the directrix).   
  
*Defined in:*  [conic.js](./src/src_element_conic.js.md).   
Extends [Conic](./Conic.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Conic](./Conic.md)**  
            ↳ **Parabola**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Parabola](./Parabola.md#constructor)**  JXG.Curve |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "parabola".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|array} **point** {[JXG.Line](./JXG.Line.md)} **line**
:   Parent elements are a point and a line or a pair of coordinates. Optional parameters three and four are numbers which define the curve length (e.g. start/end). Default values are -pi and pi.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a parabola by a point C and a line l.
var A = board.create('point', [-1,4]);
var B = board.create('point', [-1,-4]);
var l = board.create('line', [A,B]);
var C = board.create('point', [1,1]);
var el = board.create('parabola',[C,l]);
```

```javascript
var par = board.create('parabola',[[3.25, 0], [[0.25, 1],[0.25, 0]]]);
```
