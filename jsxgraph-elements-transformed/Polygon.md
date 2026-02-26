

# Polygon



## 描述

A polygon is a plane figure made up of line segments (the borders) connected to form a closed polygonal chain. It is determined by




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Polygon](./JXG.Polygon.md)**  
         ↳ **Polygon**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Polygon](./Polygon.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "polygon".  
  

Possible parent array combinations are:

{Array} **vertices**
:   The polygon's vertices. If the first and the last vertex don't match the first one will be added to the array by the creator. Here, two points match if they have the same 'id' attribute. Additionally, a polygon can be created by providing a polygon and a transformation (or an array of transformations). The result is a polygon which is the transformation of the supplied polygon.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [0.0, 2.0]);
var p2 = board.create('point', [2.0, 1.0]);
var p3 = board.create('point', [4.0, 6.0]);
var p4 = board.create('point', [1.0, 4.0]);

var pol = board.create('polygon', [p1, p2, p3, p4]);
```

```javascript
var p = [[0.0, 2.0], [2.0, 1.0], [4.0, 6.0], [1.0, 3.0]];

var pol = board.create('polygon', p, {hasInnerPoints: true});
```

```javascript
var f1 = function() { return [0.0, 2.0]; },
      f2 = function() { return [2.0, 1.0]; },
      f3 = function() { return [4.0, 6.0]; },
      f4 = function() { return [1.0, 4.0]; },
      cc1 = board.create('polygon', [f1, f2, f3, f4]);
      board.update();
```

```javascript
var t = board.create('transform', [2, 1.5], {type: 'scale'});
var a = board.create('point', [-3,-2], {name: 'a'});
var b = board.create('point', [-1,-4], {name: 'b'});
var c = board.create('point', [-2,-0.5], {name: 'c'});
var pol1 = board.create('polygon', [a,b,c], {vertices: {withLabel: false}});
var pol2 = board.create('polygon', [pol1, t], {vertices: {withLabel: true}});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[borders](./Polygon.md#borders)**  Attributes for the polygon border lines. |
|  | **[hasInnerPoints](./Polygon.md#hasInnerPoints)**  If true, moving the mouse over inner points triggers hasPoint. |
|  | **[highlightByStrokeWidth](./Polygon.md#highlightByStrokeWidth)**  By default, the strokewidths of the borders of a polygon are not changed during highlighting (only strokeColor and strokeOpacity are changed to highlightStrokeColor, and highlightStrokeOpacity). |
|  | **[label](./Polygon.md#label)**  Attributes for the polygon label. |
|  | **[vertices](./Polygon.md#vertices)**  Attributes for the polygon vertices. |
|  | **[withLines](./Polygon.md#withLines)**  Is the polygon bordered by lines? |




### {[Line](./Line.md)} **borders**

Attributes for the polygon border lines.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {Boolean} **hasInnerPoints**

If true, moving the mouse over inner points triggers hasPoint.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [JXG.GeometryElement#hasPoint](./JXG.GeometryElement.md#hasPoint)


#### Default Value:

:   false


### {Boolean} **highlightByStrokeWidth**

By default, the strokewidths of the borders of a polygon are not changed during highlighting (only strokeColor and strokeOpacity are changed
to highlightStrokeColor, and highlightStrokeOpacity).
However, strokewidth is changed to highlightStrokewidth if an individual border gets the focus.

With this attribute set to true, also the borders change strokeWidth if the polygon itself gets the focus.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {[Label](./Label.md)} **label**

Attributes for the polygon label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **vertices**

Attributes for the polygon vertices.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {Boolean} **withLines**

Is the polygon bordered by lines?
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true
