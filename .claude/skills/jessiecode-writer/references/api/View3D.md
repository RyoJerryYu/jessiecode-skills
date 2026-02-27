# View3D 3D 视图

<!-- USAGE_FREQUENCY: advanced -->

## 描述

View3D 元素提供容器和用于创建、显示 3D 元素的方法。它是所有 3D 几何元素的容器，定义了 3D 空间的投影方式、坐标范围和显示属性。

## JessieCode 语法

```js
// 创建 3D 视图
view = board.create('view3d', [lower, dim, cube], options);

// lower: [x, y] 左下角坐标
// dim: [w, h] 宽度和高度
// cube: [[x1, x2], [y1, y2], [z1, z2]] 3D 坐标范围
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| lower | Array | 形式为 [x, y] 的数组，定义 2D 框架的左下角 |
| dim | Array | 形式为 [w, h] 的数组，定义 2D 框架的宽度和高度 |
| cube | Array | 形式为 [[x1, x2], [y1, y2], [z1, z2]] 的数组，确定 3D 立方体的坐标范围 |

**参数说明**：
- `lower` 和 `dim` 定义 3D 立方体投影的 2D 框架
- 当视图的 azimuth=0 和 elevation=0 时，3D 视图将覆盖板上一个矩形区域
- `cube` 确定 3D 空间的坐标范围

## 属性

### 主要属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `projection` | String | 'parallel' | 投影类型：'parallel'（平行投影）或 'central'（透视投影） |
| `axesPosition` | String | 'center' | 主轴位置：'center'、'border' 或 'none' |
| `trackball` | Object | - | 启用虚拟轨迹球用户操作 |
| `depthOrder` | Object | - | 深度排序设置 |
| `verticalDrag` | Object | - | 允许垂直拖拽 |
| `az` | Object | - | 方位角用户操作设置 |
| `el` | Object | - | 仰角用户操作设置 |
| `bank` | Object | - | 倾斜角用户操作设置 |
| `values` | Array | - | 可通过键盘切换的预设视图 |

### projection - 投影类型

| 值 | 描述 |
|------|------|
| `parallel` | 平行投影（正交投影） |
| `central` | 透视投影（中心投影） |

### trackball - 轨迹球

| 子属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `enabled` | Boolean | false | 是否启用轨迹球 |
| `outside` | Boolean | true | 光标离开画布后是否继续 |
| `button` | Number | -1 | 使用哪个鼠标按钮（-1/0/2） |
| `key` | String | 'none' | 需要按住的键（'none'/'shift'/'ctrl'） |

### depthOrder - 深度排序

| 子属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `enabled` | Boolean | false | 是否启用深度排序 |
| `layers` | Array | [12, 13] | 要应用深度排序的图层 |

### axesPosition - 坐标轴位置

| 值 | 描述 |
|------|------|
| `center` | 坐标轴在中心（默认） |
| `border` | 坐标轴在边框 |
| `none` | 不显示坐标轴 |

### az/el/bank - 角度控制

每个属性（az=方位角，el=仰角，bank=倾斜角）有以下子属性：

| 子属性 | 类型 | 描述 |
|------|------|------|
| `pointer.enabled` | Boolean | 是否允许指针操作 |
| `pointer.speed` | Number | 指针移动速度 |
| `pointer.outside` | Boolean | 光标离开画布后是否继续 |
| `pointer.button` | Number | 鼠标按钮 |
| `pointer.key` | String | 额外按键 |
| `keyboard.enabled` | Boolean | 是否允许键盘操作 |
| `keyboard.step` | Number | 每次按键的步进大小 |
| `keyboard.key` | String | 额外按键 |
| `continuous` | Boolean | 是否循环 |
| `slider.visible` | Boolean | 是否显示滑块 |
| `slider.point1.pos` | Array/String | 滑块起点位置 |
| `slider.point2.pos` | Array/String | 滑块终点位置 |

### 平面和坐标轴属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `xAxis` | Object | 中心 3D x 轴属性 |
| `xAxisBorder` | Object | 边框 3D x 轴属性 |
| `yAxis` | Object | 中心 3D y 轴属性 |
| `yAxisBorder` | Object | 边框 3D y 轴属性 |
| `zAxis` | Object | 中心 3D z 轴属性 |
| `zAxisBorder` | Object | 边框 3D z 轴属性 |
| `xPlaneRear` | Object | 后侧 x 平面属性 |
| `xPlaneFront` | Object | 前侧 x 平面属性 |
| `yPlaneRear` | Object | 后侧 y 平面属性 |
| `yPlaneFront` | Object | 前侧 y 平面属性 |
| `zPlaneRear` | Object | 后侧 z 平面属性 |
| `zPlaneFront` | Object | 前侧 z 平面属性 |

## 示例

### 1. 基本 3D 视图（平行投影）

```js
var bound = [-4, 6];
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [bound, bound, bound]],
    {
        projection: 'parallel',
        trackball: {enabled: true},
    });

