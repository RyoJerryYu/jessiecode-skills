

# MinorArc



## 描述

A minor arc given by three points is that part of the circumference of a circle having measure at most 180 degrees (pi radians). It is defined by a center, one point that defines the radius, and a third point that defines the angle of the arc.   
  
*Defined in:*  [arc.js](./src/src_element_arc.js.md).   
Extends [Curve](./Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Curve](./Curve.md)**  
            ↳ **MinorArc**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[MinorArc](./MinorArc.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "minorarc".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p3**
:   . Minor arc is an arc of a circle around p1 having measure less than or equal to 180 degrees (pi radians) and starts at p2. The radius is determined by p2, the angle by p3.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create an arc out of three free points
var p1 = board.create('point', [2.0, 2.0]);
var p2 = board.create('point', [1.0, 0.5]);
var p3 = board.create('point', [3.5, 1.0]);

var a = board.create('arc', [p1, p2, p3]);
```
