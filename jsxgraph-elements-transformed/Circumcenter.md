

# Circumcenter



## 描述

Constructs the center of a [Circumcircle](./Circumcircle.md) without creating the circle. Like the circumcircle the circumcenter is constructed by providing three points.   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.Point](./JXG.Point.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.CoordsElement**  
   ↳ **[JXG.Point](./JXG.Point.md)**  
         ↳ **Circumcenter**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Circumcenter](./Circumcenter.md#constructor)**  A circumcenter is given by three points which are all lying on the circle with the constructed circumcenter as the midpoint. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "circumcenter".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p3**
:   The constructed point is the midpoint of the circle determined by p1, p2, and p3.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [0.0, 2.0]);
var p2 = board.create('point', [2.0, 1.0]);
var p3 = board.create('point', [3.0, 3.0]);

var cc1 = board.create('circumcenter', [p1, p2, p3]);
```
