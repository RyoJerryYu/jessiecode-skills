

# Angle



## 描述

Angle sector defined by three points or two lines. Visually it is just a [Sector](./Sector.md) element with a radius not defined by the parent elements but by an attribute radius. As opposed to the sector, an angle has two angle points and no radius point. Sector is displayed if type=="sector". If type=="square", instead of a sector a parallelogram is displayed. In case of type=="auto", a square is displayed if the angle is near orthogonal. The precision to decide if an angle is orthogonal is determined by the attribute [Angle#orthoSensitivity](./Angle.md#orthoSensitivity).

If no name is provided the angle label is automatically set to a lower greek letter. If no label should be displayed use the attribute withLabel:false or set the name attribute to the empty string.   
  
*Defined in:*  [sector.js](./src/src_element_sector.js.md).   
Extends [Sector](./Sector.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.Curve](./JXG.Curve.md)**  
      ↳ **[Sector](./Sector.md)**  
            ↳ **Angle**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[Angle](./Angle.md#constructor)** |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "angle".  
  

Possible parent array combinations are:

{[JXG.Point](../symbols/JXG.Point.html)} **p1** {[JXG.Point](../symbols/JXG.Point.html)} **p2** {[JXG.Point](./JXG.Point.md)} **p1**
:   An angle is always drawn counterclockwise from p1 to p3 around p2. Second possibility of input parameters are:
  
  
:   line2, coords1 or direction1, coords2 or direction2, radius The angle is defined by two lines. The two legs which define the angle are given by two coordinate arrays. The points given by these coordinate arrays are projected initially (i.e. only once) onto the two lines. The other possibility is to supply directions (+/- 1).


### Throws

- Throws: {Error} If the element cannot be constructed with the given parent objects an exception is thrown.
First possibility of input parameters are:


### 示例

```javascript
// Create an angle out of three free points
var p1 = board.create('point', [5.0, 3.0]),
    p2 = board.create('point', [1.0, 0.5]),
    p3 = board.create('point', [1.5, 5.0]),

    a = board.create('angle', [p1, p2, p3]),
    t = board.create('text', [4, 4, function() { return JXG.toFixed(a.Value(), 2); }]);
```

```javascript
// Create an angle out of two lines and two directions
var p1 = board.create('point', [-1, 4]),
 p2 = board.create('point', [4, 1]),
 q1 = board.create('point', [-2, -3]),
 q2 = board.create('point', [4,3]),

 li1 = board.create('line', [p1,p2], {strokeColor:'black', lastArrow:true}),
 li2 = board.create('line', [q1,q2], {lastArrow:true}),

 a1 = board.create('angle', [li1, li2, [5.5, 0], [4, 3]], { radius:1 }),
 a2 = board.create('angle', [li1, li2, 1, -1], { radius:2 });
```

```javascript
// Display the angle value instead of the name
var p1 = board.create('point', [0,2]);
var p2 = board.create('point', [0,0]);
var p3 = board.create('point', [-2,0.2]);

var a = board.create('angle', [p1, p2, p3], {
	 radius: 1,
  name: function() {
  	return JXG.Math.Geometry.trueAngle(p1, p2, p3).toFixed(1) + '°';
  }});
```

```javascript
// Apply a transformation to an angle.
var t = board.create('transform', [2, 1.5], {type: 'scale'});
var an1 = board.create('angle', [[-4,3.9], [-3, 4], [-3, 3]]);
var an2 = board.create('curve', [an1, t]);
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[arc](./Angle.md#arc)**  Attributes for sub-element arc. |
|  | **[dot](./Angle.md#dot)**  Attributes of the dot point marking right angles. |
|  | **[orthoSensitivity](./Angle.md#orthoSensitivity)**  Sensitivity (in degrees) to declare an angle as right angle. |
|  | **[orthoType](./Angle.md#orthoType)**  Display type of the angle field in case of a right angle. |
|  | **[pointsquare](./Angle.md#pointsquare)** |
|  | **[radius](./Angle.md#radius)**  Radius of the sector, displaying the angle. |
|  | **[radiuspoint](./Angle.md#radiuspoint)** |
|  | **[type](./Angle.md#type)**  Display type of the angle field. |




### {[Arc](./Arc.md)} **arc**

Attributes for sub-element arc. In general, the arc will run through the first point and
thus will not have the same radius as the angle sector.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   '{visible:false}'


### {Object} **dot**

Attributes of the dot point marking right angles.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   {face: 'o', size: 2}


### {Number} **orthoSensitivity**

Sensitivity (in degrees) to declare an angle as right angle.
If the angle measure is inside this distance from a rigth angle, the orthoType
of the angle is used for display.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Angle#orthoType](./Angle.md#orthoType)


#### Default Value:

:   1.0


### {String} **orthoType**

Display type of the angle field in case of a right angle. Possible values are
'sector' or 'sectordot' or 'square' or 'none'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### See:

:   [Angle#orthoSensitivity](./Angle.md#orthoSensitivity)


#### Default Value:

:   square


### {Object} **pointsquare**

*Defined in:*  [options.js](./src/src_options.js.md).


### **radius**

Radius of the sector, displaying the angle.
The radius can be given as number (in user coordinates)
or as string 'auto'. In the latter case, the angle
is set to an value between 20 and 50 px.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'auto'


### {Object} **radiuspoint**

*Defined in:*  [options.js](./src/src_options.js.md).


### {String} **type**

Display type of the angle field. Possible values are
'sector' or 'sectordot' or 'square' or 'none'.
  
*Defined in:*  [options.js](./src/src_options.js.md).


#### Default Value:

:   'sector'


## 字段

Field Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[point](./Angle.md#point)**  The point defining the radius of the angle element. |




### {[JXG.Point](./JXG.Point.md)} **point**

The point defining the radius of the angle element.
Alias for Sector#radiuspoint.


## 方法

Method Summary

| Method Attributes | Method Name and Description |
| --- | --- |
|  | **[free](./Angle.md#free)**()  Frees an angle from a prescribed value. |
|  | **[setAngle](./Angle.md#setAngle)**(val)  Set an angle to a prescribed value given in radians. |
|  | **[Value](./Angle.md#Value)**(unit)  Returns the value of the angle. |




### {Object} **free**()

Frees an angle from a prescribed value. This is only relevant if the angle size has been set by
"setAngle()" previously. The anglepoint is set to a free point.


#### Returns:

:   {Object} Pointer to the angle element..


#### See:

:   [Angle#setAngle](./Angle.md#setAngle)


### {Object} **setAngle**(val)

Set an angle to a prescribed value given in radians.
This is only possible if the third point of the angle, i.e.
the anglepoint is a free point.
Removing the constraint again is done by calling "angle.free()".
Changing the angle requires to call the method "free()":

```
angle.setAngle(Math.PI / 6);
// ...
angle.free().setAngle(Math.PI / 4);
```


#### Parameters:

:   Number or Function which returns the size of the angle in Radians


#### Returns:

:   {Object} Pointer to the angle element..


#### See:

:   [Angle#free](./Angle.md#free)


#### 示例

```javascript
var p1, p2, p3, c, a, s;

p1 = board.create('point',[0,0]);
p2 = board.create('point',[5,0]);
p3 = board.create('point',[0,5]);

c1 = board.create('circle',[p1, p2]);

a = board.create('angle',[p2, p1, p3], {radius:3});

a.setAngle(function() {
    return Math.PI / 3;
});
board.update();
```

```javascript
var p1, p2, p3, c, a, s;

p1 = board.create('point',[0,0]);
p2 = board.create('point',[5,0]);
p3 = board.create('point',[0,5]);

c1 = board.create('circle',[p1, p2]);

a = board.create('angle',[p2, p1, p3], {radius:3});
s = board.create('slider',[[-2,1], [2,1], [0, Math.PI*0.5, 2*Math.PI]]);

a.setAngle(function() {
    return s.Value();
});
board.update();
```



### {Number} **Value**(unit)

Returns the value of the angle.


#### Parameters:

:   Unit of the returned values. Possible units are

    * 'radians' (default): angle value in radians
    * 'degrees': angle value in degrees
    * 'semicircle': angle value in radians as a multiple of π, e.g. if the angle is 1.5π, 1.5 will be returned.
    * 'circle': angle value in radians as a multiple of 2π
    * 'length': length of the arc line of the angle

    It is sufficient to supply the first three characters of the unit, e.g. 'len'.


#### Returns:

:   {Number} angle value in various units.


#### See:

:   [Sector#L](./Sector.md#L)
:   [Arc#Value](./Arc.md#Value)


#### 示例

```javascript
var A, B, C, ang,
    r = 0.5;
A = board.create("point", [3, 0]);
B = board.create("point", [0, 0]);
C = board.create("point", [2, 2]);
ang = board.create("angle", [A, B, C], {radius: r});

console.log(ang.Value());
// Output Math.PI * 0.25

console.log(ang.Value('radian'));
// Output Math.PI * 0.25

console.log(ang.Value('degree');
// Output 45

console.log(ang.Value('semicircle'));
// Output 0.25

console.log(ang.Value('circle'));
// Output 0.125

console.log(ang.Value('length'));
// Output r * Math.PI * 0.25

console.log(ang.L());
// Output r * Math.PI * 0.25
```
