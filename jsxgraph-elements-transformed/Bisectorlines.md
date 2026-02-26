

# Bisectorlines



## 描述

Bisector lines are similar to [Bisector](./Bisector.md) but take two lines as parent elements. The resulting element is a composition of two lines.   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.Composition](./JXG.Composition.md).




## 继承关系

**[JXG.Composition](./JXG.Composition.md)**  
      ↳ **Bisectorlines**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Bisectorlines](./Bisectorlines.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "bisectorlines".  
  

Possible parent array combinations are:

{[JXG.Line](../symbols/JXG.Line.html)} **l1** {[JXG.Line](./JXG.Line.md)} **l2**
:   The four angles described by the lines l1 and l2 will each be divided into two equal angles.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [6.0, 4.0]);
var p2 = board.create('point', [3.0, 2.0]);
var p3 = board.create('point', [1.0, 7.0]);
var p4 = board.create('point', [3.0, 0.0]);
var l1 = board.create('line', [p1, p2]);
var l2 = board.create('line', [p3, p4]);

var bi1 = board.create('bisectorlines', [l1, l2]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[line1](./Bisectorlines.md#line1)**  Attributes for first line. |
|  | **[line2](./Bisectorlines.md#line2)**  Attributes for second line. |




### {[Line](./Line.md)} **line1**

Attributes for first line.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Line](./Line.md)} **line2**

Attributes for second line.
  
*Defined in:*  [options.js](./src/src_options.js.md).
