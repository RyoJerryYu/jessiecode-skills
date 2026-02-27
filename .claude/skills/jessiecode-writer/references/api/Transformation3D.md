# Transformation3D 3D 变换

<!-- USAGE_FREQUENCY: advanced -->

## 描述

定义投影 3D 变换，如平移、旋转、反射、缩放等。变换基于 4x4 矩阵，可以应用于 3D 点、线、曲线等几何元素。

## JessieCode 语法

```js
// 创建 3D 变换
t = view.create('transform3d', [parameters], << type: 'transformType' >>);

// 应用变换到元素
P2 = view.create('point3d', [P1, t], options);
```

## 变换类型

### 1. 平移 (translate)

```js
// 平移向量 (x, y, z)
t = view.create('transform3d', [x, y, z], << type: 'translate' >>);
```

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number/Function | x 方向平移量 |
| y | Number/Function | y 方向平移量 |
| z | Number/Function | z 方向平移量 |

**变换矩阵**：
```
(1  0  0  0)
(0  1  0  0)
(0  0  1  0)
(x  y  z  1)
```

**示例**：
```js
// 沿 x 轴平移 2 单位，y 轴 3 单位，z 轴 2 单位
var t1 = view.create('transform3d', [2, 3, 2], { type: 'translate' });
```

### 2. 缩放 (scale)

```js
// 缩放因子 (scale_x, scale_y, scale_z)
t = view.create('transform3d', [scale_x, scale_y, scale_z], << type: 'scale' >>);
```

| 参数 | 类型 | 描述 |
|------|------|------|
| scale_x | Number/Function | x 方向缩放因子 |
| scale_y | Number/Function | y 方向缩放因子 |
| scale_z | Number/Function | z 方向缩放因子 |

**变换矩阵**：
```
(1  0    0   0)
(0  sx   0   0)
(0  0   sy   0)
(0  0    0  sz)
```

**示例**：
```js
// x 方向放大 2 倍，y 方向放大 3 倍，z 方向不变
var t = view.create('transform3d', [2, 3, 1], { type: 'scale' });
```

### 3. 旋转 (rotate)

```js
// 绕任意轴旋转
t = view.create('transform3d', [angle, normal, point], << type: 'rotate' >>);

// 绕 X 轴旋转
t = view.create('transform3d', [angle, point], << type: 'rotateX' >>);

// 绕 Y 轴旋转
t = view.create('transform3d', [angle, point], << type: 'rotateY' >>);

// 绕 Z 轴旋转
t = view.create('transform3d', [angle, point], << type: 'rotateZ' >>);
```

| 参数 | 类型 | 描述 |
|------|------|------|
| angle | Number/Function | 旋转角度（弧度） |
| normal | Array | 旋转轴的法向量 [nx, ny, nz] |
| point | Array | 旋转中心点 [x, y, z]（可选，默认为原点） |

**rotateX 变换矩阵**（绕 X 轴旋转角度 a）：
```
(1  0      0     0)
(0  cos(a) -sin(a) 0)
(0  sin(a)  cos(a) 0)
(0  0      0     1)
```

**示例**：
```js
// 绕 Z 轴旋转 45 度（PI/4 弧度）
var t = view.create('transform3d', [PI/4, [0, 0, 0]], { type: 'rotateZ' });

// 绕任意轴旋转
var t2 = view.create('transform3d', [PI/6, [1, 1, 0], [0, 0, 0]], { type: 'rotate' });
```

## 示例

### 1. 平移变换

```js
var bound = [-5, 5];
var view = board.create('view3d',
    [[-6, -3], [8, 8],
    [bound, bound, bound]]);

var slider = board.create('slider', [[-4, 4], [0, 4], [0, 0, 5]]);

var p1 = view.create('point3d', [1, 2, 2], { name: '拖动我', size: 5 });

// 固定平移
var t1 = view.create('transform3d', [2, 3, 2], { type: 'translate' });
var p2 = view.create('point3d', [p1, t1], { name: '固定平移', size: 5 });

// 动态平移（由滑块控制）
var t2 = view.create('transform3d', [
    function() { return slider.Value() + 3; },
    0, 0
], { type: 'translate' });
var p3 = view.create('point3d', [p1, t2], { name: '函数平移', size: 5 });
```

### 2. 缩放变换

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 原始点
var p1 = view.create('point3d', [1, 1, 1], { size: 4, name: 'P1' });

