

# Legend



## 描述

Creates a legend for a chart element. Parameter is a pair of coordinates. The label names and the label colors are supplied in the attributes:




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Legend](./JXG.Legend.md)**  
         ↳ **Legend**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Legend](./Legend.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "legend".  
  

Possible parent array combinations are:

{Number} **x**
:   Horizontal coordinate of the left top point of the legend
  
  

{Number} **y**
:   Vertical coordinate of the left top point of the legend


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var board = JXG.JSXGraph.initBoard('jxgbox', {axis:true,boundingbox:[-4,48.3,12.0,-2.3]});
var x       = [-3,-2,-1,0,1,2,3,4,5,6,7,8];
var dataArr = [4,7,7,27,33,37,46,22,11,4,1,0];

colors = ['green', 'yellow', 'red', 'blue'];
board.create('chart', [x,dataArr], {chartStyle:'bar', width:1.0, labels:dataArr, colors: colors} );
board.create('legend', [8, 45], {labels:dataArr, colors: colors, strokeWidth:5} );
```

```javascript
var inputFun, cf = [], cf2 = [], niveaunum,
    niveauline = [], niveauopac = [],legend;

  inputFun = "x^2/2-2*x*y+y^2/2";
  niveauline = [-3,-2,-1,-0.5, 0, 1,2,3];
  niveaunum = niveauline.length;
  for (let i = 0; JXG.Math.lt(i, niveaunum); i++) {
    let niveaui = niveauline[i];
    niveauopac.push(((i + 1) / (niveaunum + 1)));
    cf.push(board.create("implicitcurve", [
      inputFun + "-(" + niveaui.toFixed(2) + ")", [-2, 2], [-2, 2]], {
      strokeWidth: 2,
      strokeColor: JXG.palette.red,
      strokeOpacity: niveauopac[i],
      needsRegularUpdate: false,
      name: "niveau"+i,
      visible: true
    }));
  }
  legend = board.create('legend', [-1.75, 1.75], {
    labels: niveauline,
    colors: [cf[0].visProp.strokecolor],
    strokeOpacity: niveauopac,
    linelength: 0.2,
    frozen:true
  }
  );
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[colors](./Legend.md#colors)**  (Circular) array of label colors. |
|  | **[frozen](./Legend.md#frozen)**  The element can be fixed and may not be dragged around. |
|  | **[labels](./Legend.md#labels)**  Label names of a legend element. |
|  | **[lineLength](./Legend.md#lineLength)**  Length of line in one legend entry |
|  | **[rowHeight](./Legend.md#rowHeight)**  Height (in px) of one legend entry |
|  | **[strokeOpacity](./Legend.md#strokeOpacity)**  (Circular) array of opacity for legend line stroke color for one legend entry. |
|  | **[strokeWidth](./Legend.md#strokeWidth)**  Height (in px) of one legend entry |
|  | **[style](./Legend.md#style)**  Default style of a legend element. |




### {Array} **colors**

(Circular) array of label colors.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   "['#B02B2C', '#3F4C6B', '#C79810', '#D15600', '#FFFF88', '#c3d9ff', '#4096EE', '#008C00']"


### {Boolean} **frozen**

The element can be fixed and may not be dragged around. If true, the legend will even stay at its position on zoom and
moveOrigin events.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [JXG.GeometryElement#frozen](./JXG.GeometryElement.md#frozen)


#### Default Value:

:   false


### {Array} **labels**

Label names of a legend element.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   "['1', '2', '3', '4', '5', '6', '7', '8']"


### {Number} **lineLength**

Length of line in one legend entry
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   1


### {Number} **rowHeight**

Height (in px) of one legend entry
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   20


### {Array} **strokeOpacity**

(Circular) array of opacity for legend line stroke color for one legend entry.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   [1]


### {Number} **strokeWidth**

Height (in px) of one legend entry
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   5


### {String} **style**

Default style of a legend element. The only possible value is 'vertical'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'vertical'
