

# Input



## 描述

This element is used to provide a constructor for special texts containing a HTML form input element. For this element, the attribute "display" has to have the value 'html' (which is the default).

**Setting a CSS class:** The attribute cssClass affects the HTML div element that contains the input element. To change the CSS properties of the HTML input element a selector of the form .myinput > input { ... } has to be used. See the analog example for buttons: [Button](./Button.md).

**Access the input element with JavaScript:** The underlying HTML button element can be accessed through the sub-object 'rendNodeInput', e.g. to add event listeners.   
  
*Defined in:*  [input.js](./src/src_element_input.js.md).   
Extends [Text](./Text.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.CoordsElement**  
   ↳ **[JXG.Text](./JXG.Text.md)**  
      ↳ **[Text](./Text.md)**  
            ↳ **Input**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Input](./Input.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "input".  
  

Possible parent array combinations are:

{number|function} **x** {number|function} **y** {String} **value** {String|function} **label**
:   Parent elements for input elements.

    x and y are the coordinates of the lower left corner of the text box. The position of the text is fixed, x and y are numbers. The position is variable if x or y are functions.

    The default value of the input element must be given as string.

    The label of the input element may be given as string or function.


### 示例

```javascript
// Create an input element at position [1,4].
 var input = board.create('input', [0, 1, 'sin(x)*x', 'f(x)='], {cssStyle: 'width: 100px'});
 var f = board.jc.snippet(input.Value(), true, 'x', false);
 var graph = board.create('functiongraph',[f,
         function() {
           var c = new JXG.Coords(JXG.COORDS_BY_SCREEN,[0,0],board);
           return c.usrCoords[1];
         },
         function() {
           var c = new JXG.Coords(JXG.COORDS_BY_SCREEN,[board.canvasWidth,0],board);
           return c.usrCoords[1];
         }
       ]);

 board.create('text', [1, 3, '<button onclick="updateGraph()">Update graph</button>']);

 var updateGraph = function() {
     graph.Y = board.jc.snippet(input.Value(), true, 'x', false);
     graph.updateCurve();
     board.update();
 }
```

```javascript
// Add the `keyup` event to an input field
var A = board.create('point', [3, -2]);
var i = board.create('input', [-4, -4, "1", "x "]);

i.rendNodeInput.addEventListener("keyup", ( function () {
   var x = parseFloat(this.value);
   if (!isNaN(x)) {
	   A.moveTo([x, 3], 100);
   }
}));
```

```javascript
// Add the `change` event to an input field
var A = board.create('point', [3, -2]);
var i = board.create('input', [-4, -4, "1", "x "]);

i.rendNodeInput.addEventListener("change", ( function () {
   var x = parseFloat(i.Value());
   A.moveTo([x, 2], 100);
}));
```

```javascript
// change the width of an input field
 let s = board.create('slider', [[-3, 3], [2, 3], [50, 100, 300]]);
 let inp = board.create('input', [-6, 1, 'Math.sin(x)*x', 'f(x)='],{cssStyle:()=>'width:'+s.Value()+'px'});
```

```javascript
Apply CSS classes to label and input tag
    <style>
        div.JXGtext_inp {
            font-weight: bold;
        }

        // Label
        div.JXGtext_inp > span > span {
            padding: 3px;
        }

        // Input field
        div.JXGtext_inp > span > input {
            width: 100px;
            border: solid 4px red;
            border-radius: 25px;
        }
    </style>

var inp = board.create('input', [-6, 1, 'x', 'y'], {
     CssClass: 'JXGtext_inp', HighlightCssClass: 'JXGtext_inp'
});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[disabled](./Input.md#disabled)**  Control the attribute "disabled" of the HTML input field. |
|  | **[maxlength](./Input.md#maxlength)**  Control the attribute "maxlength" of the HTML input field. |




### {Boolean} **disabled**

Control the attribute "disabled" of the HTML input field.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {Number} **maxlength**

Control the attribute "maxlength" of the HTML input field.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   524288 (as in HTML)


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[set](./Input.md#set)**(val)  Sets value of the input element. |
|  | **[Value](./Input.md#Value)**()  Returns the value (content) of the input element |




### {[JXG.GeometryElement](./JXG.GeometryElement.md)} **set**(val)

Sets value of the input element.


#### Parameters:




#### Returns:

:   {[JXG.GeometryElement](./JXG.GeometryElement.md)} Reference to the element.


#### 示例

```javascript
var i1 = board.create('input', [-3, 4, 'sin(x)', 'f(x)='], {cssStyle: 'width:4em', maxlength: 2});
        var c1 = board.create('checkbox', [-3, 2, 'label 1'], {});
        var b1 = board.create('button', [-3, -1, 'Change texts', function () {
                i1.setText('g(x)');
                i1.set('cos(x)');
                c1.setText('label 2');
                b1.setText('Texts are changed');
            }],
            {cssStyle: 'width:400px'});
```



### {String} **Value**()

Returns the value (content) of the input element


#### Returns:

:   {String} content of the input field.
