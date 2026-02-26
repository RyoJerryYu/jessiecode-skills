

# RegularPolygon



## 描述

A regular polygon is a polygon that is direct equiangular (all angles are equal in measure) and equilateral (all sides have the same length). It needs two points which define the base line and the number of vertices.   
  
*Defined in:*  [polygon.js](./src/src_base_polygon.js.md).   
Extends [Polygon](./Polygon.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Polygon](./JXG.Polygon.md)**  
      ↳ **[Polygon](./Polygon.md)**  
            ↳ **RegularPolygon**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[RegularPolygon](./RegularPolygon.md#constructor)**  Constructs a regular polygon. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "regularpolygon".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](./JXG.Point.md)} **p2** {Number} **n**
:   The constructed regular polygon has n vertices and the base line defined by p1 and p2.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [0.0, 2.0]);
var p2 = board.create('point', [2.0, 1.0]);

var pol = board.create('regularpolygon', [p1, p2, 5]);
```

```javascript
var p1 = board.create('point', [0.0, 2.0]);
var p2 = board.create('point', [4.0,4.0]);
var p3 = board.create('point', [2.0,0.0]);

var pol = board.create('regularpolygon', [p1, p2, p3]);
```

```javascript
// Line of reflection
        var li = board.create('line', [1,1,1], {strokeColor: '#aaaaaa'});
        var reflect = board.create('transform', [li], {type: 'reflect'});
        var pol1 = board.create('polygon', [[-3,-2], [-1,-4], [-2,-0.5]]);
        var pol2 = board.create('polygon', [pol1, reflect]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[borders](./RegularPolygon.md#borders)**  Attributes for the polygon border lines. |
|  | **[hasInnerPoints](./RegularPolygon.md#hasInnerPoints)**  If true, moving the mouse over inner points triggers hasPoint. |
|  | **[label](./RegularPolygon.md#label)**  Attributes for the polygon label. |
|  | **[vertices](./RegularPolygon.md#vertices)**  Attributes for the polygon vertices. |
|  | **[withLines](./RegularPolygon.md#withLines)**  Is the polygon bordered by lines? |




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