// 均匀缩放（2 倍）
var scaleUniform = view.create('transform3d', [2, 2, 2], { type: 'scale' });
var p2 = view.create('point3d', [p1, scaleUniform], { size: 4, name: 'P2' });

// 非均匀缩放
var scaleNonUniform = view.create('transform3d', [2, 0.5, 1], { type: 'scale' });
var p3 = view.create('point3d', [p1, scaleNonUniform], { size: 4, name: 'P3' });
```

### 3. 旋转变换

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        projection: 'central'
    });

// 原始点
var p1 = view.create('point3d', [2, 0, 0], { size: 4, name: 'P1' });

// 绕 Z 轴旋转 90 度
var rotZ = view.create('transform3d', [PI/2, [0, 0, 0]], { type: 'rotateZ' });
var p2 = view.create('point3d', [p1, rotZ], { size: 4, name: 'P2' });

// 绕 Y 轴旋转 90 度
var rotY = view.create('transform3d', [PI/2, [0, 0, 0]], { type: 'rotateY' });
var p3 = view.create('point3d', [p1, rotY], { size: 4, name: 'P3' });

// 绕 X 轴旋转 90 度
var rotX = view.create('transform3d', [PI/2, [0, 0, 0]], { type: 'rotateX' });
var p4 = view.create('point3d', [p1, rotX], { size: 4, name: 'P4' });
```

### 4. 动态旋转

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 创建滑块控制角度
var angleSlider = board.create('slider', [[-4, 4], [4, 4], [0, 0, 2 * PI]]);

// 原始点
var p1 = view.create('point3d', [3, 0, 0], { size: 4 });

// 绕 Z 轴动态旋转
var rot = view.create('transform3d', [
    function() { return angleSlider.Value(); },
    [0, 0, 0]
], { type: 'rotateZ' });

// 旋转后的点
var p2 = view.create('point3d', [p1, rot], {
    size: 4,
    color: 'red',
    name: function() { return '角度：' + angleSlider.Value().toFixed(2); }
});

// 创建轨迹
var trace = view.create('curve3d', [
    function(t) { return 3 * Math.cos(t); },
    function(t) { return 3 * Math.sin(t); },
    function() { return 0; },
    [0, 2 * PI]
], { strokeColor: 'gray', dash: 1 });
```

### 5. 绕任意轴旋转

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 定义旋转轴（从原点到 [1,1,1] 的向量）
var axis = [1, 1, 1];

// 原始点
var p1 = view.create('point3d', [2, 0, 0], { size: 4 });

// 绕任意轴旋转 45 度
var rot = view.create('transform3d', [PI/4, axis, [0, 0, 0]], { type: 'rotate' });

// 旋转后的点
var p2 = view.create('point3d', [p1, rot], { size: 4, color: 'red' });
```

### 6. 变换串联

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 原始点
var p1 = view.create('point3d', [1, 1, 1], { size: 4 });

// 定义多个变换
var translate = view.create('transform3d', [1, 0, 0], { type: 'translate' });
var rotate = view.create('transform3d', [PI/4, [0, 0, 0]], { type: 'rotateZ' });
var scale = view.create('transform3d', [2, 2, 2], { type: 'scale' });

// 依次应用变换
var p2 = view.create('point3d', [p1, translate], { size: 4 });
var p3 = view.create('point3d', [p2, rotate], { size: 4 });
var p4 = view.create('point3d', [p3, scale], { size: 4 });

// 或一次性应用所有变换
var p5 = view.create('point3d', [p1, [translate, rotate, scale]], {
    size: 4,
    color: 'red'
});
```

### 7. 变换 3D 曲线

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        projection: 'central'
    });

// 原始螺旋线
var helix = view.create('curve3d', [
    function(t) { return Math.cos(t); },
    function(t) { return Math.sin(t); },
    function(t) { return t / (2 * PI); },
    [0, 4 * PI]
], { strokeWidth: 2, strokeColor: 'blue' });

// 缩放变换
var scale = view.create('transform3d', [2, 2, 1], { type: 'scale' });

// 变换后的螺旋线
var helixScaled = view.create('curve3d', [helix, scale], {
    strokeWidth: 2,
    strokeColor: 'red'
});
```

### 8. 滑块控制缩放

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 创建滑块
var scaleX = board.create('slider', [[-4, -2], [3, 3], [0.5, 1, 3]]);
var scaleY = board.create('slider', [[-4, -2], [2, 2], [0.5, 1, 3]]);
var scaleZ = board.create('slider', [[-4, -2], [1, 1], [0.5, 1, 3]]);

