

# RadicalAxis



## 描述

The radical axis is the line connecting the two interstion points of two circles with distinct centers. The angular bisector of the polar lines of the circle centers with respect to the other circle is always the radical axis. The radical axis passes through the intersection points when the circles intersect. When a circle about the midpoint of circle centers, passing through the circle centers, intersects the circles, the polar lines pass through those intersection points.   
  
*Defined in:*  [line.js](./src/src_base_line.js.md).   
Extends [JXG.Line](./JXG.Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
         ↳ **RadicalAxis**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[RadicalAxis](./RadicalAxis.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "radicalaxis".  
  

Possible parent array combinations are:

{[JXG.Circle](./JXG.Circle.md)} **circle**
:   one of the two respective circles.
  
  

{[JXG.Circle](./JXG.Circle.md)} **circle**
:   the other of the two respective circles.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create the radical axis line with respect to two circles
  var board = JXG.JSXGraph.initBoard('7b7233a0-f363-47dd-9df5-5018d0d17a98', {boundingbox: [-1, 9, 9, -1], axis: true, showcopyright: false, shownavigation: false});
  var p1 = board.create('point', [2, 3]);
  var p2 = board.create('point', [1, 4]);
  var c1 = board.create('circle', [p1, p2]);
  var p3 = board.create('point', [6, 5]);
  var p4 = board.create('point', [8, 6]);
  var c2 = board.create('circle', [p3, p4]);
  var r1 = board.create('radicalaxis', [c1, c2]);
```
