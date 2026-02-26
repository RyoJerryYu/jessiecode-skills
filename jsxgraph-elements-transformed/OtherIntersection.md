

# OtherIntersection



## 描述

Given a set of intersection points, this is another ("other") intersection point,   
  
*Defined in:*  [point.js](./src/src_base_point.js.md).   
Extends [JXG.Point](./JXG.Point.md).




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Point](./JXG.Point.md)**  
         ↳ **OtherIntersection**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[OtherIntersection](./OtherIntersection.md#constructor)**  If two elements of type curve, circle or line intersect in more than one point, with this element it is possible to construct the "other" intersection. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "otherintersection".  
  

Possible parent array combinations are:

{[JXG.Line](../symbols/JXG.Line.html)|[JXG.Circle](../symbols/JXG.Circle.html)} **el1** {[JXG.Line](../symbols/JXG.Line.html)|[JXG.Circle](../symbols/JXG.Circle.html)} **el2** {[JXG.Point](./JXG.Point.md)|Array} **p**
:   Two elements which are intersected and a point or an array of points which have to be different from the new intersection point.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create an intersection point of circle and line
var p1 = board.create('point', [2.0, 2.0]);
var c1 = board.create('circle', [p1, 2.0]);

var p2 = board.create('point', [2.0, 2.0]);
var p3 = board.create('point', [2.0, 2.0]);
var l1 = board.create('line', [p2, p3]);

var p1 = board.create('intersection', [c1, l1, 0]);
var p2 = board.create('otherintersection', [c1, l1, p1]);
```

```javascript
// circle / circle
 var c1 = board.create('circle', [[0, 0], 3]);
 var c2 = board.create('circle', [[2, 2], 3]);

 var p1 = board.create('intersection', [c1, c2, 0]);
 var p2 = board.create('otherintersection', [c1, c2, p1]);
```

```javascript
// curve / line
 var curve = board.create('implicitcurve', ['-(y**2) + x**3 - 2 * x + 1'], { strokeWidth: 2 });
 var A = board.create('glider', [-1.5, 1, curve]);
 var B = board.create('glider', [0.5, 0.5, curve]);
 var line = board.create('line', [A, B], { color: 'black', strokeWidth: 1 });
 var C = board.create('otherintersection', [curve, line, [A, B]], {precision: 0.01});
 var D = board.create('point', [() => C.X(), () => -C.Y()], { name: '-C = A + B' });
```

```javascript
// curve / curve
 var c1 = board.create('functiongraph', ['x**2 - 3'], { strokeWidth: 2 });
 var A = board.create('point', [0, 2]);
 var c2 = board.create('functiongraph', [(x) => -(x**2) + 2 * A.X() * x + A.Y() - A.X()**2], { strokeWidth: 2 });
 var p1 = board.create('intersection', [c1, c2]);
 var p2 = board.create('otherintersection', [c1, c2, [p1]]);
```
