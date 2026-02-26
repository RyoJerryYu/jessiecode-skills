

# Reflection



## 描述

Reflect a point, line, circle, curve, polygon across a given line.   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.GeometryElement](./JXG.GeometryElement.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
      ↳ **Reflection**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Reflection](./Reflection.md#constructor)**  A reflected element (point, polygon, line or curve) is given by a given object of the same type and a line of reflection. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "reflection".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|[JXG.Line](../symbols/JXG.Line.html)|[JXG.Curve](../symbols/JXG.Curve.html)|[JXG.Polygon](../symbols/JXG.Polygon.html)} **p** {[JXG.Line](./JXG.Line.md)} **l**
:   The reflection element is the reflection of p across the line l.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [0.0, 4.0]);
var p2 = board.create('point', [6.0, 1.0]);
var l1 = board.create('line', [p1, p2]);
var p3 = board.create('point', [3.0, 3.0]);

var rp1 = board.create('reflection', [p3, l1]);
```

```javascript
// Reflection of more elements
        // reflection line
        var li = board.create('line', [1,1,1], {strokeColor: '#aaaaaa'});

        var p1 = board.create('point', [-3,-1], {name: "A"});
        var q1 = board.create('reflection', [p1, li], {name: "A'"});

        var l1 = board.create('line', [1,-5,1]);
        var l2 = board.create('reflection', [l1, li]);

        var cu1 = board.create('curve', [[-3, -3, -2.5, -3, -3, -2.5], [-3, -2, -2, -2, -2.5, -2.5]], {strokeWidth:3});
        var cu2 = board.create('reflection', [cu1, li], {strokeColor: 'red', strokeWidth:3});

        var pol1 = board.create('polygon', [[-6,-3], [-4,-5], [-5,-1.5]]);
        var pol2 = board.create('reflection', [pol1, li]);

        var c1 = board.create('circle', [[-2,-2], [-2, -1]]);
        var c2 = board.create('reflection', [c1, li]);

        var a1 = board.create('arc', [[1, 1], [0, 1], [1, 0]], {strokeColor: 'red'});
        var a2 = board.create('reflection', [a1, li], {strokeColor: 'red'});

        var s1 = board.create('sector', [[-3.5,-3], [-3.5, -2], [-3.5,-4]], {
                          anglePoint: {visible:true}, center: {visible: true}, radiusPoint: {visible: true},
                          fillColor: 'yellow', strokeColor: 'black'});
        var s2 = board.create('reflection', [s1, li], {fillColor: 'yellow', strokeColor: 'black', fillOpacity: 0.5});

        var an1 = board.create('angle', [[-4,3.9], [-3, 4], [-3, 3]]);
        var an2 = board.create('reflection', [an1, li]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[center](./Reflection.md#center)**  Attributes of circle center, i.e. |
|  | **[type](./Reflection.md#type)**  Type of transformation. |




### {center} **center**

Attributes of circle center, i.e. the center of the circle,
if a circle is the mirror element and the transformation type is 'Euclidean'
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {String} **type**

Type of transformation. Possible values are 'Euclidean', 'projective'.
If the value is 'Euclidean', the reflected element of a circle is again a circle,
otherwise it is a conic section.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'Euclidean'
