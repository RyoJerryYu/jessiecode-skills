

# Semicircle



## 描述

A semicircle is a special arc defined by two points. The arc hits both points.   
  
*Defined in:*  [arc.js](./src/src_element_arc.js.md).   
Extends [Arc](./Arc.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Curve](./Curve.md)**  
         ↳ **[Arc](./Arc.md)**  
               ↳ **Semicircle**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Semicircle](./Semicircle.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "semicircle".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](./JXG.Point.md)} **p2**
:   The result will be a composition of an arc drawn clockwise from p1 and p2 and the midpoint of p1 and p2.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create an arc out of three free points
var p1 = board.create('point', [4.5, 2.0]);
var p2 = board.create('point', [1.0, 0.5]);

var a = board.create('semicircle', [p1, p2]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[center](./Semicircle.md#center)**  Attributes for center point of the semicircle. |




### {[Point](./Point.md)} **center**

Attributes for center point of the semicircle.
  
*Defined in:*  [options.js](./src/src_options.js.md).


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[midpoint](./Semicircle.md#midpoint)**  The midpoint of the two defining points. |




### {[Midpoint](./Midpoint.md)} **midpoint**

The midpoint of the two defining points.
