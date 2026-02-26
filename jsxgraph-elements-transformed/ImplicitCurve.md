

# ImplicitCurve



## 描述

An implicit curve is a plane curve defined by an implicit equation relating two coordinate variables, commonly *x* and *y*. For example, the unit circle is defined by the implicit equation x2 + y2 = 1. In general, every implicit curve is defined by an equation of the form *f(x, y) = 0* for some function *f* of two variables. ([Wikipedia](https://en.wikipedia.org/wiki/Implicit_curve))

The partial derivatives for *f* are optional. If not given, numerical derivatives are used instead. This is good enough for most practical use cases. But if supplied, both partial derivatives must be supplied.

The most effective attributes to tinker with if the implicit curve algorithm fails are [ImplicitCurve#resolution\_outer](../symbols/ImplicitCurve.html#resolution_outer), [ImplicitCurve#resolution\_inner](../symbols/ImplicitCurve.html#resolution_inner), [ImplicitCurve#alpha\_0](../symbols/ImplicitCurve.html#alpha_0), [ImplicitCurve#h\_initial](../symbols/ImplicitCurve.html#h_initial), [ImplicitCurve#h\_max](../symbols/ImplicitCurve.html#h_max), and [ImplicitCurve#qdt\_box](./ImplicitCurve.md#qdt_box).   
  
*Defined in:*  [curve.js](./src/src_base_curve.js.md).   
Extends [JXG.Curve](./JXG.Curve.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
         ↳ **ImplicitCurve**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[ImplicitCurve](./ImplicitCurve.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "implicitcurve".  
  

Possible parent array combinations are:

{Function|String} **f**
:   Function of two variables for the left side of the equation *f(x,y)=0*. If f is supplied as string, it has to use the variables 'x' and 'y'.
  
  

{Function|String} **dfx**
:   Optional partial derivative in respect to the first variable If dfx is supplied as string, it has to use the variables 'x' and 'y'.
  
  

{Function|String} **dfy**
:   Optional partial derivative in respect to the second variable If dfy is supplied as string, it has to use the variables 'x' and 'y'.
  
  

{Array|Function} **rangex**
:   Optional array of length 2 of the form [x\_min, x\_max] setting the domain of the x coordinate of the implicit curve. If not supplied, the board's boundingbox (+ the attribute "margin") is taken.
  
  

{Array|Function} **rangey**
:   Optional array of length 2 of the form [y\_min, y\_max] setting the domain of the y coordinate of the implicit curve. If not supplied, the board's boundingbox (+ the attribute "margin") is taken.


### 示例

```javascript
var f, c;
  f = (x, y) => 1 / 16 * x ** 2 + y ** 2 - 1;
  c = board.create('implicitcurve', [f], {
      strokeWidth: 3,
      strokeColor: JXG.palette.red,
      strokeOpacity: 0.8
  });
```

```javascript
var a, c, f;
 a = board.create('slider', [[-3, 6], [3, 6], [-3, 1, 3]], {
     name: 'a', stepWidth: 0.1
 });
 f = (x, y) => x ** 2 - 2 * x * y - 2 * x + (a.Value() + 1) * y ** 2 + (4 * a.Value() + 2) * y + 4 * a.Value() - 3;
 c = board.create('implicitcurve', [f], {
     strokeWidth: 3,
     strokeColor: JXG.palette.red,
     strokeOpacity: 0.8,
     resolution_outer: 20,
     resolution_inner: 20
 });
```

```javascript
var c = board.create('implicitcurve', ['abs(x * y) - 3'], {
     strokeWidth: 3,
     strokeColor: JXG.palette.red,
     strokeOpacity: 0.8
 });
```

```javascript
var niveauline = [];
niveauline = [0.5, 1, 1.5, 2];
for (let i = 0; i < niveauline.length; i++) {
    board.create("implicitcurve", [
        (x, y) => x ** .5 * y ** .5 - niveauline[i],
           [0.25, 3], [0.5, 4] // Domain
    ], {
        strokeWidth: 2,
        strokeColor: JXG.palette.red,
        strokeOpacity: (1 + i) / niveauline.length,
        needsRegularUpdate: false
    });
}
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[alpha\_0](./ImplicitCurve.md#alpha_0)**  Angle α0 between two successive tangents: determines the smoothness of the curve. |
|  | **[delta\_0](./ImplicitCurve.md#delta_0)**  Allowed distance (in user units) of predictor point to curve. |
|  | **[h\_critical](./ImplicitCurve.md#h_critical)**  If h is below this threshold (in user units), we bail out of the tracing phase of that component. |
|  | **[h\_initial](./ImplicitCurve.md#h_initial)**  Initial step width (in user units). |
|  | **[h\_max](./ImplicitCurve.md#h_max)**  Maximum step width (in user units). |
|  | **[kappa\_0](./ImplicitCurve.md#kappa_0)**  Inverse of desired number of Newton steps. |
|  | **[loop\_detection](./ImplicitCurve.md#loop_detection)**  Use Gosper's loop detector. |
|  | **[loop\_dir](./ImplicitCurve.md#loop_dir)**  Minimum acos of angle to detect loop. |
|  | **[loop\_dist](./ImplicitCurve.md#loop_dist)**  Allowed distance (in user units multiplied by actual step width) to detect loop. |
|  | **[margin](./ImplicitCurve.md#margin)**  Defines the margin (in user coordinates) around the JSXGraph board in which the implicit curve is plotted. |
|  | **[max\_steps](./ImplicitCurve.md#max_steps)**  Maximum iterations for one component of the implicit curve. |
|  | **[qdt\_box](./ImplicitCurve.md#qdt_box)**  Half of the box size (in user units) to search for existing line segments in the quadtree. |
|  | **[resolution\_inner](./ImplicitCurve.md#resolution_inner)**  Vertical resolution (in pixel) to search for components of the implicit curve. |
|  | **[resolution\_outer](./ImplicitCurve.md#resolution_outer)**  Horizontal resolution: distance (in pixel) between vertical lines to search for components of the implicit curve. |
|  | **[tol\_0](./ImplicitCurve.md#tol_0)**  Tolerance to find starting points for the tracing phase of a component. |
|  | **[tol\_cusp](./ImplicitCurve.md#tol_cusp)**  Tolerance for cusp / bifurcation detection. |
|  | **[tol\_newton](./ImplicitCurve.md#tol_newton)**  Tolerance for the Newton steps. |
|  | **[tol\_progress](./ImplicitCurve.md#tol_progress)**  If two points are closer than this value, we bail out of the tracing phase for that component. |




### **alpha\_0**

Angle α0 between two successive tangents: determines the smoothness of
the curve.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.05


### **delta\_0**

Allowed distance (in user units) of predictor point to curve.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.05


### **h\_critical**

If h is below this threshold (in user units), we bail out
of the tracing phase of that component.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.001


### **h\_initial**

Initial step width (in user units).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.1


### **h\_max**

Maximum step width (in user units).
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.5


### **kappa\_0**

Inverse of desired number of Newton steps.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.2


### **loop\_detection**

Use Gosper's loop detector.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   true


### **loop\_dir**

Minimum acos of angle to detect loop.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.99


### **loop\_dist**

Allowed distance (in user units multiplied by actual step width) to detect loop.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.09


### **margin**

Defines the margin (in user coordinates) around the JSXGraph board in which the
implicit curve is plotted.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   1


### **max\_steps**

Maximum iterations for one component of the implicit curve.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   1024


### **qdt\_box**

Half of the box size (in user units) to search for existing line segments in the quadtree.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.2


### **resolution\_inner**

Vertical resolution (in pixel) to search for components of the implicit curve.
A small number increases the running time. For large number components may be missed.
Minimum value is 0.01.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   5


### **resolution\_outer**

Horizontal resolution: distance (in pixel) between vertical lines to search for components of the implicit curve.
A small number increases the running time. For large number components may be missed.
Minimum value is 0.01.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   5


### **tol\_0**

Tolerance to find starting points for the tracing phase of a component.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   JXG.Math.eps


### **tol\_cusp**

Tolerance for cusp / bifurcation detection.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.05


### **tol\_newton**

Tolerance for the Newton steps.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   1.0e-7


### **tol\_progress**

If two points are closer than this value, we bail out of the tracing phase for that
component.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   0.0001


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[domain](./ImplicitCurve.md#domain)**  Defines a domain for searching f(x,y)=0. |




### **domain**

Defines a domain for searching f(x,y)=0. Default is null, meaning
the bounding box of the board is used.
Using domain, visProp.margin is ignored.


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[dfx](./ImplicitCurve.md#dfx)**()  Partial derivative in the first variable of the left side of the equation *f(x,y)=0*. |
|  | **[dfy](./ImplicitCurve.md#dfy)**()  Partial derivative in the second variable of the left side of the equation *f(x,y)=0*. |
|  | **[f](./ImplicitCurve.md#f)**()  Function of two variables for the left side of the equation *f(x,y)=0*. |




### {Number} **dfx**()

Partial derivative in the first variable of
the left side of the equation *f(x,y)=0*.
If null, then numerical derivative is used.


#### Returns:

:   {Number}


### {Number} **dfy**()

Partial derivative in the second variable of
the left side of the equation *f(x,y)=0*.
If null, then numerical derivative is used.


#### Returns:

:   {Number}


### {Number} **f**()

Function of two variables for the left side of the equation *f(x,y)=0*.


#### Returns:

:   {Number}
