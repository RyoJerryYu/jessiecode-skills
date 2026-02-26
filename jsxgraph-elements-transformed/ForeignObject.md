

# ForeignObject



## 描述

Display any HTML content in an SVG foreignObject container - even below other elements.

Instead of board.create('foreignobject') the shortcut board.create('fo') may be used.

**NOTE:** In Safari up to version 15, a foreignObject does not obey the layer structure if it contains <video> or <iframe> tags, as well as elements which are positioned with position:absolute|relative|fixed. In this case, the foreignobject will be "above" the JSXGraph construction.




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.CoordsElement**  
   ↳ **[JXG.ForeignObject](./JXG.ForeignObject.md)**  
         ↳ **ForeignObject**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[ForeignObject](./ForeignObject.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "foreignobject".  
  

Possible parent array combinations are:

{String} **content**
:   HTML content of the foreignObject. May also be <video> or <iframe>
  
  

{Array} **position**
:   Position of the foreignObject given by [x, y] in user coordinates. Same as for images.
  
  

{Array} **size**
:   (Optional) argument size of the foreignObject in user coordinates. If not given, size is specified by the HTML attributes or CSS properties of the content.


### 示例

```javascript
var p = board.create('point', [1, 7], {size: 16});
var fo = board.create('foreignobject', [
    '<video width="300" height="200" src="https://eucbeniki.sio.si/vega2/278/Video_metanje_oge_.mp4" type="html5video" controls>',
    [0, -3], [9, 6]],
    {layer: 8, fixed: true}
 );
```

```javascript
var p = board.create('point', [1, 7], {size: 16});
var fo = board.create('fo', [
    '<div style="background-color:blue; color: yellow; padding:20px; width:200px; height:50px; ">Hello</div>',
    [-7, -6]],
    {layer: 1, fixed: false}
 );
```

```javascript
board.renderer.container.style.backgroundColor = 'lightblue';
var points = [];
points.push( board.create('point', [-2, 3.5], {fixed:false,color: 'yellow', size: 6,name:'6 am'}) );
points.push( board.create('point', [0, 3.5],  {fixed:false,color: 'yellow', size: 6,name:'12 pm'}) );
points.push( board.create('point', [2, 3.5],  {fixed:false,color: 'yellow', size: 6,name:'6 pm'}) );

var fo = board.create('fo', [
    '<video width="100%" height="100%" src="https://benedu.net/moodle/aaimg/ajx_img/astro/tr/1vd.mp4" type="html5video" controls>',
    [-6, -4], [12, 8]],
    {layer: 0, fixed: true}
 );

var f = JXG.Math.Numerics.lagrangePolynomial(points);
var graph = board.create('functiongraph', [f, -10, 10], {fixed:true,strokeWidth:3, layer: 8});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[attractors](./ForeignObject.md#attractors)**  List of attractor elements. |
|  | **[evaluateOnlyOnce](./ForeignObject.md#evaluateOnlyOnce)**  If set to true, this object is only evaluated once and not re-evaluated on update. |




### {Array} **attractors**

List of attractor elements. If the distance of the foreignobject is less than
attractorDistance the foreignobject is made to glider of this element.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   empty


### {Boolean} **evaluateOnlyOnce**

If set to true, this object is only evaluated once and not re-evaluated on update.
This is necessary if you want to have a board within a foreignObject of another board.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false
