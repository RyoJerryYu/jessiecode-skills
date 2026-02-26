

# Hatch



## 描述

Hatches are collections of short line segments used to mark congruent lines or curves.   
  
*Defined in:*  [ticks.js](./src/src_base_ticks.js.md).   
Extends [JXG.Ticks](./JXG.Ticks.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Ticks](./JXG.Ticks.md)**  
         ↳ **Hatch**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Hatch](./Hatch.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "hatch".  
  

Possible parent array combinations are:

{[JXG.Line](./JXG.Line.md)|JXG.curve} **line**
:   The line or curve the hatch marks are going to be attached to.
  
  

{Number} **numberofhashes**
:   Number of dashes. The distance of the hashes can be controlled with the attribute ticksDistance.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create an axis providing two coords pairs.
  var p1 = board.create('point', [0, 3]);
  var p2 = board.create('point', [1, 3]);
  var l1 = board.create('line', [p1, p2]);
  var t = board.create('hatch', [l1, 3]);
```

```javascript
// Alter the position of the hatch

var p = board.create('point', [-5, 0]);
var q = board.create('point', [5, 0]);
var li = board.create('line', [p, q]);
var h = board.create('hatch', [li, 2], {anchor: 0.2, ticksDistance:0.4});
```

```javascript
// Alternative hatch faces

var li = board.create('line', [[-6,0], [6,3]]);
var h1 = board.create('hatch', [li, 2], {tickEndings: [1,1], face:'|'});
var h2 = board.create('hatch', [li, 2], {tickEndings: [1,1], face:'>', anchor: 0.3});
var h3 = board.create('hatch', [li, 2], {tickEndings: [1,1], face:'<', anchor: 0.7});
```



## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[ticksDistance](./Hatch.md#ticksDistance)**  The default distance (in user coordinates, not pixels) between two hatch symbols. |




### {Number} **ticksDistance**

The default distance (in user coordinates, not pixels) between two hatch symbols.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.2
