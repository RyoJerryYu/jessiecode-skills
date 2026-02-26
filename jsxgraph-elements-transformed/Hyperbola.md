

# Hyperbola



## 描述

A hyperbola is a special conic section given by two points (the foci) and a third point on the hyperbola or the length of the major axis.   
  
*Defined in:*  [conic.js](./src/src_element_conic.js.md).   
Extends [Conic](./Conic.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Conic](./Conic.md)**  
            ↳ **Hyperbola**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Hyperbola](./Hyperbola.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "hyperbola".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|array} **point1** {[JXG.Point](../symbols/JXG.Point.html)|array} **point2** {[JXG.Point](./JXG.Point.md)|array} **point3**
:   Parent elements can be three elements either of type [JXG.Point](./JXG.Point.md) or array of numbers describing the coordinates of a point. In the latter case the point will be constructed automatically as a fixed invisible point.
  
  

{[JXG.Point](../symbols/JXG.Point.html)|array} **point1** {[JXG.Point](./JXG.Point.md)|array} **point2** {number|function} **number**
:   Parent elements can be two elements either of type [JXG.Point](./JXG.Point.md) or array of numbers describing the coordinates of a point. The third parameter is a number/function which defines the length of the major axis
  
  

{Number} **start**
:   (Optional) parameter of the curve start, default: -π.
  
  

{Number} **end**
:   (Optional) parameter for the curve end, default: π.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create an Hyperbola by three points
var A = board.create('point', [-1,4]);
var B = board.create('point', [-1,-4]);
var C = board.create('point', [1,1]);
var el = board.create('hyperbola',[A,B,C]);
```
