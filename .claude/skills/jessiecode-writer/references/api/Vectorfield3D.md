# Vectorfield3D 3D 向量场

<!-- USAGE_FREQUENCY: advanced -->

## 描述

向量场是对 3D 空间中每个点分配一个向量。

绘制 3D 向量场可以通过两种方式定义：
- 三个函数 f1(x, y, z)、f2(x, y, z) 和 f3(x, y, z)
- 一个返回长度为 3 的数组的函数 f(x, y, z)

## JessieCode 语法

```js
// 基本语法 - 创建 3D 向量场
field = vectorfield3d(F, xData, yData, zData);

// 使用三个函数定义
field = vectorfield3d([f1, f2, f3], [xStart, xSteps, xEnd], [yStart, ySteps, yEnd], [zStart, zSteps, zEnd]);

// 使用返回数组的函数定义
field = vectorfield3d(f, [xStart, xSteps, xEnd], [yStart, ySteps, yEnd], [zStart, zSteps, zEnd]);

// 带属性创建
field = vectorfield3d(
    [(x, y, z) => cos(y), (x, y, z) => sin(x), (x, y, z) => z],
    [-2, 5, 2],
    [-2, 5, 2],
    [-2, 5, 2]
) <<
    strokeColor: 'red',
    scale: 0.5
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| F | Array/Function | 包含三个函数 f1(x, y, z)、f2(x, y, z) 和 f3(x, y, z) 的数组，或返回长度为 3 的数组的函数 f(x, y, z) |
| xData | Array | 长度为 3 的数组，包含 x 的起始值、步数、结束值。向量场在 x 方向将包含 (步数) + 1 个向量 |
| yData | Array | 长度为 3 的数组，包含 y 的起始值、步数、结束值。向量场在 y 方向将包含 (步数) + 1 个向量 |
| zData | Array | 长度为 3 的数组，包含 z 的起始值、步数、结束值。向量场在 z 方向将包含 (步数) + 1 个向量 |

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `scale` | Number/Function | 1 | 向量的缩放因子 |
| `arrowHead` | Object | 见下方 | 自定义向量的箭头样式 |
| `strokeColor` | String | '#000000' | 向量线条颜色 |
| `strokeWidth` | Number | 2 | 向量线条宽度 |
| `highlightStrokeColor` | String | 高亮颜色 | 高亮时的颜色 |

### 箭头属性 (arrowHead)

```js
arrowHead: <<
    enabled: true,    // 是否启用箭头
    size: 5,          // 箭头腿的长度（像素）
    angle: PI * 0.125 // 箭头腿的角度（弧度）
>>
```

| 字段 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `enabled` | Boolean | true | 是否启用箭头 |
| `size` | Number | 5 | 箭头腿的长度（像素） |
| `angle` | Number | π/8 | 箭头腿的角度（弧度） |

**注意**：启用箭头会降低性能。

## 方法

### setF(func)

设置 3D 向量场的定义函数。

| 参数 | 类型 | 描述 |
|------|------|------|
| func | Array/Function | 包含三个函数 f1(x, y, z)、f2(x, y, z) 和 f3(x, y, z) 的数组，或返回长度为 3 的数组的函数 f(x, y, z) |

**返回值**：3D 向量场对象的引用

**注意**：在 JessieCode 中，通常通过重新创建元素或使用动态函数来实现更新。

## 示例

### 1. 创建基本 3D 向量场

```js
// 创建 3D 视图
view = view3d(
    [-6, -3],
    [8, 8],
    [[-3, 3], [-3, 3], [-3, 3]]
);

// 定义三个函数
f1 = (x, y, z) => cos(y);
f2 = (x, y, z) => sin(x);
f3 = (x, y, z) => z;

// 创建 3D 向量场
vf = view.create('vectorfield3d', [
    [f1, f2, f3],
    [-2, 5, 2],  // x 从 -2 到 2，5 步
    [-2, 5, 2],  // y 从 -2 到 2，5 步
    [-2, 5, 2]   // z 从 -2 到 2，5 步
]) <<
    strokeColor: 'red',
    scale: 0.5
