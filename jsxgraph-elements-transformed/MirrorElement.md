

# MirrorElement



## 描述

Reflect a point, line, circle, curve, polygon across a given point.   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.GeometryElement](./JXG.GeometryElement.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
      ↳ **MirrorElement**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[MirrorElement](./MirrorElement.md#constructor)**  A mirror element is determined by the reflection of a given point, line, circle, curve, polygon across another given point. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "mirrorelement".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)|[JXG.Line](../symbols/JXG.Line.html)|[JXG.Curve](../symbols/JXG.Curve.html)|JXG.Ppolygon} **p1** {[JXG.Point](./JXG.Point.md)} **p2**
:   The constructed element is the mirror image of p2 across p1.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// point of reflection
        var mirr = board.create('point', [-1,-1], {color: '#aaaaaa'});

        var p1 = board.create('point', [-3,-1], {name: "A"});
        var q1 = board.create('mirrorelement', [p1, mirr], {name: "A'"});

        var l1 = board.create('line', [1, -5, 1]);
        var l2 = board.create('mirrorelement', [l1, mirr]);

        var cu1 = board.create('curve', [[-3, -3, -2.5, -3, -3, -2.5], [-3, -2, -2, -2, -2.5, -2.5]], {strokeWidth:3});
        var cu2 = board.create('mirrorelement', [cu1, mirr], {strokeColor: 'red', strokeWidth:3});

        var pol1 = board.create('polygon', [[-6,-2], [-4,-4], [-5,-0.5]]);
        var pol2 = board.create('mirrorelement', [pol1, mirr]);

        var c1 = board.create('circle', [[-6,-6], [-6, -5]]);
        var c2 = board.create('mirrorelement', [c1, mirr]);

        var a1 = board.create('arc', [[1, 1], [0, 1], [1, 0]], {strokeColor: 'red'});
        var a2 = board.create('mirrorelement', [a1, mirr], {strokeColor: 'red'});

        var s1 = board.create('sector', [[-3.5,-3], [-3.5, -2], [-3.5,-4]], {
                          anglePoint: {visible:true}, center: {visible: true}, radiusPoint: {visible: true},
                          fillColor: 'yellow', strokeColor: 'black'});
        var s2 = board.create('mirrorelement', [s1, mirr], {fillColor: 'yellow', strokeColor: 'black', fillOpacity: 0.5});

        var an1 = board.create('angle', [[-4,3.9], [-3, 4], [-3, 3]]);
        var an2 = board.create('mirrorelement', [an1, mirr]);
```
