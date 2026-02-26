

# Button



## 描述

A text element that contains an HTML button tag. For this element, the attribute "display" has to have the value 'html' (which is the default).

**Setting a CSS class:** The attribute cssClass affects the HTML div element that contains the button element. To change the CSS properties of the HTML button element a selector of the form .mybutton > button { ... } has to be used. See the example below.

**Access the button element with JavaScript:** The underlying HTML button element can be accessed through the sub-object 'rendNodeButton', e.g. to add event listeners.   
  
*Defined in:*  [button.js](./src/src_element_button.js.md).   
Extends [Text](./Text.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.CoordsElement**  
   ↳ **[JXG.Text](./JXG.Text.md)**  
      ↳ **[Text](./Text.md)**  
            ↳ **Button**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Button](./Button.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "button".  
  

Possible parent array combinations are:

{number|function} **x** {number|function} **y** {String|function} **label** {function} **handler**
:   Parent elements for button elements.

    x and y are the coordinates of the lower left corner of the text box. The position of the text is fixed, x and y are numbers. The position is variable if x or y are functions.

    The label of the input element may be given as string.

    The (optional) handler function which is called when the button is pressed.


### 示例

```javascript
var p = board.create('point', [0.5, 0.5], {id: 'p1'});

 // Create a button element at position [1,2].
 var button1 = board.create('button', [1, 2, 'Change Y with JavaScript', function() {
     p.moveTo([p.X(), p.Y() + 0.5], 100);
 }], {});

 // Create a button element at position [1,4].
 var button2 = board.create('button', [1, 4, 'Change Y with JessieCode',
     "$('p1').Y = $('p1').Y() - 0.5;"
 ], {});
```

```javascript
// A toggle button
var butt = board.create('button', [-2, -2, 'Off', function() {
  var txt;
  butt.value = !butt.value;
  if (butt.value) {
  	txt = 'On';
  } else {
  	txt = 'Off';
  }
	butt.rendNodeButton.innerHTML = txt;
}]);

// Set initial value for the button
if (!JXG.exists(butt.value)) {
	butt.value = false;
}

var p = board.create('point', [2, -2], {
	visible: () => butt.value
});
```

```javascript
var i1 = board.create('input', [-3, 4, 'sin(x)', 'f(x)='], {cssStyle: 'width:4em', maxlength: 2});
var c1 = board.create('checkbox', [-3, 2, 'label 1'], {});
var b1 = board.create('button', [-3, -1, 'Change texts', function () {
        i1.setText('g(x)');
        i1.set('cos(x)');
        c1.setText('label 2');
        b1.setText('Texts are changed');
    }],
    {cssStyle: 'width:200px'});
```

```javascript
// Set the CSS class of the button

// CSS:
<style>
.mybutton > button {
  background-color: #04AA6D;
  border: none;
  color: white;
  padding: 1px 3px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
</style>

// JavaScript:
var button = board.create('button',
    [1, 4, 'answers', function () {}],
    {cssClass:'mybutton', highlightCssClass: 'mybutton'});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[disabled](./Button.md#disabled)**  Control the attribute "disabled" of the HTML button. |




### {Boolean} **disabled**

Control the attribute "disabled" of the HTML button.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false