>>;
```

### 2. 使用返回数组的函数

```js
// 创建 3D 视图
view = view3d(
    [-6, -3],
    [8, 8],
    [[-3, 3], [-3, 3], [-3, 3]]
);

// 定义返回数组的函数
f = (x, y, z) => [sin(y), cos(x), z];

// 创建 3D 向量场
vf = view.create('vectorfield3d', [
    f,
    [-2, 5, 2],
    [-2, 5, 2],
    [-2, 5, 2]
]);
```

### 3. 使用滑块控制 3D 向量场

```js
// 创建 3D 视图
view = view3d(
    [-6, -3],
    [8, 8],
    [[-3, 3], [-3, 3], [-3, 3]]
);

// 创建滑块控制向量长度
s = slider(0, 2, 0.1);

// 创建 3D 向量场，使用滑块控制缩放
vf = view.create('vectorfield3d', [
    [(x, y, z) => cos(y), (x, y, z) => sin(x), (x, y, z) => z],
    [-2, 5, 2],
    [-2, 5, 2],
    [-2, 5, 2]
]) <<
    strokeColor: 'blue',
    scale: function() { return V(s); }
>>;
```

### 4. 漩涡 3D 向量场

```js
// 创建 3D 视图
view = view3d(
    [-6, -3],
    [8, 8],
    [[-3, 3], [-3, 3], [-3, 3]]
);

// 创建漩涡向量场
vf = view.create('vectorfield3d', [
    [(x, y, z) => -y, (x, y, z) => x, (x, y, z) => 0],
    [-2, 5, 2],
    [-2, 5, 2],
    [-2, 5, 2]
]) <<
    scale: 0.5,
    arrowHead: <<
        enabled: true,
        size: 6,
        angle: PI / 12
    >>,
    strokeColor: 'purple'
>>;
```

### 5. 带箭头的 3D 向量场

```js
// 创建 3D 视图
view = view3d(
    [-6, -3],
    [8, 8],
    [[-3, 3], [-3, 3], [-3, 3]]
);

// 创建带大箭头的 3D 向量场
vf = view.create('vectorfield3d', [
    [(x, y, z) => sin(y), (x, y, z) => cos(x), (x, y, z) => z],
    [-2, 5, 2],
    [-2, 5, 2],
    [-2, 5, 2]
]) <<
    arrowHead: <<
        enabled: true,
        size: 8,
        angle: PI / 16
    >>,
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

### 6. 动态 3D 向量场

```js
// 创建 3D 视图
view = view3d(
    [-6, -3],
    [8, 8],
    [[-3, 3], [-3, 3], [-3, 3]]
);

// 创建滑块控制参数
a = slider(-2, 2, 0.1);

// 创建动态 3D 向量场
vf = view.create('vectorfield3d', [
    [function(x, y, z) { return a * x; },
     function(x, y, z) { return -a * y; },
     function(x, y, z) { return z; }],
    [-2, 5, 2],
    [-2, 5, 2],
    [-2, 5, 2]
]) <<
    strokeColor: 'green'
>>;
```

## 注意事项

1. **3D 视图必需**：3D 向量场必须在 3D 视图（view3d）中创建
2. **性能**：启用箭头 (`arrowHead.enabled: true`) 会降低渲染性能，特别是在网格点较多时
3. **缩放**：`scale` 属性用于控制向量的显示长度，值为 1 表示原始大小
4. **函数定义**：可以使用三个独立函数或一个返回数组的函数来定义向量场
5. **网格密度**：xData、yData 和 zData 中的步数值决定了向量的密度，步数越多向量越密集
6. **动态更新**：可以通过在参数中使用函数来实现动态更新的 3D 向量场
7. **创建方式**：在 JessieCode 中，3D 元素通常需要使用 `view.create()` 方法创建

## 相关元素

- [Vectorfield](./Vectorfield.md) - 2D 向量场
- [Slopefield](./Slopefield.md) - 斜率场
- [Curve3D](./Curve3D.md) - 3D 曲线
- [View3D](./View3D.md) - 3D 视图
- [Slider](./Slider.md) - 滑块（用于动态控制）
