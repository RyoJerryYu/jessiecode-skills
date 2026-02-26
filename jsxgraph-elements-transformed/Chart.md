

# Chart



## 描述

Various types of charts for data visualization.   
  
*Defined in:*  [chart.js](./src/src_base_chart.js.md).   
Extends [JXG.Chart](./JXG.Chart.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Chart](./JXG.Chart.md)**  
         ↳ **Chart**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Chart](./Chart.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "chart".  
  

Possible parent array combinations are:

{Array} **x**
:   Array of x-coordinates (default case, see below for alternatives)
  
  

{Array} **y**
:   Array of y-coordinates (default case, see below for alternatives)

    The parent array may be of one of the following forms:

    1. Parents array looks like [number, number, number, ...]. It is interpreted as array of y-coordinates. The x coordinates are automatically set to [1, 2, ...]
    2. Parents array looks like [[number, number, number, ...]]. The content is interpreted as array of y-coordinates. The x coordinates are automatically set to [1, 2, ...]x coordinates are automatically set to [1, 2, ...] Default case: [[x0,x1,x2,...],[y1,y2,y3,...]]

    The attribute value for the key 'chartStyle' determines the type(s) of the chart. 'chartStyle' is a comma separated list of strings of the possible chart types 'bar', 'fit', 'line', 'pie', 'point', 'radar', 'spline'.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
board = JXG.JSXGraph.initBoard('jxgbox', {boundingbox:[-0.5,8,9,-2],axis:true});

  var f = [4, 2, -1, 3, 6, 7, 2];
  var chart = board.create('chart', f,
                {chartStyle:'bar',
                 width:0.8,
                 labels:f,
                 colorArray:['#8E1B77','#BE1679','#DC1765','#DA2130','#DB311B','#DF4917','#E36317','#E87F1A',
                             '#F1B112','#FCF302','#C1E212'],
                 label: {fontSize:30, display:'internal', anchorX:'left', rotate:90}
            });
```

```javascript
board = JXG.JSXGraph.initBoard('jxgbox', {boundingbox: [-1, 9, 13, -3], axis:true});

  var s = board.create('slider', [[4,7],[8,7],[1,1,1.5]], {name:'S', strokeColor:'black', fillColor:'white'});
  var f = [function(){return (s.Value()*4.5).toFixed(2);},
                     function(){return (s.Value()*(-1)).toFixed(2);},
                     function(){return (s.Value()*3).toFixed(2);},
                     function(){return (s.Value()*2).toFixed(2);},
                     function(){return (s.Value()*(-0.5)).toFixed(2);},
                     function(){return (s.Value()*5.5).toFixed(2);},
                     function(){return (s.Value()*2.5).toFixed(2);},
                     function(){return (s.Value()*(-0.75)).toFixed(2);},
                     function(){return (s.Value()*3.5).toFixed(2);},
                     function(){return (s.Value()*2).toFixed(2);},
                     function(){return (s.Value()*(-1.25)).toFixed(2);}
                     ];
  var chart = board.create('chart', [f],
                                            {chartStyle:'bar',width:0.8,labels:f,
                                             colorArray:['#8E1B77','#BE1679','#DC1765','#DA2130','#DB311B','#DF4917','#E36317','#E87F1A',
                                                         '#F1B112','#FCF302','#C1E212']});

  var dataArr = [4,1,3,2,5,6.5,1.5,2,0.5,1.5,-1];
  var chart2 = board.create('chart', dataArr, {chartStyle:'line,point'});
  chart2[0].setAttribute('strokeColor:black','strokeWidth:2pt');
  for(var i=0; i<11;i++) {
           chart2[1][i].setAttribute({strokeColor:'black',fillColor:'white',face:'[]', size:4, strokeWidth:'2pt'});
  }
  board.unsuspendUpdate();
```

```javascript
var dataArr = [4, 1.2, 3, 7, 5, 4, 1.54, function () { return 2; }];
        var a = board.create('chart', dataArr, {
                chartStyle:'pie', colors:['#B02B2C','#3F4C6B','#C79810','#D15600'],
                fillOpacity:0.9,
                center:[5,2],
                strokeColor:'#ffffff',
                strokeWidth:6,
                highlightBySize:true,
                highlightOnSector:true
            });
```

```javascript
board = JXG.JSXGraph.initBoard('jxgbox', {boundingbox: [-12, 12, 20, -12], axis: false});
            board.suspendUpdate();
            // See labelArray and paramArray
            var dataArr = [[23, 14, 15.0], [60, 8, 25.0], [0, 11.0, 25.0], [10, 15, 20.0]];

            var a = board.create('chart', dataArr, {
                chartStyle:'radar',
                colorArray:['#0F408D','#6F1B75','#CA147A','#DA2228','#E8801B','#FCF302','#8DC922','#15993C','#87CCEE','#0092CE'],
                //fillOpacity:0.5,
                //strokeColor:'black',
                //strokeWidth:1,
                //polyStrokeWidth:1,
                paramArray:['Speed','Flexibility', 'Costs'],
                labelArray:['Ruby','JavaScript', 'PHP', 'Python'],
                //startAngle:Math.PI/4,
                legendPosition:'right',
                //"startShiftRatio": 0.1,
                //endShiftRatio:0.1,
                //startShiftArray:[0,0,0],
                //endShiftArray:[0.5,0.5,0.5],
                start:0
                //end:70,
                //startArray:[0,0,0],
                //endArray:[7,7,7],
                //radius:3,
                //showCircles:true,
                //circleLabelArray:[1,2,3,4,5],
                //highlightColorArray:['#E46F6A','#F9DF82','#F7FA7B','#B0D990','#69BF8E','#BDDDE4','#92C2DF','#637CB0','#AB91BC','#EB8EBF'],
            });
            board.unsuspendUpdate();
```
