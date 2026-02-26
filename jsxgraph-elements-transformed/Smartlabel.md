

# Smartlabel



## 描述

Customized text elements for displaying measurements of JSXGraph elements, Examples are length of a segment, perimeter or area of a circle or polygon (including polygonal chain), slope of a line, value of an angle, and coordinates of a point.

If additionally a text, or a function is supplied and the content is not the empty string, that text is displayed instead of the measurement.

Smartlabels use custom made CSS layouts defined in jsxgraph.css. Therefore, the inclusion of the file jsxgraph.css is mandatory or the CSS classes have to be replaced by other classes.

The default attributes for smartlabels are defined for each type of measured element in the following sub-objects. This is a deviation from the usual JSXGraph attribute usage.




## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md),JXG.GeometryElement**  
   ↳ **[JXG.Text](./JXG.Text.md)**  
         ↳ **Smartlabel**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Smartlabel](./Smartlabel.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "smartlabel".  
  

Possible parent array combinations are:

{[JXG.GeometryElement](./JXG.GeometryElement.md)} **Parent**
:   parent object: point, line, circle, polygon, angle.
  
  

{String|Function} **Txt**
:   Optional text. In case, this content is not the empty string, the measurement is overwritten by this text.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p1 = board.create('point', [3, 4], {showInfobox: false, withLabel: false});
board.create('smartlabel', [p1], {digits: 1, unit: 'm', dir: 'col', useMathJax: false});
```

```javascript
var s1 = board.create('line', [[-7, 2], [6, -6]], {point1: {visible:true}, point2: {visible:true}});
board.create('smartlabel', [s1], {unit: 'm', measure: 'length', prefix: 'L = ', useMathJax: false});
board.create('smartlabel', [s1], {unit: 'm',  measure: 'slope', prefix: 'Δ = ', useMathJax: false});
```

```javascript
var c1 = board.create('circle', [[0, 1], [4, 1]], {point2: {visible: true}});
board.create('smartlabel', [c1], {unit: 'm', measure: 'perimeter', prefix: 'U = ', useMathJax: false});
board.create('smartlabel', [c1], {unit: 'm', measure: 'area', prefix: 'A = ', useMathJax: false});
board.create('smartlabel', [c1], {unit: 'm', measure: 'radius', prefix: 'R = ', useMathJax: false});
```

```javascript
var p2 = board.create('polygon', [[-6, -5], [7, -7], [-4, 3]], {});
board.create('smartlabel', [p2], {
    unit: 'm',
    measure: 'area',
    prefix: 'A = ',
    cssClass: 'smart-label-pure smart-label-polygon',
    highlightCssClass: 'smart-label-pure smart-label-polygon',
    useMathJax: false
});
board.create('smartlabel', [p2, () => 'X: ' + p2.vertices[0].X().toFixed(1)], {
    measure: 'perimeter',
    cssClass: 'smart-label-outline smart-label-polygon',
    highlightCssClass: 'smart-label-outline smart-label-polygon',
    useMathJax: false
});
```

```javascript
var a1 = board.create('angle', [[1, -1], [1, 2], [1, 5]], {name: 'β', withLabel: false});
var sma = board.create('smartlabel', [a1], {digits: 1, prefix: a1.name + '=', unit: '°', useMathJax: false});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[cssClass](./Smartlabel.md#cssClass)**  CSS classes for the smart label. |
|  | **[dir](./Smartlabel.md#dir)**  Display of point coordinates either as row vector or column vector. |
|  | **[highlightCssClass](./Smartlabel.md#highlightCssClass)**  CSS classes for the smart label when highlighted. |
|  | **[measure](./Smartlabel.md#measure)**  Type of measurement. |
|  | **[prefix](./Smartlabel.md#prefix)**  Prefix text for the smartlabel. |
|  | **[suffix](./Smartlabel.md#suffix)**  Suffix text for the smartlabel. |
|  | **[unit](./Smartlabel.md#unit)**  Measurement unit appended to the output text. |




### {String} **cssClass**

CSS classes for the smart label. Available classes are:

* 'smart-label-solid'
* 'smart-label-outline'
* 'smart-label-pure'

By default, an additional class is given specific for the element type.
Available classes are 'smart-label-angle', 'smart-label-circle',
'smart-label-line', 'smart-label-point', 'smart-label-polygon'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Smartlabel#highlightCssClass](./Smartlabel.md#highlightCssClass)


#### Default Value:

:   * 'smart-label-solid smart-label-circle' for circles
    * 'smart-label-solid smart-label-point' for points
    * ...


### {String} **dir**

Display of point coordinates either as row vector or column vector.
Available values are 'row' or 'column'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'row'


### {String} **highlightCssClass**

CSS classes for the smart label when highlighted.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Smartlabel#cssClass](./Smartlabel.md#cssClass)


#### Default Value:

:   * 'smart-label-solid smart-label-circle' for circles
    * 'smart-label-solid smart-label-point' for points
    * ...


### {String} **measure**

Type of measurement.
Available values are:

* 'deg', 'rad' for angles
* 'area', 'perimeter', 'radius' for circles
* 'length', 'slope' for lines
* 'area', 'perimeter' for polygons

Dependent on this value, i.e. the type of measurement, the label is
positioned differently on the object.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   * 'radius' for circles
    * 'length' for lines
    * 'area' for polygons
    * 'deg' for angles


### **prefix**

Prefix text for the smartlabel. Comes before the measurement value.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   ''


### **suffix**

Suffix text for the smartlabel. Comes after unit.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   ''


### **unit**

Measurement unit appended to the output text. For areas, the unit is squared automatically.
Comes directly after the measurement value.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   ''
