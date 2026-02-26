

# NonReflexAngle



## 描述

A non-reflex angle is the instance of an angle that is at most 180°. It is defined by a center, one point that defines the radius, and a third point that defines the angle of the sector.   
  
*Defined in:*  [sector.js](./src/src_element_sector.js.md).   
Extends [Angle](./Angle.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Sector](./Sector.md)**  
         ↳ **[Angle](./Angle.md)**  
               ↳ **NonReflexAngle**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[NonReflexAngle](./NonReflexAngle.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "nonreflexangle".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p3**
:   . Minor sector is a sector of a circle around p1 having measure less than or equal to 180 degrees (pi radians) and starts at p2. The radius is determined by p2, the angle by p3.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a non-reflex angle out of three free points
var p1 = board.create('point', [5.0, 3.0]),
    p2 = board.create('point', [1.0, 0.5]),
    p3 = board.create('point', [1.5, 5.0]),

    a = board.create('nonreflexangle', [p1, p2, p3], {radius: 2}),
    t = board.create('text', [4, 4, function() { return JXG.toFixed(a.Value(), 2); }]);
```
