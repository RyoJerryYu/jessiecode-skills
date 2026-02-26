

# Riemannsum



## 描述

Visualize the Riemann sum which is an approximation of an integral by a finite sum. It is realized as a special curve. The returned element has the method Value() which returns the sum of the areas of the bars.

In case of type "simpson" and "trapezoidal", the horizontal line approximating the function value is replaced by a parabola or a secant. IN case of "simpson", the parabola is approximated visually by a polygonal chain of fixed step width.   
  
*Defined in:*  [curve.js](./src/src_base_curve.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Riemannsum**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Riemannsum](./Riemannsum.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "riemannsum".  
  

Possible parent array combinations are:

{function|array} **f** {number|function} **n** {string|function} **type**   *Optional* {function|number} **a**   *Optional* {function|number} **b**   *Optional*
:   Parent elements of Riemannsum are a Either a function term f(x) describing the function graph which is filled by the Riemann bars, or an array consisting of two functions and the area between is filled by the Riemann bars.

    n determines the number of bars, it is either a fixed number or a function.

    type is a string or function returning one of the values: 'left', 'right', 'middle', 'lower', 'upper', 'random', 'simpson', or 'trapezoidal'. Default value is 'left'. "simpson" is Simpson's 1/3 rule.

    Further parameters are an optional number or function for the left interval border a, and an optional number or function for the right interval border b.

    Default values are a=-10 and b=10.


### 示例

```javascript
// Create Riemann sums for f(x) = 0.5*x*x-2*x.
  var s = board.create('slider',[[0,4],[3,4],[0,4,10]],{snapWidth:1});
  var f = function(x) { return 0.5*x*x-2*x; };
  var r = board.create('riemannsum',
              [f, function(){return s.Value();}, 'upper', -2, 5],
              {fillOpacity:0.4}
              );
  var g = board.create('functiongraph',[f, -2, 5]);
  var t = board.create('text',[-2,-2, function(){ return 'Sum=' + JXG.toFixed(r.Value(), 4); }]);
```

```javascript
// Riemann sum between two functions
  var s = board.create('slider',[[0,4],[3,4],[0,4,10]],{snapWidth:1});
  var g = function(x) { return 0.5*x*x-2*x; };
  var f = function(x) { return -x*(x-4); };
  var r = board.create('riemannsum',
              [[g,f], function(){return s.Value();}, 'lower', 0, 4],
              {fillOpacity:0.4}
              );
  var f = board.create('functiongraph',[f, -2, 5]);
  var g = board.create('functiongraph',[g, -2, 5]);
  var t = board.create('text',[-2,-2, function(){ return 'Sum=' + JXG.toFixed(r.Value(), 4); }]);
```



## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[Value](./Riemannsum.md#Value)**()  Returns the value of the Riemann sum, i.e. |




### {Number} **Value**()

Returns the value of the Riemann sum, i.e. the sum of the (signed) areas of the rectangles.


#### Returns:

:   {Number} value of Riemann sum.
