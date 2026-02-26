

# Transformation



## 描述

Define projective 2D transformations like translation, rotation, reflection.   
  
*Defined in:*  [transformation.js](./src/src_base_transformation.js.md).   
Extends [JXG.Transformation](./JXG.Transformation.md).




## 继承关系

**[JXG.Transformation](./JXG.Transformation.md)**  
      ↳ **Transformation**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Transformation](./Transformation.md#constructor)**  A transformation consists of a 3x3 matrix, i.e. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "transformation".  
  

Possible parent array combinations are:

{number|function|[JXG.GeometryElement](./JXG.GeometryElement.md)} **parameters**
:   The parameters depend on the transformation type, supplied as attribute 'type'. Possible transformation types are

    * 'translate'
    * 'scale'
    * 'reflect'
    * 'rotate'
    * 'shear'
    * 'generic'
    * 'matrix'

    Valid parameters for these types are:

    **type:"translate"**
    :   **x, y** Translation vector (two numbers or functions). The transformation matrix for x = a and y = b has the form:

        ```
         ( 1  0  0)   ( z ) ( a  1  0) * ( x ) ( b  0  1)   ( y )
        ```

    **type:"scale"**
    :   **scale\_x, scale\_y** Scale vector (two numbers or functions). The transformation matrix for scale\_x = a and scale\_y = b has the form:

        ```
         ( 1  0  0)   ( z ) ( 0  a  0) * ( x ) ( 0  0  b)   ( y )
        ```

    **type:"rotate"**
    :   **alpha, [point | x, y]** The parameters are the angle value in Radians (a number or function), and optionally a coordinate pair (two numbers or functions) or a point element defining the rotation center. If the rotation center is not given, the transformation rotates around (0,0). The transformation matrix for angle a and rotating around (0, 0) has the form:

        ```
         ( 1    0        0      )   ( z ) ( 0    cos(a)   -sin(a)) * ( x ) ( 0    sin(a)   cos(a) )   ( y )
        ```

    **type:"shear"**
    :   **shear\_x, shear\_y** Shear vector (two numbers or functions). The transformation matrix for shear\_x = a and shear\_y = b has the form:

        ```
         ( 1  0  0)   ( z ) ( 0  1  a) * ( x ) ( 0  b  1)   ( y )
        ```

    **type:"reflect"**
    :   The parameters can either be:

        * **line** a line element,
        * **p, q** two point elements,
        * **p\_x, p\_y, q\_x, q\_y** four numbers or functions determining a line through points (p\_x, p\_y) and (q\_x, q\_y).

    **type:"generic"**
    :   **a, b, c, d, e, f, g, h, i** Nine matrix entries (numbers or functions) for a generic projective transformation. The matrix has the form

        ```
         ( a  b  c )   ( z ) ( d  e  f ) * ( x ) ( g  h  i )   ( y )
        ```

    **type:"matrix"**
    :   **M** 3x3 transformation matrix containing numbers or functions


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// The point B is determined by taking twice the vector A from the origin

var p0 = board.create('point', [0, 3], {name: 'A'}),
    t = board.create('transform', [function(){ return p0.X(); }, "Y(A)"], {type: 'translate'}),
    p1 = board.create('point', [p0, t], {color: 'blue'});
```

```javascript
// The point B is the result of scaling the point A with factor 2 in horizontal direction
// and with factor 0.5 in vertical direction.

var p1 = board.create('point', [1, 1]),
    t = board.create('transform', [2, 0.5], {type: 'scale'}),
    p2 = board.create('point', [p1, t], {color: 'blue'});
```

```javascript
// The point B is rotated around C which gives point D. The angle is determined
// by the vertical height of point A.

var p0 = board.create('point', [0, 3], {name: 'A'}),
    p1 = board.create('point', [1, 1]),
    p2 = board.create('point', [2, 1], {name:'C', fixed: true}),

    // angle, rotation center:
    t = board.create('transform', ['Y(A)', p2], {type: 'rotate'}),
    p3 = board.create('point', [p1, t], {color: 'blue'});
```

```javascript
// A concatenation of several transformations.
var p1 = board.create('point', [1, 1]),
    t1 = board.create('transform', [-2, -1], {type: 'translate'}),
    t2 = board.create('transform', [Math.PI/4], {type: 'rotate'}),
    t3 = board.create('transform', [2, 1], {type: 'translate'}),
    p2 = board.create('point', [p1, [t1, t2, t3]], {color: 'blue'});
```

```javascript
// Reflection of point A
var p1 = board.create('point', [1, 1]),
    p2 = board.create('point', [1, 3]),
    p3 = board.create('point', [-2, 0]),
    l = board.create('line', [p2, p3]),
    t = board.create('transform', [l], {type: 'reflect'}),  // Possible are l, l.id, l.name
    p4 = board.create('point', [p1, t], {color: 'blue'});
```

```javascript
// Type: 'matrix'
        var y = board.create('slider', [[-3, 1], [-3, 4], [0, 1, 6]]);
        var t1 = board.create('transform', [
            [
                [1, 0, 0],
                [0, 1, 0],
                [() => y.Value(), 0, 1]
            ]
        ], {type: 'matrix'});

        var A = board.create('point', [2, -3]);
        var B = board.create('point', [A, t1]);
```

```javascript
// One time application of a transform to points A, B
var p1 = board.create('point', [1, 1]),
    p2 = board.create('point', [-1, -2]),
    t = board.create('transform', [3, 2], {type: 'shear'});
t.applyOnce([p1, p2]);
```

```javascript
// Construct a square of side length 2 with the
// help of transformations
    var sq = [],
        right = board.create('transform', [2, 0], {type: 'translate'}),
        up = board.create('transform', [0, 2], {type: 'translate'}),
        pol, rot, p0;

    // The first point is free
    sq[0] = board.create('point', [0, 0], {name: 'Drag me'}),

    // Construct the other free points by transformations
    sq[1] = board.create('point', [sq[0], right]),
    sq[2] = board.create('point', [sq[0], [right, up]]),
    sq[3] = board.create('point', [sq[0], up]),

    // Polygon through these four points
    pol = board.create('polygon', sq, {
            fillColor:'blue',
            gradient:'radial',
            gradientsecondcolor:'white',
            gradientSecondOpacity:'0'
    }),

    p0 = board.create('point', [0, 3], {name: 'angle'}),
    // Rotate the square around point sq[0] by dragging A vertically.
    rot = board.create('transform', ['Y(angle)', sq[0]], {type: 'rotate'});

    // Apply the rotation to all but the first point of the square
    rot.bindTo(sq.slice(1));
```

```javascript
// Text transformation
var p0 = board.create('point', [0, 0], {name: 'p_0'});
var p1 = board.create('point', [3, 0], {name: 'p_1'});
var txt = board.create('text',[0.5, 0, 'Hello World'], {display:'html'});

// If p_0 is dragged, translate p_1 and text accordingly
var tOff = board.create('transform', [() => p0.X(), () => p0.Y()], {type:'translate'});
tOff.bindTo(txt);
tOff.bindTo(p1);

// Rotate text around p_0 by dragging point p_1
var tRot = board.create('transform', [
    () => Math.atan2(p1.Y() - p0.Y(), p1.X() - p0.X()), p0], {type:'rotate'});
tRot.bindTo(txt);

// Scale text by dragging point "p_1"
// We do this by
// - moving text by -p_0 (inverse of transformation tOff),
// - scale the text (because scaling is relative to (0,0))
// - move the text back by +p_0
var tOffInv = board.create('transform', [
        () => -p0.X(),
        () => -p0.Y()
], {type:'translate'});
var tScale = board.create('transform', [
        // Some scaling factor
        () => p1.Dist(p0) / 3,
        () => p1.Dist(p0) / 3
], {type:'scale'});
tOffInv.bindTo(txt); tScale.bindTo(txt); tOff.bindTo(txt);
```
