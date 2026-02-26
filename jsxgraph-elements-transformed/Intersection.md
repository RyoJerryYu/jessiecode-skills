

# Intersection



## 描述

A point intersecting two 1-dimensional elements. It is one point of the set \* consisting of the intersection points of the two elements. The following element types can be (mutually) intersected: line, circle, curve, polygon, polygonal chain.   
  
*Defined in:*  [point.js](./src/src_base_point.js.md).   
Extends [JXG.Point](./JXG.Point.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.CoordsElement**  
   ↳ **[JXG.Point](./JXG.Point.md)**  
         ↳ **Intersection**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Intersection](./Intersection.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "intersection".  
  

Possible parent array combinations are:

{[JXG.Line](../symbols/JXG.Line.html)|[JXG.Circle](../symbols/JXG.Circle.html)} **el1** {[JXG.Line](../symbols/JXG.Line.html)|[JXG.Circle](./JXG.Circle.md)} **el2** {Number|Function} **i**
:   The result will be a intersection point on el1 and el2. i determines the intersection point if two points are available:

    * i==0: use the positive square root,
    * i==1: use the negative square root.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create an intersection point of circle and line
var p1 = board.create('point', [4.0, 4.0]);
var c1 = board.create('circle', [p1, 2.0]);

var p2 = board.create('point', [1.0, 1.0]);
var p3 = board.create('point', [5.0, 3.0]);
var l1 = board.create('line', [p2, p3]);

var i = board.create('intersection', [c1, l1, 0]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
| <static> | Intersection.**[alwaysIntersect](./Intersection.md#.alwaysIntersect)**  Used in JXG.Intersection. |




### <static> {Boolean} Intersection.**alwaysIntersect**

Used in JXG.Intersection.
This flag sets the behaviour of intersection points of e.g.
two segments. If true, the intersection is treated as intersection of lines. If false
the intersection point exists if the segments intersect setwise.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
| <private> <static> | Intersection.**[intersectionNumbers](./Intersection.md#.intersectionNumbers)**  Array of length 2 containing the numbers i and j. |




### <private> <static> {Array} Intersection.**intersectionNumbers**

Array of length 2 containing the numbers i and j.
The intersection point is i-th intersection point.
j is unused.
