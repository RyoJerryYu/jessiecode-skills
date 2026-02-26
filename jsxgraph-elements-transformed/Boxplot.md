

# Boxplot



## 描述

Vertical or horizontal box plot curve to present numerical data through their quartiles. The direction of the box plot is controlled by the attribute "dir".   
  
*Defined in:*  [curve.js](./src/src_base_curve.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Boxplot**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Boxplot](./Boxplot.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "boxplot".  
  

Possible parent array combinations are:

{Array} **quantiles**
:   Array containing at least five quantiles. The elements can be of type number, function or string.
  
  

{Number|Function} **axis**
:   Axis position of the box plot
  
  

{Number|Function} **width**
:   Width of the rectangle part of the box plot. The width of the first and 4th quantile is relative to this width and can be controlled by the attribute "smallWidth".


### 示例

```javascript
var Q = [ -1, 2, 3, 3.5, 5 ];

var b = board.create('boxplot', [Q, 2, 4], {strokeWidth: 3});
```

```javascript
var Q = [ -1, 2, 3, 3.5, 5 ];
var b = board.create('boxplot', [Q, 3, 4], {dir: 'horizontal', smallWidth: 0.25, color:'red'});
```

```javascript
var data = [57, 57, 57, 58, 63, 66, 66, 67, 67, 68, 69, 70, 70, 70, 70, 72, 73, 75, 75, 76, 76, 78, 79, 81];
var Q = [];

Q[0] = JXG.Math.Statistics.min(data);
Q = Q.concat(JXG.Math.Statistics.percentile(data, [25, 50, 75]));
Q[4] = JXG.Math.Statistics.max(data);

var b = board.create('boxplot', [Q, 0, 3]);
```

```javascript
var mi = board.create('glider', [0, -1, board.defaultAxes.y]);
var ma = board.create('glider', [0, 5, board.defaultAxes.y]);
var Q = [function() { return mi.Y(); }, 2, 3, 3.5, function() { return ma.Y(); }];

var b = board.create('boxplot', [Q, 0, 2]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[dir](./Boxplot.md#dir)**  Direction of the box plot: 'vertical' or 'horizontal' |
|  | **[smallWidth](./Boxplot.md#smallWidth)**  Relative width of the maximum and minimum quantile |




### {String} **dir**

Direction of the box plot: 'vertical' or 'horizontal'
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'vertical'


### {Number} **smallWidth**

Relative width of the maximum and minimum quantile
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.5