// 原始立方体顶点
var p1 = view.create('point3d', [1, 1, 1], { size: 3 });
var p2 = view.create('point3d', [-1, 1, 1], { size: 3 });
var p3 = view.create('point3d', [-1, -1, 1], { size: 3 });
var p4 = view.create('point3d', [1, -1, 1], { size: 3 });
var p5 = view.create('point3d', [1, 1, -1], { size: 3 });
var p6 = view.create('point3d', [-1, 1, -1], { size: 3 });
var p7 = view.create('point3d', [-1, -1, -1], { size: 3 });
var p8 = view.create('point3d', [1, -1, -1], { size: 3 });

// 缩放变换
var scale = view.create('transform3d', [
    function() { return scaleX.Value(); },
    function() { return scaleY.Value(); },
    function() { return scaleZ.Value(); }
], { type: 'scale' });

// 变换后的顶点
var sp1 = view.create('point3d', [p1, scale], { size: 3, color: 'red' });
var sp2 = view.create('point3d', [p2, scale], { size: 3, color: 'red' });
var sp3 = view.create('point3d', [p3, scale], { size: 3, color: 'red' });
var sp4 = view.create('point3d', [p4, scale], { size: 3, color: 'red' });
var sp5 = view.create('point3d', [p5, scale], { size: 3, color: 'red' });
var sp6 = view.create('point3d', [p6, scale], { size: 3, color: 'red' });
var sp7 = view.create('point3d', [p7, scale], { size: 3, color: 'red' });
var sp8 = view.create('point3d', [p8, scale], { size: 3, color: 'red' });
```

### 9. 中心点旋转

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 定义旋转中心
var center = view.create('point3d', [2, 2, 2], { size: 4, name: '中心' });

// 原始点
var p1 = view.create('point3d', [4, 2, 2], { size: 4 });

// 绕通过中心点的 Z 轴旋转
var rot = view.create('transform3d', [PI/3, [0, 0, 1], [2, 2, 2]], { type: 'rotateZ' });

// 旋转后的点
var p2 = view.create('point3d', [p1, rot], { size: 4, color: 'red' });

// 创建连线显示关系
var line = view.create('line3d', [center, p1], {
    strokeColor: 'gray',
    dash: 1
});
var line2 = view.create('line3d', [center, p2], {
    strokeColor: 'gray',
    dash: 1
});
```

### 10. 复合变换演示

```js
var view = board.create('view3d',
    [[-6, -3], [10, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        projection: 'central'
    });

// 原始点（蓝色）
var p1 = view.create('point3d', [1, 0, 0], {
    size: 5,
    strokeColor: 'blue',
    name: '原始点'
});

// 第一步：平移
var t1 = view.create('transform3d', [2, 0, 0], { type: 'translate' });
var p2 = view.create('point3d', [p1, t1], {
    size: 5,
    strokeColor: 'green',
    name: '平移后'
});

// 第二步：旋转
var t2 = view.create('transform3d', [PI/2, [0, 0, 1], [0, 0, 0]], { type: 'rotateZ' });
var p3 = view.create('point3d', [p2, t2], {
    size: 5,
    strokeColor: 'orange',
    name: '旋转后'
});

// 第三步：缩放
var t3 = view.create('transform3d', [1.5, 1.5, 1.5], { type: 'scale' });
var p4 = view.create('point3d', [p3, t3], {
    size: 5,
    strokeColor: 'red',
    name: '缩放后'
});
```

## 注意事项

1. **变换顺序**：变换串联时，顺序很重要。先应用的变换写在前面
2. **角度单位**：旋转角度使用弧度制，不是角度制
3. **齐次坐标**：3D 变换使用 4x4 矩阵，点在齐次坐标中表示为 (w, x, y, z)
4. **动态变换**：参数可以是函数，用于创建动态变换效果
5. **变换类型**：支持的类型包括 'translate'、'scale'、'rotate'、'rotateX'、'rotateY'、'rotateZ'
6. **旋转轴**：使用 'rotate' 类型时，需要提供旋转轴的法向量和旋转中心点

## 相关元素

- [Point3D](./Point3D.md) - 3D 点
- [Line3D](./Line3D.md) - 3D 直线
- [Curve3D](./Curve3D.md) - 3D 曲线
- [View3D](./View3D.md) - 3D 视图
- [Transformation](./Transformation.md) - 2D 变换
