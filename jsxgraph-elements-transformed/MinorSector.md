

# MinorSector



## 描述

A minor sector is a sector of a circle having measure at most 180 degrees (pi radians). It is defined by a center, one point that defines the radius, and a third point that defines the angle of the sector.   
  
*Defined in:*  [sector.js](./src/src_element_sector.js.md).   
Extends [Curve](./Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Curve](./Curve.md)**  
            ↳ **MinorSector**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[MinorSector](./MinorSector.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "minorsector".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p3**
:   . Minor sector is a sector of a circle around p1 having measure less than or equal to 180 degrees (pi radians) and starts at p2. The radius is determined by p2, the angle by p3.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create sector out of three free points
var p1 = board.create('point', [2.0, 2.0]);
var p2 = board.create('point', [1.0, 0.5]);
var p3 = board.create('point', [3.5, 1.0]);

var a = board.create('minorsector', [p1, p2, p3]);
```

```javascript
var A = board.create('point', [3, -2]),
    B = board.create('point', [-2, -2]),
    C = board.create('point', [0, 4]);

var angle = board.create('minorsector', [B, A, C], {
        strokeWidth: 0,
        arc: {
        	visible: true,
        	strokeWidth: 3,
          lastArrow: {size: 4},
          firstArrow: {size: 4}
        }
      });
//angle.arc.setAttribute({firstArrow: false});
angle.arc.setAttribute({lastArrow: false});
```
