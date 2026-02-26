

# Arrowparallel



## 描述

A segment with an arrow head attached thath is parallel to a given segment. The segment is given by its defining two points, the arrow starts at a given point.

*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [Parallel](./Parallel.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
      ↳ **[Line](./Line.md)**  
         ↳ **[Parallel](./Parallel.md)**  
               ↳ **Arrowparallel**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Arrowparallel](./Arrowparallel.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "arrowparallel".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p3**
:   The constructed arrow contains p3 and has the same slope as the line through p1 and p2.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a parallel
var p1 = board.create('point', [0.0, 2.0]);
var p2 = board.create('point', [2.0, 1.0]);
var l1 = board.create('segment', [p1, p2]);

var p3 = board.create('point', [3.0, 3.0]);
var pl1 = board.create('arrowparallel', [p1, p2, p3]);
```
