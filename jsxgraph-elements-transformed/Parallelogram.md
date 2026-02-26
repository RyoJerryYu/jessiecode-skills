

# Parallelogram



## 描述

A quadrilateral polygon with parallel opposite sides.   
  
*Defined in:*  [polygon.js](./src/src_base_polygon.js.md).   
Extends [Polygon](./Polygon.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Polygon](./JXG.Polygon.md)**  
      ↳ **[Polygon](./Polygon.md)**  
            ↳ **Parallelogram**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Parallelogram](./Parallelogram.md#constructor)**  Constructs a parallelogram. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "parallelogram".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|Array} **p1** {[JXG.Point](../symbols/JXG.Point.html)|Array} **p2** {[JXG.Point](./JXG.Point.md)|Array} **p3**
:   The parallelogram is a polygon through the points [p1, p2, pp, p3], where pp is a parallelpoint, available as sub-object parallelogram.parallelPoint.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [-3, -4]);
var p2 = board.create('point', [3, -1]);
var p3 = board.create('point', [-2, 0]);
var par = board.create('parallelogram', [p1, p2, p3], {
    hasInnerPoints: true,
    parallelpoint: {
        size: 6,
        face: '<<>>'
    }
});
```



## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[parallelPoint](./Parallelogram.md#parallelPoint)**  Parallel point which makes the quadrilateral a parallelogram. |




### **parallelPoint**

Parallel point which makes the quadrilateral a parallelogram. Can also be accessed with
parallelogram.vertices[2].