var curve = view.create('curve3d', [
    (t) => (2 + Math.cos(3 * t)) * Math.cos(2 * t),
    (t) => (2 + Math.cos(3 * t)) * Math.sin(2 * t),
    (t) => Math.sin(3 * t),
    [-Math.PI, Math.PI]
], { strokeWidth: 4 });
```

### 2. 透视投影

```js
var bound = [-4, 6];
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [bound, bound, bound]],
    {
        projection: 'central',
        trackball: {enabled: true},

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

### 3. 边框坐标轴

```js
var bound = [-4, 6];
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [bound, bound, bound]],
    {
        projection: 'central',
        trackball: {enabled: true},

        // 主轴在边框
        axesPosition: 'border',

        // 边框坐标轴设置
        xAxisBorder: { ticks3d: { ticksDistance: 2} },
        yAxisBorder: { ticks3d: { ticksDistance: 2} },
        zAxisBorder: { ticks3d: { ticksDistance: 2} },

        // 平面上不显示坐标轴
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

### 4. 不显示坐标轴

```js
var bound = [-4, 6];
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [bound, bound, bound]],
    {
        projection: 'central',
        trackball: {enabled: true},

        axesPosition: 'none'
    });

var curve = view.create('curve3d', [
    (t) => (2 + Math.cos(3 * t)) * Math.cos(2 * t),
    (t) => (2 + Math.cos(3 * t)) * Math.sin(2 * t),
    (t) => Math.sin(3 * t),
    [-Math.PI, Math.PI]
], { strokeWidth: 4 });
```

### 5. 自定义平面样式

```js
var bound = [-4, 6];
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [bound, bound, bound]],
    {
        projection: 'central',
        trackball: {enabled: true},

        axesPosition: 'border',

        xAxisBorder: { ticks3d: { ticksDistance: 2} },
        yAxisBorder: { ticks3d: { ticksDistance: 2} },
        zAxisBorder: { ticks3d: { ticksDistance: 2} },

        // 后侧平面
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

        // 前侧平面
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
        }
    });

var curve = view.create('curve3d', [
    (t) => (2 + Math.cos(3 * t)) * Math.cos(2 * t),
    (t) => (2 + Math.cos(3 * t)) * Math.sin(2 * t),
    (t) => Math.sin(3 * t),
    [-Math.PI, Math.PI]
], { strokeWidth: 4 });
```

### 6. 中心坐标轴和自定义平面

```js
var bound = [-5, 5];
var view = board.create('view3d',
    [[-6, -3],
     [8, 8],
     [bound, bound, bound]],
    {
        // 主轴在中心
        axesPosition: 'center',
        xAxis: { strokeColor: 'blue', strokeWidth: 3},

        // 平面
        xPlaneRear: { fillColor: 'yellow',  mesh3d: {visible: false}},
        yPlaneFront: { visible: true, fillColor: 'blue'},

        // 平面上的坐标轴
        xPlaneRearYAxis: {strokeColor: 'red'},
        xPlaneRearZAxis: {strokeColor: 'red'},

        yPlaneFrontXAxis: {strokeColor: 'blue'},
        yPlaneFrontZAxis: {strokeColor: 'blue'},

        zPlaneFrontXAxis: {visible: false},
        zPlaneFrontYAxis: {visible: false}
    });
```

### 7. 角度滑块控制

```js
var bound = [-5, 5];
var view = board.create('view3d',
    [[-6, -3], [8, 8],
    [bound, bound, bound]],
    {
        projection: 'central',

        // 方位角滑块
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

        // 仰角滑块
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

        // 倾斜角滑块
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

### 8. 创建 3D 点和直线

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        projection: 'central',
        trackball: {enabled: true}
    });

// 创建 3D 点
var p1 = view.create('point3d', [1, 2, 3], {
    size: 5,
    withLabel: true,
    name: 'P1'
});

var p2 = view.create('point3d', [4, 1, 2], {
    size: 5,
    withLabel: true,
    name: 'P2'
});

// 创建 3D 直线
var line = view.create('line3d', [p1, p2], {
    strokeColor: 'blue',
    strokeWidth: 2
});
```

### 9. 创建 3D 球体

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        projection: 'central',
        depthOrder: { enabled: true }
    });

// 球心和半径点
var center = view.create('point3d', [0, 0, 0], {size: 3});
var radiusPoint = view.create('point3d', [3, 0, 0], {size: 3});

// 球体
var sphere = view.create('sphere3d', [center, radiusPoint], {
    fillColor: 'blue',
    fillOpacity: 0.3
});
```

