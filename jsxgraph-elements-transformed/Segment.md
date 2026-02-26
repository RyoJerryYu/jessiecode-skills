

# Segment



## 描述

A (line) segment defined by two points. It's strictly spoken just a wrapper for element [Line](./Line.md) with [Line#straightFirst](../symbols/Line.html#straightFirst) and [Line#straightLast](./Line.md#straightLast) properties set to false. If there is a third variable then the segment has a fixed length (which may be a function, too) determined by the absolute value of that number.   
  
*Defined in:*  [line.js](./src/src_base_line.js.md).   
Extends [JXG.Line](./JXG.Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
         ↳ **Segment**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Segment](./Segment.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "segment".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|array} **point1** {[JXG.Point](./JXG.Point.md)|array} **point2**
:   Parent elements can be two elements either of type [JXG.Point](./JXG.Point.md) or array of numbers describing the coordinates of a point. In the latter case the point will be constructed automatically as a fixed invisible point.
  
  

{number|function} **length**
:   The points are adapted - if possible - such that their distance is equal to the absolute value of this number.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a segment providing two points.
  var p1 = board.create('point', [4.5, 2.0]);
  var p2 = board.create('point', [1.0, 1.0]);
  var l1 = board.create('segment', [p1, p2]);
```

```javascript
// Create a segment providing two points.
  var p1 = board.create('point', [4.0, 1.0]);
  var p2 = board.create('point', [1.0, 1.0]);
  // AB
  var l1 = board.create('segment', [p1, p2]);
  var p3 = board.create('point', [4.0, 2.0]);
  var p4 = board.create('point', [1.0, 2.0]);
  // CD
  var l2 = board.create('segment', [p3, p4, 3]); // Fixed length
  var p5 = board.create('point', [4.0, 3.0]);
  var p6 = board.create('point', [1.0, 4.0]);
  // EF
  var l3 = board.create('segment', [p5, p6, function(){ return l1.L();} ]); // Fixed, but dependent length
```
