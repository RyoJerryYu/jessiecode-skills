

# Tangent



## 描述

The tangent line at a point on a line, circle, conic, turtle, or curve. A tangent line is always constructed by a point on a line, circle, or curve and describes the tangent in the point on that line, circle, or curve.

If the point is not on the object (line, circle, conic, curve, turtle) the output depends on the type of the object. For conics and circles, the polar line will be constructed. For function graphs, the tangent of the vertical projection of the point to the function graph is constructed. For all other objects, the tangent in the orthogonal projection of the point to the object will be constructed.   
  
*Defined in:*  [line.js](./src/src_base_line.js.md).   
Extends [JXG.Line](./JXG.Line.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Line](./JXG.Line.md)**  
         ↳ **Tangent**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Tangent](./Tangent.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "tangent".  
  

Possible parent array combinations are:

{[Glider](./Glider.md)} **g**
:   A glider on a line, circle, or curve.
  
  

{[JXG.GeometryElement](./JXG.GeometryElement.md)} **c**
:   Optional element for which the tangent is constructed


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a tangent providing a glider on a function graph
  var c1 = board.create('curve', [function(t){return t},function(t){return t*t*t;}]);
  var g1 = board.create('glider', [0.6, 1.2, c1]);
  var t1 = board.create('tangent', [g1]);
```
