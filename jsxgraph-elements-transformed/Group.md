

# Group



## 描述

A container element to control the movement of given set of point, image or text elements simultaneously. The elements of the group and dependent elements can be translated, rotated and scaled by dragging one of the group elements.   
  
*Defined in:*  [group.js](./src/src_base_group.js.md).   
Extends [JXG.Group](./JXG.Group.md).




## 继承关系

**[JXG.Group](./JXG.Group.md)**  
      ↳ **Group**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Group](./Group.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "group".  
  

Possible parent array combinations are:

{[JXG.Board](./JXG.Board.md)} **board**
:   The board the points are on.
  
  

{Array} **parents**
:   Array of points to group.
  
  

{Object} **attributes**
:   Visual properties (unused).


### 示例

```javascript
// Create some free points. e.g. A, B, C, D
 // Create a group

 var p, col, g;
 col = 'blue';
 p = [];
 p.push(board.create('point',[-2, -1 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[2, -1 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[2, 1 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[-2, 1], {size: 5, strokeColor:col, fillColor:col}));
 g = board.create('group', p);
```

```javascript
// Create some free points. e.g. A, B, C, D
 // Create a group
 // If the points define a polygon and the polygon has the attribute hasInnerPoints:true,
 // the polygon can be dragged around.

 var p, col, pol, g;
 col = 'blue';
 p = [];
 p.push(board.create('point',[-2, -1 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[2, -1 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[2, 1 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[-2, 1], {size: 5, strokeColor:col, fillColor:col}));

 pol = board.create('polygon', p, {hasInnerPoints: true});
 g = board.create('group', p);
```

```javascript
// Allow rotations:
 // Define a center of rotation and declare points of the group as "rotation points".

 var p, col, pol, g;
 col = 'blue';
 p = [];
 p.push(board.create('point',[-2, -1 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[2, -1 ], {size: 5, strokeColor:'red', fillColor:'red'}));
 p.push(board.create('point',[2, 1 ], {size: 5, strokeColor:'red', fillColor:'red'}));
 p.push(board.create('point',[-2, 1], {size: 5, strokeColor:col, fillColor:col}));

 pol = board.create('polygon', p, {hasInnerPoints: true});
 g = board.create('group', p);
 g.setRotationCenter(p[0]);
 g.setRotationPoints([p[1], p[2]]);
```

```javascript
// Allow rotations:
 // As rotation center, arbitrary points, coordinate arrays,
 // or functions returning coordinate arrays can be given.
 // Another possibility is to use the predefined string 'centroid'.

 // The methods to define the rotation points can be chained.

 var p, col, pol, g;
 col = 'blue';
 p = [];
 p.push(board.create('point',[-2, -1 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[2, -1 ], {size: 5, strokeColor:'red', fillColor:'red'}));
 p.push(board.create('point',[2, 1 ], {size: 5, strokeColor:'red', fillColor:'red'}));
 p.push(board.create('point',[-2, 1], {size: 5, strokeColor:col, fillColor:col}));

 pol = board.create('polygon', p, {hasInnerPoints: true});
 g = board.create('group', p).setRotationCenter('centroid').setRotationPoints([p[1], p[2]]);
```

```javascript
// Allow scaling:
 // As for rotation one can declare points of the group to trigger a scaling operation.
 // For this, one has to define a scaleCenter, in analogy to rotations.

 // Here, the yellow  point enables scaling, the red point a rotation.

 var p, col, pol, g;
 col = 'blue';
 p = [];
 p.push(board.create('point',[-2, -1 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[2, -1 ], {size: 5, strokeColor:'yellow', fillColor:'yellow'}));
 p.push(board.create('point',[2, 1 ], {size: 5, strokeColor:'red', fillColor:'red'}));
 p.push(board.create('point',[-2, 1], {size: 5, strokeColor:col, fillColor:col}));

 pol = board.create('polygon', p, {hasInnerPoints: true});
 g = board.create('group', p).setRotationCenter('centroid').setRotationPoints([p[2]]);
 g.setScaleCenter(p[0]).setScalePoints(p[1]);
```

```javascript
// Allow Translations:
 // By default, every point of a group triggers a translation.
 // There may be situations, when this is not wanted.

 // In this example, E triggers nothing, but itself is rotation center
 // and is translated, if other points are moved around.

 var p, q, col, pol, g;
 col = 'blue';
 p = [];
 p.push(board.create('point',[-2, -1 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[2, -1 ], {size: 5, strokeColor:'yellow', fillColor:'yellow'}));
 p.push(board.create('point',[2, 1 ], {size: 5, strokeColor:'red', fillColor:'red'}));
 p.push(board.create('point',[-2, 1], {size: 5, strokeColor:col, fillColor:col}));
 q = board.create('point',[0, 0], {size: 5, strokeColor:col, fillColor:col});

 pol = board.create('polygon', p, {hasInnerPoints: true});
 g = board.create('group', p.concat(q)).setRotationCenter('centroid').setRotationPoints([p[2]]);
 g.setScaleCenter(p[0]).setScalePoints(p[1]);
 g.removeTranslationPoint(q);
```

```javascript
// Add an image and use the group tools to manipulate it
      let urlImg = "https://jsxgraph.org/distrib/images/uccellino.jpg";
      let lowleft = [-2, -1]

      let col = 'blue';
      let p = [];
      p.push(board.create('point', lowleft, { size: 5, strokeColor: col, fillColor: col }));
      p.push(board.create('point', [2, -1], { size: 5, strokeColor: 'yellow', fillColor: 'yellow', name: 'scale' }));
      p.push(board.create('point', [2, 1], { size: 5, strokeColor: 'red', fillColor: 'red', name: 'rotate' }));
      p.push(board.create('point', [-2, 1], { size: 5, strokeColor: col, fillColor: col, name: 'translate' }));

      let im = board.create('image', [urlImg, lowleft, [2, 2]]);
      let pol = board.create('polygon', p, { hasInnerPoints: true });

      let g = board.create('group', p.concat(im))
      // g.addPoint(im)   // image, but adds as a point

      g.setRotationCenter(lowleft)
      g.setRotationPoints([p[2]]);

      g.setScaleCenter(p[0]).setScalePoints(p[1]);
```
