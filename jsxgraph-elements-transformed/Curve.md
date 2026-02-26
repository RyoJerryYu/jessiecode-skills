

# Curve



## 描述

Curves can be defined by mappings or by discrete data sets. In general, a curve is a mapping from R to R^2, where t maps to (x(t),y(t)). The graph is drawn for t in the interval [a,b].

The following types of curves can be plotted:




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Curve**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Curve](./Curve.md#constructor)**  JXG.Curve x,y Parent elements for Data Plots. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "curve".  
  

Possible parent array combinations are:

{function|number} **x** {function|number} **y** {function|number} **a**   *Optional* {function|number} **b**   *Optional*
:   Parent elements for Parametric Curves.

    x describes the x-coordinate of the curve. It may be a function term in one variable, e.g. x(t). In case of x being of type number, x(t) is set to a constant function. this function at the values of the array.

    y describes the y-coordinate of the curve. In case of a number, y(t) is set to the constant function returning this number.

    Further parameters are an optional number or function for the left interval border a, and an optional number or function for the right interval border b.

    Default values are a=-10 and b=10.


### 示例

```javascript
// Parametric curve
// Create a curve of the form (t-sin(t), 1-cos(t), i.e.
// the cycloid curve.
  var graph = board.create('curve',
                       [function(t){ return t-Math.sin(t);},
                        function(t){ return 1-Math.cos(t);},
                        0, 2*Math.PI]
                    );
```

```javascript
// Data plots
// Connect a set of points given by coordinates with dashed line segments.
// The x- and y-coordinates of the points are given in two separate
// arrays.
  var x = [0,1,2,3,4,5,6,7,8,9];
  var y = [9.2,1.3,7.2,-1.2,4.0,5.3,0.2,6.5,1.1,0.0];
  var graph = board.create('curve', [x,y], {dash:2});
```

```javascript
// Polar plot
// Create a curve with the equation r(phi)= a*(1+phi), i.e.
// a cardioid.
  var a = board.create('slider',[[0,2],[2,2],[0,1,2]]);
  var graph = board.create('curve',
                       [function(phi){ return a.Value()*(1-Math.cos(phi));},
                        [1,0],
                        0, 2*Math.PI],
                        {curveType: 'polar'}
                    );
```

```javascript
// Draggable Bezier curve
 var col, p, c;
 col = 'blue';
 p = [];
 p.push(board.create('point',[-2, -1 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[1, 2.5 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[-1, -2.5 ], {size: 5, strokeColor:col, fillColor:col}));
 p.push(board.create('point',[2, -2], {size: 5, strokeColor:col, fillColor:col}));

 c = board.create('curve', JXG.Math.Numerics.bezier(p),
             {strokeColor:'red', name:"curve", strokeWidth:5, fixed: false}); // Draggable curve
 c.addParents(p);
```

```javascript
// The curve cu2 is the reflection of cu1 against line li
        var li = board.create('line', [1,1,1], {strokeColor: '#aaaaaa'});
        var reflect = board.create('transform', [li], {type: 'reflect'});
        var cu1 = board.create('curve', [[-1, -1, -0.5, -1, -1, -0.5], [-3, -2, -2, -2, -2.5, -2.5]]);
        var cu2 = board.create('curve', [cu1, reflect], {strokeColor: 'red'});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[curveType](../symbols/Curve.html#curveType)**  The curveType is set in [JXG.Curve#generateTerm](../symbols/JXG.Curve.html#generateTerm) and used in [JXG.Curve#updateCurve](./JXG.Curve.md#updateCurve). |
|  | **[doAdvancedPlot](./Curve.md#doAdvancedPlot)**  If true use a recursive bisection algorithm. |
|  | **[doAdvancedPlotOld](./Curve.md#doAdvancedPlotOld)**  If true use the algorithm by Gillam and Hohenwarter, which was default until version 0.98. |
|  | **[firstArrow](./Curve.md#firstArrow)**  Configure arrow head at the start position for curve. |
|  | **[handDrawing](./Curve.md#handDrawing)**  The data points of the curve are not connected with straight lines but with bezier curves. |
|  | **[label](./Curve.md#label)**  Attributes for curve label. |
|  | **[lastArrow](./Curve.md#lastArrow)**  Configure arrow head at the end position for curve. |
|  | **[numberPointsHigh](./Curve.md#numberPointsHigh)**  Number of points used for plotting triggered by up events (i.e. |
|  | **[numberPointsLow](./Curve.md#numberPointsLow)**  Number of points used for plotting triggered by move events (i.e. |
|  | **[plotVersion](./Curve.md#plotVersion)**  Select the version of the plot algorithm. |
|  | **[recursionDepthHigh](./Curve.md#recursionDepthHigh)**  Configure arrow head at the start position for curve. |
|  | **[recursionDepthLow](./Curve.md#recursionDepthLow)**  Number of points used for plotting triggered by move events in case (i.e. |




### {String} **curveType**

The curveType is set in [JXG.Curve#generateTerm](../symbols/JXG.Curve.html#generateTerm) and used in [JXG.Curve#updateCurve](./JXG.Curve.md#updateCurve).
Possible values are

* 'none'
* 'plot': Data plot
* 'parameter': we can not distinguish function graphs and parameter curves
* 'functiongraph': function graph
* 'polar'
* 'implicit' (not yet)

Only parameter and plot are set directly. Polar is set with [JXG.GeometryElement#setAttribute](./JXG.GeometryElement.md#setAttribute) only.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   null


### {Boolean} **doAdvancedPlot**

If true use a recursive bisection algorithm.
It is slower, but usually the result is better. It tries to detect jumps
and singularities.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true


### {Boolean} **doAdvancedPlotOld**

If true use the algorithm by Gillam and Hohenwarter, which was default until version 0.98.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Curve#doAdvancedPlot](./Curve.md#doAdvancedPlot)


#### Default Value:

:   false


### {Boolean | Object} **firstArrow**

Configure arrow head at the start position for curve.
Recommended arrow head type is 7.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Line#firstArrow](./Line.md#firstArrow) for options


#### Default Value:

:   false


### {Boolean} **handDrawing**

The data points of the curve are not connected with straight lines but with bezier curves.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {[Label](./Label.md)} **label**

Attributes for curve label.
  
*Defined in:*  [options.js](./src/src_options.js.md).


### {Boolean | Object} **lastArrow**

Configure arrow head at the end position for curve.
Recommended arrow head type is 7.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Line#lastArrow](./Line.md#lastArrow) for options


#### Default Value:

:   false


### {Number} **numberPointsHigh**

Number of points used for plotting triggered by up events
(i.e. high quality plotting) in case
[Curve#doAdvancedPlot](./Curve.md#doAdvancedPlot) is false.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Curve#doAdvancedPlot](./Curve.md#doAdvancedPlot)


#### Default Value:

:   1600


### {Number} **numberPointsLow**

Number of points used for plotting triggered by move events
(i.e. lower quality plotting but fast) in case
[Curve#doAdvancedPlot](./Curve.md#doAdvancedPlot) is false.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Curve#doAdvancedPlot](./Curve.md#doAdvancedPlot)


#### Default Value:

:   400


### {Number} **plotVersion**

Select the version of the plot algorithm.

* Version 1 is very outdated
* Version 2 is the default version in JSXGraph v0.99.\*, v1.0, and v1.1, v1.2.0
* Version 3 is an internal version that was never published in a stable version.
* Version 4 is available since JSXGraph v1.2.0

Version 4 plots correctly logarithms if the function term is supplied as string (i.e. as JessieCode)
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   2


### {Number} **recursionDepthHigh**

Configure arrow head at the start position for curve.
Recommended arrow head type is 7.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Curve#doAdvancedPlot](./Curve.md#doAdvancedPlot)


#### Default Value:

:   17


### {Number} **recursionDepthLow**

Number of points used for plotting triggered by move events in case
(i.e. lower quality plotting but fast)
[Curve#doAdvancedPlot](./Curve.md#doAdvancedPlot) is true.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Curve#doAdvancedPlot](./Curve.md#doAdvancedPlot)


#### Default Value:

:   13
