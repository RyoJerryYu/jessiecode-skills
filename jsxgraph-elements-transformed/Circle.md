

# Circle



## 描述

A circle can be defined by various combinations of points and numbers.   
  
*Defined in:*  [circle.js](./src/src_base_circle.js.md).   
Extends [JXG.Circle](./JXG.Circle.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Circle](./JXG.Circle.md)**  
         ↳ **Circle**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Circle](./Circle.md#constructor)**  A circle consists of all points with a given distance from one point. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "circle".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **center** {number|[JXG.Point](../symbols/JXG.Point.html)|[JXG.Line](../symbols/JXG.Line.html)|[JXG.Circle](./JXG.Circle.md)} **radius**
:   The center must be given as a [JXG.Point](../symbols/JXG.Point.html), see [JXG.providePoints](./JXG.md#.providePoints), but the radius can be given as a number (which will create a circle with a fixed radius), another [JXG.Point](../symbols/JXG.Point.html), a [JXG.Line](../symbols/JXG.Line.html) (the distance of start and end point of the line will determine the radius), or another [JXG.Circle](./JXG.Circle.md).

    If the radius is supplied as number or output of a function, its absolute value is taken.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a circle providing two points
var p1 = board.create('point', [2.0, 2.0]),
    p2 = board.create('point', [2.0, 0.0]),
    c1 = board.create('circle', [p1, p2]);

// Create another circle using the above circle
var p3 = board.create('point', [3.0, 2.0]),
    c2 = board.create('circle', [p3, c1]);
```

```javascript
// Create a circle providing two points
var p1 = board.create('point', [2.0, 2.0]),
    c1 = board.create('circle', [p1, 3]);

// Create another circle using the above circle
var c2 = board.create('circle', [function() { return [p1.X(), p1.Y() + 1];}, function() { return c1.Radius(); }]);
```

```javascript
var li = board.create('line', [1,1,1], {strokeColor: '#aaaaaa'});
var reflect = board.create('transform', [li], {type: 'reflect'});

var c1 = board.create('circle', [[-2,-2], [-2, -1]], {center: {visible:true}});
var c2 = board.create('circle', [c1, reflect]);
     *
```

```javascript
var t = board.create('transform', [2, 1.5], {type: 'scale'});
var c1 = board.create('circle', [[1.3, 1.3], [0, 1.3]], {strokeColor: 'black', center: {visible:true}});
var c2 = board.create('circle', [c1, t], {strokeColor: 'black'});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[center](./Circle.md#center)**  Attributes for center point. |
|  | **[hasInnerPoints](./Circle.md#hasInnerPoints)**  If true, moving the mouse over inner points triggers hasPoint. |
|  | **[label](./Circle.md#label)**  Attributes for circle label. |
|  | **[point](./Circle.md#point)**  Attributes for center point. |
|  | **[point2](./Circle.md#point2)**  Attributes for center point. |




### {[Point](./Point.md)} **center**

Attributes for center point.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {Boolean} **hasInnerPoints**

If true, moving the mouse over inner points triggers hasPoint.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [JXG.GeometryElement#hasPoint](./JXG.GeometryElement.md#hasPoint)


#### Default Value:

:   false


### {[Label](./Label.md)} **label**

Attributes for circle label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **point**

Attributes for center point.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {[Point](./Point.md)} **point2**

Attributes for center point.
  
*Defined in:*  [options.js](./src/src_options.js.md).
