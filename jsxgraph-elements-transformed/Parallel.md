

# Parallel



## 描述

A parallel is a line through a given point, parallel to a given line.

If original line is given as a JSXGraph line object, the resulting parallel line will be defined by the given point and an infinitely far away point (an ideal point). That means, the line can not be shortened to a segment.

If the original line is given as two points, the resulting parallel line can be shortened to a a segment.   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [Line](./Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
      ↳ **[Line](./Line.md)**  
            ↳ **Parallel**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Parallel](./Parallel.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "parallel".  
  

Possible parent array combinations are:

{[JXG.Line](../symbols/JXG.Line.html)} **l** {[JXG.Point](./JXG.Point.md)} **p**
:   The constructed line contains p and has the same slope as l. Alternative parameters are p1, p2, p: The constructed line contains p and has the same slope as the line through p1 and p2.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a parallel
var p1 = board.create('point', [0.0, 2.0]);
var p2 = board.create('point', [2.0, 1.0]);
var l1 = board.create('line', [p1, p2]);

var p3 = board.create('point', [3.0, 3.0]);
var pl1 = board.create('parallel', [l1, p3]);
```

```javascript
var p1, p2, p3, l1, pl1;

p1 = board.create('point', [0.0, 2.0]);
p2 = board.create('point', [2.0, 1.0]);
l1 = board.create('line', [p1, p2]);

p3 = board.create('point', [1.0, 3.0]);
pl1 = board.create('parallel', [p1, p2, p3], {straightFirst: false, straightLast: false});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[point](./Parallel.md#point)**  Attributes of helper point of normal. |




### {[Point](./Point.md)} **point**

Attributes of helper point of normal.
  
*Defined in:*  [options.js](./src/src_options.js.md).
