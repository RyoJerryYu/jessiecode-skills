

# Checkbox



## 描述

A text element that contains an HTML checkbox tag. For this element, the attribute "display" has to have the value 'html' (which is the default).

**Setting a CSS class:** The attribute cssClass affects the HTML div element that contains the checkbox element. To change the CSS properties of the HTML checkbox element a selector of the form .mycheck > checkbox { ... } has to be used. See the analog example for buttons: [Button](./Button.md).

**Access the checkbox element with JavaScript:** The underlying HTML checkbox element can be accessed through the sub-object 'rendNodeCheck', e.g. to add event listeners.   
  
*Defined in:*  [checkbox.js](./src/src_element_checkbox.js.md).   
Extends [Text](./Text.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md),JXG.CoordsElement**  
   ↳ **[JXG.Text](./JXG.Text.md)**  
      ↳ **[Text](./Text.md)**  
            ↳ **Checkbox**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Checkbox](./Checkbox.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "checkbox".  
  

Possible parent array combinations are:

{number|function} **x** {number|function} **y** {String|function} **label**
:   Parent elements for checkbox elements.

    x and y are the coordinates of the lower left corner of the text box. The position of the text is fixed, x and y are numbers. The position is variable if x or y are functions.

    The label of the input element may be given as string or function.

    The value of the checkbox can be controlled with the attribute checked

    The HTML node can be accessed with element.rendNodeCheckbox


### 示例

```javascript
// Create a checkbox element at position [0,3].
  var checkbox = board.create('checkbox', [0, 3, 'Change Y'], {});
  var p = board.create('point', [
      function(){ return 0.5;}, // X-coordinate
      function() {
          y = 0.5;
          if (checkbox.Value()) {
              y += 0.5;
          }
          return y;
      }]);
```

```javascript
var checkbox = board.create('checkbox', [0, 4, 'Click me']),
    p = board.create('point', [1, 1]);

JXG.addEvent(checkbox.rendNodeCheckbox, 'change', function() {
    if (this.Value()) {
        p.moveTo([4, 1]);
    } else {
        p.moveTo([1, 1]);
    }
}, checkbox);
```

```javascript
var i1 = board.create('input', [1, 5, 'sin(x)', 'f(x)='], {cssStyle: 'width:4em', maxlength: 2});
        var c1 = board.create('checkbox', [1, 3, 'label 1'], {});
        var b1 = board.create('button', [1, 1, 'Change texts', function () {
                i1.setText('g(x)=');
                i1.set('cos(x)');
                c1.setText('label 2');
                b1.setText('Texts are changed');
            }],
            {cssStyle: 'width:200px'});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[checked](./Checkbox.md#checked)**  Control the attribute "checked" of the HTML checkbox. |
|  | **[disabled](./Checkbox.md#disabled)**  Control the attribute "disabled" of the HTML checkbox. |




### {Boolean} **checked**

Control the attribute "checked" of the HTML checkbox.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


### {Boolean} **disabled**

Control the attribute "disabled" of the HTML checkbox.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[Value](./Checkbox.md#Value)**()  Returns the value of the checkbox element |




### {String} **Value**()

Returns the value of the checkbox element


#### Returns:

:   {String} value of the checkbox.
