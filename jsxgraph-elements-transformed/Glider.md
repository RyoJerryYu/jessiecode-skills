

# Glider



## 描述

A glider is a point bound to a line, circle or curve or even another point.   
  
*Defined in:*  [point.js](./src/src_base_point.js.md).   
Extends [JXG.Point](./JXG.Point.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.CoordsElement**  
   ↳ **[JXG.Point](./JXG.Point.md)**  
         ↳ **Glider**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Glider](./Glider.md#constructor)**  A glider is a point which lives on another geometric element like a line, circle, curve, turtle. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "glider".  
  

Possible parent array combinations are:

{Number} **z**   *Optional* {Number} **x**   *Optional* {Number} **y**   *Optional* {[JXG.GeometryElement](./JXG.GeometryElement.md)} **GlideObject**
:   Parent elements can be two or three elements of type number and the object the glider lives on. The coordinates are completely optional. If not given the origin is used. If you provide two numbers for coordinates they will be interpreted as affine Euclidean coordinates, otherwise they will be interpreted as homogeneous coordinates. In any case the point will be projected on the glide object.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
// Create a glider with user defined coordinates. If the coordinates are not on
// the circle (like in this case) the point will be projected onto the circle.
var p1 = board.create('point', [2.0, 2.0]);
var c1 = board.create('circle', [p1, 2.0]);
var p2 = board.create('glider', [2.0, 1.5, c1]);
```

```javascript
// Create a glider with default coordinates (1,0,0). Same premises as above.
var p1 = board.create('point', [2.0, 2.0]);
var c1 = board.create('circle', [p1, 2.0]);
var p2 = board.create('glider', [c1]);
```

```javascript
//animate example 2
var p1 = board.create('point', [2.0, 2.0]);
var c1 = board.create('circle', [p1, 2.0]);
var p2 = board.create('glider', [c1]);
var button1 = board.create('button', [1, 7, 'start animation',function(){p2.startAnimation(1,4)}]);
var button2 = board.create('button', [1, 5, 'stop animation',function(){p2.stopAnimation()}]);
```



## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[startAnimation](./Glider.md#startAnimation)**(direction, stepCount, delay, maxRounds)  Animate a point. |
|  | **[stopAnimation](./Glider.md#stopAnimation)**()  Stop animation. |




### {[JXG.CoordsElement](./JXG.CoordsElement.md)} **startAnimation**(direction, stepCount, delay, maxRounds)

Animate a point.
  
*Defined in:*  [coordselement.js](./src/src_base_coordselement.js.md).


#### Parameters:

:   The direction the glider is animated. Can be +1 or -1.
:   The number of steps in which the parent element is divided.
    Must be at least 1.
:   Time in msec between two animation steps. Default is 250.
:   The number of rounds the glider will be animated. The glider will run infinitely if
    maxRounds is negative or equal to Infinity.


#### Returns:

:   {[JXG.CoordsElement](./JXG.CoordsElement.md)} Reference to itself.


#### See:

:   [Glider#stopAnimation](./Glider.md#stopAnimation)


#### 示例

```javascript
// Divide the circle line into 6 steps and
// visit every step 330 msec counterclockwise.
var ci = board.create('circle', [[-1,2], [2,1]]);
var gl = board.create('glider', [0,2, ci]);
gl.startAnimation(-1, 6, 330);
```

```javascript
//animate example closed curve
var c1 = board.create('curve',[(u)=>4*Math.cos(u),(u)=>2*Math.sin(u)+2,0,2*Math.PI]);
var p2 = board.create('glider', [c1]);
var button1 = board.create('button', [1, 7, 'start animation',function(){p2.startAnimation(1,8)}]);
var button2 = board.create('button', [1, 5, 'stop animation',function(){p2.stopAnimation()}]);
```

```javascript
// Divide the slider area into 20 steps and
// visit every step 30 msec. Stop after 2 rounds.
var n = board.create('slider',[[-2,4],[2,4],[1,5,100]],{name:'n'});
n.startAnimation(1, 20, 30, 2);
```



### {[JXG.CoordsElement](./JXG.CoordsElement.md)} **stopAnimation**()

Stop animation.
  
*Defined in:*  [coordselement.js](./src/src_base_coordselement.js.md).


#### Returns:

:   {[JXG.CoordsElement](./JXG.CoordsElement.md)} Reference to itself.


#### See:

:   [Glider#startAnimation](./Glider.md#startAnimation)
