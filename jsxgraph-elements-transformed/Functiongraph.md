

# Functiongraph



## 描述

A functiongraph visualizes a map x → f(x). The graph is displayed for x in the interval [a,b] and is a [Curve](./Curve.md) element.   
  
*Defined in:*  [curve.js](./src/src_base_curve.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Functiongraph**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Functiongraph](./Functiongraph.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "functiongraph".  
  

Possible parent array combinations are:

{function} **f** {number|function} **a**   *Optional* {number|function} **b**   *Optional*
:   Parent elements are a function term f(x) describing the function graph.

    Further, an optional number or function for the left interval border a, and an optional number or function for the right interval border b.

    Default values are a=-10 and b=10.


### 示例

```javascript
// Create a function graph for f(x) = 0.5*x*x-2*x
  var graph = board.create('functiongraph',
                       [function(x){ return 0.5*x*x-2*x;}, -2, 4]
                    );
```

```javascript
// Create a function graph for f(x) = 0.5*x*x-2*x with variable interval
  var s = board.create('slider',[[0,4],[3,4],[-2,4,5]]);
  var graph = board.create('functiongraph',
                       [function(x){ return 0.5*x*x-2*x;},
                        -2,
                        function(){return s.Value();}]
                    );
```
