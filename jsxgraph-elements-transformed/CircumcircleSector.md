

# CircumcircleSector



## 描述

A sector whose arc is a circum circle arc through three points. A circumcircle sector is different from a [Sector](./Sector.md) mostly in the way the parent elements are interpreted. At first, the circum center is determined from the three given points. Then the sector is drawn from p1 through p2 to p3.   
  
*Defined in:*  [sector.js](./src/src_element_sector.js.md).   
Extends [Sector](./Sector.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Sector](./Sector.md)**  
            ↳ **CircumcircleSector**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[CircumcircleSector](./CircumcircleSector.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "circumcirclesector".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p1**
:   A circumcircle sector is defined by the circumcircle which is determined by these three given points. The circumcircle sector is always drawn from p1 through p2 to p3.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create an arc out of three free points
var p1 = board.create('point', [1.5, 5.0]),
    p2 = board.create('point', [1.0, 0.5]),
    p3 = board.create('point', [5.0, 3.0]),

    a = board.create('circumcirclesector', [p1, p2, p3]);
```



## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[center](./CircumcircleSector.md#center)**  Center of the circumcirclesector |




### {[Circumcenter](./Circumcenter.md)} **center**

Center of the circumcirclesector