### 10. 预设视图切换

```js
var bound = [-5, 5];
var view = board.create('view3d',
    [[-6, -3], [8, 8],
    [bound, bound, bound]],
    {
        projection: 'central',

        // 预设视图，可通过键盘 picture-up/picture-down 切换
        values: [
            [0, 1.57],      // 视图 1：仰角 0，方位角 1.57
            [0.78, 0.62],   // 视图 2
            [0, 0],         // 视图 3：正视图
            [5.49, 0.62],   // 视图 4
            [4.71, 0],      // 视图 5
            [3.93, 0.62],   // 视图 6
            [3.14, 0],      // 视图 7：后视图
            [2.36, 0.62],   // 视图 8
            [1.57, 1.57]    // 视图 9：俯视图
        ]
    });
```

### 11. 垂直拖拽

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        projection: 'central',

        // 启用垂直拖拽（按住 Shift 键）
        verticalDrag: {
            enabled: true,
            key: 'shift'
        }
    });

// 创建可垂直拖动的点
var p = view.create('point3d', [2, 2, 2], {
    size: 5,
    name: '按住 Shift 垂直拖动'
});
```

### 12. 完整 3D 场景

```js
var bound = [-5, 5];
var view = board.create('view3d',
    [[-6, -4], [10, 8],
    [bound, bound, bound]],
    {
        projection: 'central',
        trackball: {
            enabled: true,
            button: 0  // 左键
        },
        depthOrder: {
            enabled: true,
            layers: [12, 13]
        },
        axesPosition: 'center',

        // 坐标轴样式
        xAxis: {
            strokeColor: 'red',
            strokeWidth: 2,
            lastArrow: true,
            withLabel: true,
            name: 'x'
        },
        yAxis: {
            strokeColor: 'green',
            strokeWidth: 2,
            lastArrow: true,
            withLabel: true,
            name: 'y'
        },
        zAxis: {
            strokeColor: 'blue',
            strokeWidth: 2,
            lastArrow: true,
            withLabel: true,
            name: 'z'
        },

        // 平面样式
        xPlaneRear: {
            fillColor: '#ffcccc',
            fillOpacity: 0.2,
            mesh3d: {visible: true}
        },
        yPlaneRear: {
            fillColor: '#ccffcc',
            fillOpacity: 0.2,
            mesh3d: {visible: true}
        },
        zPlaneRear: {
            fillColor: '#ccccff',
            fillOpacity: 0.2,
            mesh3d: {visible: true}
        }
    });

// 创建螺旋线
var helix = view.create('curve3d', [
    function(t) { return 3 * Math.cos(t); },
    function(t) { return 3 * Math.sin(t); },
    function(t) { return t / (2 * PI); },
    [0, 4 * PI]
], {
    strokeWidth: 3,
    strokeColor: 'purple'
});

// 创建球体
var center = view.create('point3d', [0, 0, 0], {size: 3});
var radiusPoint = view.create('point3d', [2, 0, 0], {size: 3});
var sphere = view.create('sphere3d', [center, radiusPoint], {
    fillColor: 'yellow',
    fillOpacity: 0.3
});
```

## 注意事项

1. **投影类型**：
   - `parallel`：平行投影，适合技术图纸和精确测量
   - `central`：透视投影，提供更真实的 3D 效果

2. **坐标范围**：`cube` 参数定义了 3D 空间的可见范围，超出范围的元素可能被裁剪

3. **深度排序**：启用 `depthOrder` 可以改善多个 3D 元素的层叠显示效果，但可能影响性能

4. **轨迹球**：启用 `trackball` 后，可以通过鼠标拖动来旋转 3D 场景，提供 3 个自由度的操作

5. **角度控制**：
   - `az`（方位角）：绕 Z 轴旋转
   - `el`（仰角）：上下视角
   - `bank`（倾斜角）：绕视线旋转

6. **键盘快捷键**：
   - 方向键：调整方位角和仰角
   - picture-up/picture-down：切换预设视图
   - 按住 Ctrl/Shift：配合鼠标操作

7. **平面可见性**：可以通过设置 `xPlaneRear.visible: false` 等属性来控制平面的可见性

## 相关元素

- [Point3D](./Point3D.md) - 3D 点
- [Line3D](./Line3D.md) - 3D 直线
- [Curve3D](./Curve3D.md) - 3D 曲线
- [Sphere3D](./Sphere3D.md) - 3D 球体
- [Axis3D](./Axis3D.md) - 3D 坐标轴
