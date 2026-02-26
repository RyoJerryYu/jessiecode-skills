

# CircumcircleArc



## 描述

A partial circum circle through three points.   
  
*Defined in:*  [arc.js](./src/src_element_arc.js.md).   
Extends [Arc](./Arc.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Curve](./Curve.md)**  
         ↳ **[Arc](./Arc.md)**  
               ↳ **CircumcircleArc**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[CircumcircleArc](./CircumcircleArc.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "circumcirclearc".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p3**
:   The result will be a composition of an arc of the circumcircle of p1, p2, and p3 and the midpoint of the circumcircle of the three points. The arc is drawn counter-clockwise from p1 over p2 to p3.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a circum circle arc out of three free points
var p1 = board.create('point', [2.0, 2.0]);
var p2 = board.create('point', [1.0, 0.5]);
var p3 = board.create('point', [3.5, 1.0]);

var a = board.create('circumcirclearc', [p1, p2, p3]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[center](./CircumcircleArc.md#center)**  Attributes for center point. |




### {[Point](./Point.md)} **center**

Attributes for center point.
  
*Defined in:*  [options.js](./src/src_options.js.md).
