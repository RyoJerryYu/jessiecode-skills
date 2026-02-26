

# Transformation3D



## 描述

Define projective 3D transformations like translation, rotation, reflection.   
  
*Defined in:*  [transformation.js](./src/src_base_transformation.js.md).   
Extends [JXG.Transformation](./JXG.Transformation.md).




## 继承关系

**[JXG.Transformation](./JXG.Transformation.md)**  
      ↳ **Transformation3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Transformation3D](./Transformation3D.md#constructor)**  A transformation consists of a 4x4 matrix, i.e. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "transformation3d".  
  

Possible parent array combinations are:

{number|function|[JXG.GeometryElement3D](./JXG.GeometryElement3D.md)} **parameters**
:   The parameters depend on the transformation type, supplied as attribute 'type'. Possible transformation types are

    * 'translate'
    * 'scale'
    * 'rotate'
    * 'rotateX'
    * 'rotateY'
    * 'rotateZ'

    Valid parameters for these types are:

    **type:"translate"**
    :   **x, y, z** Translation vector (three numbers or functions). The transformation matrix for x = a, y = b, and z = c has the form:

        ```
         ( 1  0  0  0)   ( w ) ( a  1  0  0) * ( x ) ( b  0  1  0)   ( y ) ( c  0  0  c)   ( z )
        ```

    **type:"scale"**
    :   **scale\_x, scale\_y, scale\_z** Scale vector (three numbers or functions). The transformation matrix for scale\_x = a, scale\_y = b, scale\_z = c has the form:

        ```
         ( 1  0  0  0)   ( w ) ( 0  a  0  0) * ( x ) ( 0  0  b  0)   ( y ) ( 0  0  0  c)   ( z )
        ```

    **type:"rotate"**
    :   **a, n, [p=[0,0,0]]** angle (in radians), normal, [point]. Rotate with angle a around the normal vector n through the point p.

    **type:"rotateX"**
    :   **a, [p=[0,0,0]]** angle (in radians), [point]. Rotate with angle a around the normal vector (1, 0, 0) through the point p.

    **type:"rotateY"**
    :   **a, [p=[0,0,0]]** angle (in radians), [point]. Rotate with angle a around the normal vector (0, 1, 0) through the point p.

    **type:"rotateZ"**
    :   **a, [p=[0,0,0]]** angle (in radians), [point]. Rotate with angle a around the normal vector (0, 0, 1) through the point p.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var bound = [-5, 5];
   var view = board.create('view3d',
       [[-6, -3], [8, 8],
       [bound, bound, bound]];

   var slid = board.create('slider', [[-4, 4], [0, 4], [0, 0, 5]])

   var p1 = view.create('point3d', [1, 2, 2], { name: 'drag me', size: 5 });

   // translate from p1 by some fixed or function amount
   var t1 = view.create('transform3d', [2, 3, 2], { type: 'translate' });
   var t2 = view.create('transform3d', [()=>slid.Value()+3,0,0], { type: 'translate' })

   view.create('point3d', [p1, t1], { name: 'translate fixed', size: 5 });
   view.create('point3d', [p1, t2], { name: 'translate by func', size: 5 });
```
