

# Bisector



## 描述

A bisector is a line which divides an angle into two equal angles. It is given by three points A, B, and C and divides the angle ABC into two equal sized parts.   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.Line](./JXG.Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
         ↳ **Bisector**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Bisector](./Bisector.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "bisector".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p3**
:   The angle described by p1, p2 and p3 will be divided into two equal angles.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [6.0, 4.0]);
var p2 = board.create('point', [3.0, 2.0]);
var p3 = board.create('point', [1.0, 7.0]);

var bi1 = board.create('bisector', [p1, p2, p3]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[point](./Bisector.md#point)**  Attributes for the helper point of the bisector. |




### {[Point](./Point.md)} **point**

Attributes for the helper point of the bisector.
  
*Defined in:*  [options.js](./src/src_options.js.md).
