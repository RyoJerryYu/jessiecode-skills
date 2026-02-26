

# PolygonalChain



## 描述

A polygonal chain is a connected series of line segments (borders). It is determined by




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Polygon](./JXG.Polygon.md)**  
         ↳ **PolygonalChain**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[PolygonalChain](./PolygonalChain.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "polygonalchain".  
  

Possible parent array combinations are:

{Array} **vertices**
:   The polygon's vertices. Additionally, a polygonal chain can be created by providing a polygonal chain and a transformation (or an array of transformations). The result is a polygonal chain which is the transformation of the supplied polygonal chain.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var attr = {
            snapToGrid: true
        },
        p = [];

	p.push(board.create('point', [-4, 0], attr));
	p.push(board.create('point', [-1, -3], attr));
	p.push(board.create('point', [0, 2], attr));
	p.push(board.create('point', [2, 1], attr));
	p.push(board.create('point', [4, -2], attr));

 var chain = board.create('polygonalchain', p, {borders: {strokeWidth: 3}});
```
