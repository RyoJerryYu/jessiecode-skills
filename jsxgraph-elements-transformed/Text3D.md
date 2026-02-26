

# Text3D



## 描述

Construct a text element in a 3D view.   
  
*Defined in:*  [text3d.js](./src/src_3d_text3d.js.md).   
Extends [JXG.Text3D](../symbols/JXG.Text3D.html), [Text](./Text.md).




## 继承关系

**[JXG.Text3D](./JXG.Text3D.md),Text**  
      ↳ **Text3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Text3D](./Text3D.md#constructor)**  A Text3D object is defined by 3 coordinates [x, y, z, text] or an array / function for the position of the text and a string or function defining the text. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "text3d".  
  

Possible parent array combinations are:

{number|function} **x** {number|function} **y** {number|function} **z** {String|function} **txt** {[JXG.GeometryElement3D](./JXG.GeometryElement3D.md)} **[slide=undefined]**
:   The coordinates are given as x, y, z consisting of numbers of functions and the text. If an optional 3D element "slide" is supplied, the point is a glider on that element.
  
  
:   F,txt,[slide=undefined] Alternatively, the coordinates can be supplied as array or function returning an array. If an optional 3D element "slide" is supplied, the point is a glider on that element.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent
objects an exception is thrown.


### 示例

```javascript
var bound = [-4, 6];
    var view = board.create('view3d',
        [[-4, -3], [8, 8],
        [bound, bound, bound]],
        {
            projection: 'central'
        });

    var txt1 = view.create('text3d', [[1, 2, 1], 'hello'], {
        fontSize: 20,
    });
```



## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
| <private> <static> | Text3D.**[normalizeCoords](./Text3D.md#.normalizeCoords)**()  Normalize homogeneous coordinates such the the first coordinate (the w-coordinate is equal to 1 or 0)- |
| <static> | Text3D.**[setPosition](./Text3D.md#.setPosition)**(coords, noevent)  Set the position of a 3D point. |
| <private> <static> | Text3D.**[updateCoords](./Text3D.md#.updateCoords)**()  Update the homogeneous coords array. |




### <private> <static> {Object} Text3D.**normalizeCoords**()

Normalize homogeneous coordinates such the the first coordinate (the w-coordinate is equal to 1 or 0)-


#### Returns:

:   {Object} Reference to the Text3D object


#### 示例

```javascript
p.normalizeCoords();
```



### <static> {Object} Text3D.**setPosition**(coords, noevent)

Set the position of a 3D point.


#### Parameters:

:   3D coordinates. Either of the form [x,y,z] (Euclidean) or [w,x,y,z] (homogeneous).
:   If true, no events are triggered.


#### Returns:

:   {Object} Reference to the Text3D object


#### 示例

```javascript
p.setPosition([1, 3, 4]);
```



### <private> <static> {Object} Text3D.**updateCoords**()

Update the homogeneous coords array.


#### Returns:

:   {Object} Reference to the Text3D object


#### 示例

```javascript
p.updateCoords();
```
