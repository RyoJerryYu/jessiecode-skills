

# Circumcircle



## 描述

A circumcircle is the unique circle through three points.   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.Circle](./JXG.Circle.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Circle](./JXG.Circle.md)**  
         ↳ **Circumcircle**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Circumcircle](./Circumcircle.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "circumcircle".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p3**
:   The constructed element is the circle determined by p1, p2, and p3.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [0.0, 2.0]);
var p2 = board.create('point', [2.0, 1.0]);
var p3 = board.create('point', [3.0, 3.0]);

var cc1 = board.create('circumcircle', [p1, p2, p3]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[center](./Circumcircle.md#center)**  Attributes for center point. |




### {[Point](./Point.md)} **center**

Attributes for center point.
  
*Defined in:*  [options.js](./src/src_options.js.md).
