

# View3D



## 描述

A View3D element provides the container and the methods to create and display 3D elements.   
  
*Defined in:*  [view3d.js](./src/src_3d_view3d.js.md).   
Extends [JXG.View3D](./JXG.View3D.md).




## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**  
   ↳ **[JXG.View3D](./JXG.View3D.md)**  
         ↳ **View3D**




## 构造函数

Element Summary

| Constructor Attributes | Constructor Name and Description |
| --- | --- |
|  | **[View3D](./View3D.md#constructor)**  A View3D element provides the container and the methods to create and display 3D elements. |




### 说明

This element has no direct constructor. To create an instance of this element you have to call [JXG.Board#create](./JXG.Board.md#create) with type "view3d".  
  

Possible parent array combinations are:

{Array} **lower** {Array} **dim** {Array} **cube**
:   Here, lower is an array of the form [x, y] and dim is an array of the form [w, h]. The arrays [x, y] and [w, h] define the 2D frame into which the 3D cube is (roughly) projected. If the view's azimuth=0 and elevation=0, the 3D view will cover a rectangle with lower left corner [x,y] and side lengths [w, h] of the board. The array 'cube' is of the form [[x1, x2], [y1, y2], [z1, z2]] which determines the coordinate ranges of the 3D cube.


### Throws

- Throws: {Exception} If the element cannot be constructed with the given parent objects an exception is thrown.


### 示例

```javascript
var bound = [-4, 6];
    var view = board.create('view3d',
        [[-4, -3], [8, 8],
        [bound, bound, bound]],
        {
            projection: 'parallel',
            trackball: {enabled:true},
        });

    var curve = view.create('curve3d', [
        (t) => (2 + Math.cos(3 * t)) * Math.cos(2 * t),
        (t) => (2 + Math.cos(3 * t)) * Math.sin(2 * t),
        (t) => Math.sin(3 * t),
        [-Math.PI, Math.PI]
    ], { strokeWidth: 4 });
```

```javascript
var bound = [-4, 6];
    var view = board.create('view3d',
        [[-4, -3], [8, 8],
        [bound, bound, bound]],
        {
            projection: 'central',
            trackball: {enabled:true},

            xPlaneRear: { visible: false },
            yPlaneRear: { visible: false }

        });

    var curve = view.create('curve3d', [
        (t) => (2 + Math.cos(3 * t)) * Math.cos(2 * t),
        (t) => (2 + Math.cos(3 * t)) * Math.sin(2 * t),
        (t) => Math.sin(3 * t),
        [-Math.PI, Math.PI]
    ], { strokeWidth: 4 });
```

```javascript
var bound = [-4, 6];
    var view = board.create('view3d',
        [[-4, -3], [8, 8],
        [bound, bound, bound]],
        {
            projection: 'central',
            trackball: {enabled:true},

            // Main axes
            axesPosition: 'border',

            // Axes at the border
            xAxisBorder: { ticks3d: { ticksDistance: 2} },
            yAxisBorder: { ticks3d: { ticksDistance: 2} },
            zAxisBorder: { ticks3d: { ticksDistance: 2} },

            // No axes on planes
            xPlaneRearYAxis: {visible: false},
            xPlaneRearZAxis: {visible: false},
            yPlaneRearXAxis: {visible: false},
            yPlaneRearZAxis: {visible: false},
            zPlaneRearXAxis: {visible: false},
            zPlaneRearYAxis: {visible: false}
        });

    var curve = view.create('curve3d', [
        (t) => (2 + Math.cos(3 * t)) * Math.cos(2 * t),
        (t) => (2 + Math.cos(3 * t)) * Math.sin(2 * t),
        (t) => Math.sin(3 * t),
        [-Math.PI, Math.PI]
    ], { strokeWidth: 4 });
```

```javascript
var bound = [-4, 6];
    var view = board.create('view3d',
        [[-4, -3], [8, 8],
        [bound, bound, bound]],
        {
            projection: 'central',
            trackball: {enabled:true},

            axesPosition: 'none'
        });

    var curve = view.create('curve3d', [
        (t) => (2 + Math.cos(3 * t)) * Math.cos(2 * t),
        (t) => (2 + Math.cos(3 * t)) * Math.sin(2 * t),
        (t) => Math.sin(3 * t),
        [-Math.PI, Math.PI]
    ], { strokeWidth: 4 });
```

```javascript
var bound = [-4, 6];
    var view = board.create('view3d',
        [[-4, -3], [8, 8],
        [bound, bound, bound]],
        {
            projection: 'central',
            trackball: {enabled:true},

            // Main axes
            axesPosition: 'border',

            // Axes at the border
            xAxisBorder: { ticks3d: { ticksDistance: 2} },
            yAxisBorder: { ticks3d: { ticksDistance: 2} },
            zAxisBorder: { ticks3d: { ticksDistance: 2} },

            xPlaneRear: {
                fillColor: '#fff',
                mesh3d: {visible: false}
            },
            yPlaneRear: {
                fillColor: '#fff',
                mesh3d: {visible: false}
            },
            zPlaneRear: {
                fillColor: '#fff',
                mesh3d: {visible: false}
            },
            xPlaneFront: {
                visible: true,
                fillColor: '#fff',
                mesh3d: {visible: false}
            },
            yPlaneFront: {
                visible: true,
                fillColor: '#fff',
                mesh3d: {visible: false}
            },
            zPlaneFront: {
                visible: true,
                fillColor: '#fff',
                mesh3d: {visible: false}
            },

            // No axes on planes
            xPlaneRearYAxis: {visible: false},
            xPlaneRearZAxis: {visible: false},
            yPlaneRearXAxis: {visible: false},
            yPlaneRearZAxis: {visible: false},
            zPlaneRearXAxis: {visible: false},
            zPlaneRearYAxis: {visible: false},
            xPlaneFrontYAxis: {visible: false},
            xPlaneFrontZAxis: {visible: false},
            yPlaneFrontXAxis: {visible: false},
            yPlaneFrontZAxis: {visible: false},
            zPlaneFrontXAxis: {visible: false},
            zPlaneFrontYAxis: {visible: false}

        });

    var curve = view.create('curve3d', [
        (t) => (2 + Math.cos(3 * t)) * Math.cos(2 * t),
        (t) => (2 + Math.cos(3 * t)) * Math.sin(2 * t),
        (t) => Math.sin(3 * t),
        [-Math.PI, Math.PI]
    ], { strokeWidth: 4 });
```

```javascript
var bound = [-5, 5];
 var view = board.create('view3d',
     [[-6, -3],
      [8, 8],
      [bound, bound, bound]],
     {
         // Main axes
         axesPosition: 'center',
         xAxis: { strokeColor: 'blue', strokeWidth: 3},

         // Planes
         xPlaneRear: { fillColor: 'yellow',  mesh3d: {visible: false}},
         yPlaneFront: { visible: true, fillColor: 'blue'},

         // Axes on planes
         xPlaneRearYAxis: {strokeColor: 'red'},
         xPlaneRearZAxis: {strokeColor: 'red'},

         yPlaneFrontXAxis: {strokeColor: 'blue'},
         yPlaneFrontZAxis: {strokeColor: 'blue'},

         zPlaneFrontXAxis: {visible: false},
         zPlaneFrontYAxis: {visible: false}
     });
```

```javascript
var bound = [-5, 5];
var view = board.create('view3d',
    [[-6, -3], [8, 8],
    [bound, bound, bound]],
    {
        projection: 'central',
        az: {
            slider: {
                visible: true,
                point1: {
                    pos: [5, -4]
                },
                point2: {
                    pos: [5, 4]
                },
                label: {anchorX: 'middle'}
            }
        },
        el: {
            slider: {
                visible: true,
                point1: {
                    pos: [6, -5]
                },
                point2: {
                    pos: [6, 3]
                },
                label: {anchorX: 'middle'}
            }
        },
        bank: {
            slider: {
                visible: true,
                point1: {
                    pos: [7, -6]
                },
                point2: {
                    pos: [7, 2]
                },
                label: {anchorX: 'middle'}
            }
        }
    });
```



## 属性

Attributes Summary

| Field Attributes | Field Name and Description |
| --- | --- |
|  | **[axesPosition](./View3D.md#axesPosition)**  Position of the main axes in a View3D element. |
|  | **[az](./View3D.md#az)**  Specify the user handling of the azimuth. |
|  | **[bank](./View3D.md#bank)**  Specify the user handling of the bank angle. |
|  | **[depthOrder](./View3D.md#depthOrder)**  When this attribute is enabled, elements closer to the screen are drawn over elements further from the screen within the 3D layer. |
|  | **[el](./View3D.md#el)**  Specify the user handling of the elevation. |
|  | **[projection](./View3D.md#projection)**  Choose the projection type to be used: `parallel` or `central`. |
|  | **[trackball](./View3D.md#trackball)**  Enable user handling by a virtual trackball that allows to move the 3D scene with 3 degrees of freedom. |
|  | **[values](./View3D.md#values)**  Fixed values for the view, which can be changed using keyboard keys `picture-up` and `picture-down`. |
|  | **[verticalDrag](./View3D.md#verticalDrag)**  Allow vertical dragging of objects, i.e. |
|  | **[xAxis](./View3D.md#xAxis)**  Attributes of the centered 3D x-axis. |
|  | **[xAxisBorder](./View3D.md#xAxisBorder)**  Attributes of the 3D x-axis at the border. |
|  | **[xPlaneFront](./View3D.md#xPlaneFront)**  Attributes of the 3D plane orthogonal to the x-axis at the "front" of the cube. |
|  | **[xPlaneFrontYAxis](./View3D.md#xPlaneFrontYAxis)**  Attributes of the 3D y-axis on the 3D plane orthogonal to the x-axis at the "front" of the cube. |
|  | **[xPlaneFrontZAxis](./View3D.md#xPlaneFrontZAxis)**  Attributes of the 3D z-axis on the 3D plane orthogonal to the x-axis at the "front" of the cube. |
|  | **[xPlaneRear](./View3D.md#xPlaneRear)**  Attributes of the 3D plane orthogonal to the x-axis at the "rear" of the cube. |
|  | **[xPlaneRearYAxis](./View3D.md#xPlaneRearYAxis)**  Attributes of the 3D y-axis on the 3D plane orthogonal to the x-axis at the "rear" of the cube. |
|  | **[xPlaneRearZAxis](./View3D.md#xPlaneRearZAxis)**  Attributes of the 3D z-axis on the 3D plane orthogonal to the x-axis at the "rear" of the cube. |
|  | **[yAxis](./View3D.md#yAxis)**  Attributes of the centered 3D y-axis. |
|  | **[yAxisBorder](./View3D.md#yAxisBorder)**  Attributes of the 3D y-axis at the border. |
|  | **[yPlaneFront](./View3D.md#yPlaneFront)**  Attributes of the 3D plane orthogonal to the y-axis at the "front" of the cube. |
|  | **[yPlaneFrontXAxis](./View3D.md#yPlaneFrontXAxis)**  Attributes of the 3D x-axis on the 3D plane orthogonal to the y-axis at the "front" of the cube. |
|  | **[yPlaneFrontZAxis](./View3D.md#yPlaneFrontZAxis)**  Attributes of the 3D z-axis on the 3D plane orthogonal to the y-axis at the "front" of the cube. |
|  | **[yPlaneRear](./View3D.md#yPlaneRear)**  Attributes of the 3D plane orthogonal to the y-axis at the "rear" of the cube. |
|  | **[yPlaneRearXAxis](./View3D.md#yPlaneRearXAxis)**  Attributes of the 3D x-axis on the 3D plane orthogonal to the y-axis at the "rear" of the cube. |
|  | **[yPlaneRearZAxis](./View3D.md#yPlaneRearZAxis)**  Attributes of the 3D z-axis on the 3D plane orthogonal to the y-axis at the "rear" of the cube. |
|  | **[zAxis](./View3D.md#zAxis)**  Attributes of the centered 3D z-axis. |
|  | **[zAxisBorder](./View3D.md#zAxisBorder)**  Attributes of the 3D z-axis at the border. |
|  | **[zPlaneFront](./View3D.md#zPlaneFront)**  Attributes of the 3D plane orthogonal to the z-axis at the "front" of the cube. |
|  | **[zPlaneFrontXAxis](./View3D.md#zPlaneFrontXAxis)**  Attributes of the 3D x-axis on the 3D plane orthogonal to the z-axis at the "front" of the cube. |
|  | **[zPlaneFrontYAxis](./View3D.md#zPlaneFrontYAxis)**  Attributes of the 3D y-axis on the 3D plane orthogonal to the z-axis at the "front" of the cube. |
|  | **[zPlaneRear](./View3D.md#zPlaneRear)**  Attributes of the 3D plane orthogonal to the z-axis at the "rear" of the cube. |
|  | **[zPlaneRearXAxis](./View3D.md#zPlaneRearXAxis)**  Attributes of the 3D x-axis on the 3D plane orthogonal to the z-axis at the "rear" of the cube. |
|  | **[zPlaneRearYAxis](./View3D.md#zPlaneRearYAxis)**  Attributes of the 3D y-axis on the 3D plane orthogonal to the z-axis at the "rear" of the cube. |




### {String} **axesPosition**

Position of the main axes in a View3D element. Possible values are
'center', 'border' or 'none'. This attribute is immutable, i.e.
can not be changed during the lifetime of the construction.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   'center'


### {Object} **az**

Specify the user handling of the azimuth.

* pointer sub-attributes:
  + enabled: Boolean that specifies whether pointer navigation is allowed by azimuth.
  + speed: Number indicating how many passes the range of the az\_slider makes when the cursor crosses the entire board once in the horizontal direction.
  + outside: Boolean that specifies whether the pointer navigation is continued when the cursor leaves the board.
  + button: Which button of the pointer should be used? ('-1' (=no button), '0' or '2')
  + key: Should an additional key be pressed? ('none', 'shift' or 'ctrl')
* keyboard sub-attributes:
  + enabled: Boolean that specifies whether the keyboard (left/right arrow keys) can be used to navigate the board.
  + step: Size of the step per keystroke.
  + key: Should an additional key be pressed? ('none', 'shift' or 'ctrl')
* continuous: Boolean that specifies whether the az\_slider starts again from the beginning when its end is reached.
* slider attributes of the az\_slider ([Slider](./Slider.md)) with additional
  + min: Minimum value.
  + max: Maximum value.
  + start: Start value.'min' and 'max' are used only if trackball is not enabled.
  Additionally, the attributes 'slider.point1.pos' and 'slider.point2.pos' control the position of the slider. Possible
  values are 'auto' or an array [x, y] of length 2 for the position in user coordinates (or a function returning such an array).

  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    {
         pointer: {enabled: true, speed: 1, outside: true, button: -1, key: 'none'},
         keyboard: {enabled: true, step: 10, key: 'ctrl'},
         continuous: true,
         slider: {
             visible: true,
             style: 6,
             point1: {
                 pos: 'auto',
                 frozen: false
             },
             point2: {
                 pos: 'auto',
                 frozen: false
             },
             min: 0,
             max: 2 * Math.PI,
             start: 1.0
         },
    }
    ```


### {Object} **bank**

Specify the user handling of the bank angle.

* pointer sub-attributes:
  + enabled: Boolean that specifies whether pointer navigation is allowed by elevation.
  + speed: Number indicating how many passes the range of the el\_slider makes when the cursor crosses the entire board once in the horizontal direction.
  + outside: Boolean that specifies whether the pointer navigation is continued when the cursor leaves the board.
  + button: Which button of the pointer should be used? ('-1' (=no button), '0' or '2')
  + key: Should an additional key be pressed? ('none', 'shift' or 'ctrl')
* keyboard sub-attributes:
  + enabled: Boolean that specifies whether the keyboard ('<', '>' keys) can be used to navigate the board.
  + step: Size of the step per keystroke.
  + key: Should an additional key be pressed? ('none', 'shift' or 'ctrl')
* continuous: Boolean that specifies whether the el\_slider starts again from the beginning when its end is reached.
* slider attributes of the el\_slider ([Slider](./Slider.md)) with additional
  + min: Minimum value.
  + max: Maximum value.
  + start: Start value.'min' and 'max' are used only if trackball is not enabled.
  Additionally, the attributes 'slider.point1.pos' and 'slider.point2.pos' control the position of the slider. Possible
  values are 'auto' or an array [x, y] of length 2 for the position in user coordinates (or a function returning such an array).

  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    {
         pointer: {enabled: true, speed: 1, outside: true, button: -1, key: 'none'},
         keyboard: {enabled: true, step: 10, key: 'ctrl'},
         continuous: true,
         slider: {
             visible: true,
             style: 6,
             point1: {
                 pos: 'auto',
                 frozen: false
             },
             point2: {
                 pos: 'auto',
                 frozen: false
             },
             min: 0,
             max: 2 * Math.PI,
             start: 0.3
         },
    }

    ```
    							
    ```
    ```


### {Object} **depthOrder**

When this attribute is enabled, elements closer to the screen are drawn
over elements further from the screen within the 3D layer. This affects
all elements which are in one of the layer specified in the sub-attribute 'layers'.

For each layer this depth ordering is done independently.
Sub-attributes:

* enabled: false/true
* layers: [12, 13]

  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    {
      enabled: false,
      layers: [12, 13]
    }
    ```


### {Object} **el**

Specify the user handling of the elevation.

* pointer sub-attributes:
  + enabled: Boolean that specifies whether pointer navigation is allowed by elevation.
  + speed: Number indicating how many passes the range of the el\_slider makes when the cursor crosses the entire board once in the horizontal direction.
  + outside: Boolean that specifies whether the pointer navigation is continued when the cursor leaves the board.
  + button: Which button of the pointer should be used? ('-1' (=no button), '0' or '2')
  + key: Should an additional key be pressed? ('none', 'shift' or 'ctrl')
* keyboard sub-attributes:
  + enabled: Boolean that specifies whether the keyboard (up/down arrow keys) can be used to navigate the board.
  + step: Size of the step per keystroke.
  + key: Should an additional key be pressed? ('none', 'shift' or 'ctrl')
* continuous: Boolean that specifies whether the el\_slider starts again from the beginning when its end is reached.
* slider attributes of the el\_slider ([Slider](./Slider.md)) with additional
  + min: Minimum value.
  + max: Maximum value.
  + start: Start value.'min' and 'max' are used only if trackball is not enabled.
  Additionally, the attributes 'slider.point1.pos' and 'slider.point2.pos' control the position of the slider. Possible
  values are 'auto' or an array [x, y] of length 2 for the position in user coordinates (or a function returning such an array).

  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    {
         pointer: {enabled: true, speed: 1, outside: true, button: -1, key: 'none'},
         keyboard: {enabled: true, step: 10, key: 'ctrl'},
         continuous: true,
         slider: {
             visible: true,
             style: 6,
             point1: {
                 pos: 'auto',
                 frozen: false
             },
             point2: {
                 pos: 'auto',
                 frozen: false
             },
             min: 0,
             max: 2 * Math.PI,
             start: 0.3
         },
    }

    ```
    							
    ```
    ```


### {String} **projection**

Choose the projection type to be used: `parallel` or `central`.

* `parallel` is parallel projection, also called orthographic projection
* `central` is central projection, also called perspective projection

  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   'parallel'


### {Object} **trackball**

Enable user handling by a virtual trackball that allows to move the 3D scene
with 3 degrees of freedom. If not enabled, direct user dragging (i.e. in the JSXGraph board, not manipulating the sliders) will only have
two degrees of freedom. This means, the z-axis will always be projected to a vertical 2D line.

Sub-attributes:

* enabled: Boolean that specifies whether pointer navigation is allowed by elevation.
* outside: Boolean that specifies whether the pointer navigation is continued when the cursor leaves the board.
* button: Which button of the pointer should be used? ('-1' (=no button), '0' or '2')
* key: Should an additional key be pressed? ('none', 'shift' or 'ctrl')

  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   ```
    {
      enabled: false,
      outside: true,
      button: -1,
      key: 'none'
    }
    ```


### {Array} **values**

Fixed values for the view, which can be changed using keyboard keys `picture-up` and `picture-down`.
Array of the form: [[el0, az0, r0], [el1, az1, r1, ...[eln, azn, rn]]
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   {[[0, 1.57], [0.78, 0.62], [0, 0], [5.49, 0.62], [4.71, 0], [3.93, 0.62], [3.14, 0], [2.36, 0.62], [1.57, 1.57]]}


### {Object} **verticalDrag**

Allow vertical dragging of objects, i.e. in direction of the z-axis.
Subobjects are

* enabled: true
* key: 'shift'

Possible values for attribute *key*: 'shift' or 'ctrl'.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### Default Value:

:   {enabled: true, key: 'shift'}


### {[Line3D](./Line3D.md)} **xAxis**

Attributes of the centered 3D x-axis.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### See:

:   [View3D#axesPosition](./View3D.md#axesPosition)


### {[Line3D](./Line3D.md)} **xAxisBorder**

Attributes of the 3D x-axis at the border.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### See:

:   [View3D#axesPosition](./View3D.md#axesPosition)


#### Default Value:

:   ```
    {
      name: 'x',
      withLabel: false,
      label: {
          position: '50% left',
          offset: [30, 0],
          fontsize: 15
      },
      strokeWidth: 1,
      lastArrow: false,
      ticks3d: {
          label: {
              anchorX: 'middle',
              anchorY: 'middle'
          }
      }
    }
    ```


### {[Plane3D](./Plane3D.md)} **xPlaneFront**

Attributes of the 3D plane orthogonal to the x-axis at the "front" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **xPlaneFrontYAxis**

Attributes of the 3D y-axis on the 3D plane orthogonal to the x-axis at the "front" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **xPlaneFrontZAxis**

Attributes of the 3D z-axis on the 3D plane orthogonal to the x-axis at the "front" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **xPlaneRear**

Attributes of the 3D plane orthogonal to the x-axis at the "rear" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **xPlaneRearYAxis**

Attributes of the 3D y-axis on the 3D plane orthogonal to the x-axis at the "rear" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **xPlaneRearZAxis**

Attributes of the 3D z-axis on the 3D plane orthogonal to the x-axis at the "rear" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Line3D](./Line3D.md)} **yAxis**

Attributes of the centered 3D y-axis.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### See:

:   [View3D#axesPosition](./View3D.md#axesPosition)


### {[Line3D](./Line3D.md)} **yAxisBorder**

Attributes of the 3D y-axis at the border.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### See:

:   [View3D#axesPosition](./View3D.md#axesPosition)


#### Default Value:

:   ```
    {
      name: 'x',
      withLabel: false,
      label: {
          position: '50% right',
          offset: [0, -30],
          fontsize: 15
      },
      strokeWidth: 1,
      lastArrow: false,
      ticks3d: {
          label: {
              anchorX: 'middle',
          }
      }
    }
    ```


### {[Plane3D](./Plane3D.md)} **yPlaneFront**

Attributes of the 3D plane orthogonal to the y-axis at the "front" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **yPlaneFrontXAxis**

Attributes of the 3D x-axis on the 3D plane orthogonal to the y-axis at the "front" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **yPlaneFrontZAxis**

Attributes of the 3D z-axis on the 3D plane orthogonal to the y-axis at the "front" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **yPlaneRear**

Attributes of the 3D plane orthogonal to the y-axis at the "rear" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **yPlaneRearXAxis**

Attributes of the 3D x-axis on the 3D plane orthogonal to the y-axis at the "rear" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **yPlaneRearZAxis**

Attributes of the 3D z-axis on the 3D plane orthogonal to the y-axis at the "rear" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Line3D](./Line3D.md)} **zAxis**

Attributes of the centered 3D z-axis.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### See:

:   [View3D#axesPosition](./View3D.md#axesPosition)


### {[Line3D](./Line3D.md)} **zAxisBorder**

Attributes of the 3D z-axis at the border.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


#### See:

:   [View3D#axesPosition](./View3D.md#axesPosition)


#### Default Value:

:   ```
    {
      name: 'z',
      withLabel: false,
      label: {
          position: '50% right',
          offset: [30, 0],
          fontsize: 15
      },
      strokeWidth: 1,
      lastArrow: false,
      ticks3d: {
          label: {
              anchorX: 'middle',
              anchorY: 'middle'
          }
      }
    }
    ```


### {[Plane3D](./Plane3D.md)} **zPlaneFront**

Attributes of the 3D plane orthogonal to the z-axis at the "front" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **zPlaneFrontXAxis**

Attributes of the 3D x-axis on the 3D plane orthogonal to the z-axis at the "front" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **zPlaneFrontYAxis**

Attributes of the 3D y-axis on the 3D plane orthogonal to the z-axis at the "front" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **zPlaneRear**

Attributes of the 3D plane orthogonal to the z-axis at the "rear" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **zPlaneRearXAxis**

Attributes of the 3D x-axis on the 3D plane orthogonal to the z-axis at the "rear" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).


### {[Plane3D](./Plane3D.md)} **zPlaneRearYAxis**

Attributes of the 3D y-axis on the 3D plane orthogonal to the z-axis at the "rear" of the cube.
  
*Defined in:*  [options3d.js](./src/src_options3d.js.md).
