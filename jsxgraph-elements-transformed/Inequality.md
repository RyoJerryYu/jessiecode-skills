

# Inequality



## 描述

The area which is the set of solutions of a linear inequality or an inequality of a function graph. For example, an inequality of type y <= f(x).   
  
*Defined in:*  [composition.js](./src/src_element_composition.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **Inequality**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Inequality](./Inequality.md#constructor)**  Display the solution set of a linear inequality (less than or equal to). |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "inequality".  
  

Possible parent array combinations are:

{[JXG.Line](./JXG.Line.md)} **l**
:   The area drawn will be the area below this line. With the attribute inverse:true, the inequality 'greater than or equal to' is shown.


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var p = board.create('point', [1, 3]),
    q = board.create('point', [-2, -4]),
    l = board.create('line', [p, q]),
    ineq = board.create('inequality', [l]);
ineq = board.create('inequality', [l]);
```

```javascript
// Plot the inequality
//     y >= 2/3 x + 1
// or
//     0 >= -3y + 2x +1
var l = board.create('line', [1, 2, -3]),
    ineq = board.create('inequality', [l], {inverse:true});
```

```javascript
var f = board.create('functiongraph', ['sin(x)', -2*Math.PI, 2*Math.PI]);

var ineq_lower = board.create('inequality', [f]);
var ineq_greater = board.create('inequality', [f], {inverse: true, fillColor: 'yellow'});
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[inverse](./Inequality.md#inverse)**  By default an inequality is less (or equal) than. |




### {Boolean} **inverse**

By default an inequality is less (or equal) than. Set inverse to true will consider the inequality
greater (or equal) than.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   false
