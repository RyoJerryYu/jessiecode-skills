

# MirrorPoint



## 描述

A MirrorPoint is a special case of a [MirrorElement](./MirrorElement.md).   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.Point](./JXG.Point.md).




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Point](./JXG.Point.md)**  
         ↳ **MirrorPoint**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[MirrorPoint](./MirrorPoint.md#constructor)**  A mirror point is determined by the reflection of a given point against another given point. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "mirrorpoint".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](./JXG.Point.md)} **p2**
:   The constructed point is the reflection of p2 against p1. This method is superseeded by the more general JXG.createMirrorElement.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [3.0, 3.0]);
var p2 = board.create('point', [6.0, 1.0]);

var mp1 = board.create('mirrorpoint', [p1, p2]);
```
