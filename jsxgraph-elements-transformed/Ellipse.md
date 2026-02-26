

# Ellipse



## 描述

An ellipse is a special conic section given by two points (the foci) and a third point on the ellipse or the length of the major axis.   
  
*Defined in:*  [conic.js](./src/src_element_conic.js.md).   
Extends [Conic](./Conic.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Conic](./Conic.md)**  
            ↳ **Ellipse**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Ellipse](./Ellipse.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "ellipse".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|array} **point1** {[JXG.Point](../symbols/JXG.Point.html)|array} **point2** {[JXG.Point](./JXG.Point.md)|array} **point3**
:   Parent elements can be three elements either of type [JXG.Point](./JXG.Point.md) or array of numbers describing the coordinates of a point. In the latter case the point will be constructed automatically as a fixed invisible point.
  
  

{[JXG.Point](../symbols/JXG.Point.html)|array} **point1** {[JXG.Point](./JXG.Point.md)|array} **point2** {number|function} **number**
:   Parent elements can be two elements either of type [JXG.Point](./JXG.Point.md) or array of numbers describing the coordinates of a point. The third parameter is a number/function which defines the length of the major axis
  
  

{Number} **start**
:   (Optional) parameter of the curve start, default: 0.
  
  

{Number} **end**
:   (Optional) parameter for the curve end, default: 2π.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create an Ellipse by three points
var A = board.create('point', [-1,4]);
var B = board.create('point', [-1,-4]);
var C = board.create('point', [1,1]);
var el = board.create('ellipse',[A,B,C]);
```

```javascript
// Create an elliptical arc
var p1 = board.create('point', [-1, 2]);
var p2 = board.create('point', [ 1, 2]);
var p3 = board.create('point', [0, 3]);

var ell = board.create('ellipse', [
  p1, p2, p3, 0, Math.PI], {
  lastArrow: {type: 7}
});
```
