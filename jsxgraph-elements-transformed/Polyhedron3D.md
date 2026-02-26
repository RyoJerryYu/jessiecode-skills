

# Polyhedron3D



## 描述

A polyhedron in a 3D view consists of faces.   
  
*Defined in:*  [polyhedron3d.js](./src/src_3d_polyhedron3d.js.md).   
Extends [JXG.GeometryElement3D](./JXG.GeometryElement3D.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.GeometryElement3D](./JXG.GeometryElement3D.md)**  
         ↳ **Polyhedron3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Polyhedron3D](./Polyhedron3D.md#constructor)**  Create a polyhedron in a 3D view consisting of faces. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "polyhedron3d".  
  

Possible parent array combinations are:

{} **TODO**


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var box = [-4, 4];
var view = board.create(
    'view3d',
    [[-5, -3], [8, 8],
    [box, box, box]],
    {
        projection: 'parallel',
        trackball: { enabled: false },
        depthOrder: {
            enabled: true
        },
        xPlaneRear: { visible: false },
        yPlaneRear: { visible: false },
        zPlaneRear: { fillOpacity: 0.2 }
    }
);
var cube = view.create('polyhedron3d', [
[
    [-3, -3, -3],
    [3, -3, -3],
    [3, 3, -3],
    [-3, 3, -3],

    [-3, -3, 3],
    [3, -3, 3],
    [3, 3, 3],
    [-3, 3, 3]
],
[
    [0, 1, 2, 3],
    [0, 1, 5, 4],
    [[1, 2, 6, 5], { fillColor: 'black', fillOpacity: 0.5, strokeWidth: 5 }],
    [2, 3, 7, 6],
    [3, 0, 4, 7],
    [4, 5, 6, 7]
]
], {
fillColorArray: ['blue', 'red', 'yellow']
});
```

```javascript
var box = [-4, 4];
var view = board.create(
    'view3d',
    [[-5, -3], [8, 8],
    [box, box, box]],
    {
        projection: 'parallel',
        trackball: { enabled: false },
        depthOrder: {
            enabled: true
        },
        xPlaneRear: { visible: false },
        yPlaneRear: { visible: false },
        zPlaneRear: { fillOpacity: 0.2 }
    }
);
var aa = view.create('point3d', [-3, -3, -3], { name: 'A', layer: 12});
var bb = view.create('point3d', [() => aa.X(), () => aa.Y(), 3], { name: 'B', fixed: true, layer: 12});
var cube = view.create('polyhedron3d', [
    {
        a: 'A',
        b: [3, -3, -3],
        c: [3, 3, -3],
        d: [-3, 3, -3],

        e: bb,
        f: [3, -3, 3],
        g: [3, 3, 3],
        h: [-3, 3, 3]
    },
    [
        ['a', 'b', 'c', 'd'],
        ['a', 'b', 'f', 'e'],
        ['b', 'c', 'g', 'f'],
        ['c', 'd', 'h', 'g'],
        ['d', 'a', 'e', 'h'],
        ['e', 'f', 'g', 'h'],

        ['a', 'g'], // Edge
        ['f']       // Vertex
    ]
], {
    fillColorArray: ['blue', 'red', 'yellow'],
    fillOpacity: 0.4,
    layer: 12
});
cube.faces[6].setAttribute({ strokeWidth: 5 });
cube.faces[7].setAttribute({ strokeWidth: 10 });
```

```javascript
var box = [-4, 4];
var view = board.create(
    'view3d',
    [[-5, -3], [8, 8],
    [box, box, box]],
    {
        projection: 'parallel',
        trackball: { enabled: false },
        depthOrder: {
            enabled: true
        },
        xPlaneRear: { visible: false },
        yPlaneRear: { visible: false },
        zPlaneRear: { fillOpacity: 0.2 }
    }
);
var s = board.create('slider', [[-4, -6], [4, -6], [0, 2, 4]], { name: 's' });
var cube = view.create('polyhedron3d', [
    [
        () => { let f = s.Value(); return [-f, -f, -f]; },
        () => { let f = s.Value(); return [f, -f, -f]; },
        () => { let f = s.Value(); return [f, f, -f]; },
        () => { let f = s.Value(); return [-f, f, -f]; },

        () => { let f = s.Value(); return [-f, -f, f]; },
        () => { let f = s.Value(); return [f, -f, f]; },
        () => { let f = s.Value(); return [f, f, f]; },
        // () => { let f = s.Value(); return [-f, f, f]; }
        [ () => -s.Value(),  () => s.Value(), () => s.Value() ]
    ],
    [
        [0, 1, 2, 3],
        [0, 1, 5, 4],
        [1, 2, 6, 5],
        [2, 3, 7, 6],
        [3, 0, 4, 7],
        [4, 5, 6, 7],
    ]
], {
    strokeWidth: 3,
    fillOpacity: 0.6,
    fillColorArray: ['blue', 'red', 'yellow'],
    shader: {
        enabled:false
    }
});
```

```javascript
var box = [-4, 4];
var view = board.create(
    'view3d',
    [[-5, -3], [8, 8],
    [box, box, box]],
    {
        projection: 'parallel',
        trackball: { enabled: false },
        depthOrder: {
            enabled: true
        },
        xPlaneRear: { visible: false },
        yPlaneRear: { visible: false },
        zPlaneRear: { fillOpacity: 0.2 }
    }
);
let rho = 1.6180339887;
let vertexList = [
    [0, -1, -rho], [0, +1, -rho], [0, -1, rho], [0, +1, rho],
    [1, rho, 0], [-1, rho, 0], [1, -rho, 0], [-1, -rho, 0],
    [-rho, 0, 1], [-rho, 0, -1], [rho, 0, 1], [rho, 0, -1]
];
let faceArray = [
    [4, 1, 11],
    [11, 1, 0],
    [6, 11, 0],
    [0, 1, 9],
    [11, 10, 4],
    [9, 1, 5],
    [8, 9, 5],
    [5, 3, 8],
    [6, 10, 11],
    [2, 3, 10],
    [2, 10, 6],
    [8, 3, 2],
    [3, 4, 10],
    [7, 8, 2],
    [9, 8, 7],
    [0, 9, 7],
    [4, 3, 5],
    [5, 1, 4],
    [0, 7, 6],
    [7, 2, 6]
];
var ico = view.create('polyhedron3d', [vertexList, faceArray], {
fillColorArray: [],
fillOpacity: 1,
strokeWidth: 0.1,
layer: 12,
shader: {
    enabled: true,
    type: 'angle',
    hue: 60,
    saturation: 90,
    minlightness: 60,
    maxLightness: 80
}
});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[fillColorArray](./Polyhedron3D.md#fillColorArray)**  Color array to define fill colors of faces cyclically. |




### {Array} **fillColorArray**

Color array to define fill colors of faces cyclically.
Alternatively, the fill color can be defined for each face individually.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ['white', 'black']


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[def](./Polyhedron3D.md#def)**  Contains the defining data of the polyhedron: Definitions of vertices and a list of vertices for each face. |
|  | **[faces](./Polyhedron3D.md#faces)**  List of Face3D objects. |
|  | **[numberFaces](./Polyhedron3D.md#numberFaces)**  Number of faces |




### {Object} **def**

Contains the defining data of the polyhedron:
Definitions of vertices and a list of vertices for each face. This is pretty much the input given
in the construction of the polyhedron plus internal data.


### {Array} **faces**

List of Face3D objects.


### {Number} **numberFaces**

Number of faces
