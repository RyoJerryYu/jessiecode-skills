# Axis3D 3D 单轴

## 描述

3D 轴元素是一条带有可选刻度和标签的直线。

*定义于：* [box3d.js](./src/src_3d_box3d.js.md)

*继承自：* [Arrow](./Arrow.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
   ↳ **[JXG.Line](./JXG.Line.md)**
      ↳ **[Arrow](./Arrow.md)**
         ↳ **Axis3D**

## JessieCode 语法

```js
// 通过起点和终点创建 3D 轴
axis = axis3d(start, end);

// 在 3D 视图中创建
view = view3d(...) <<
    axesPosition: 'center'
>>;
xAxis = view.create('axis3d', [startPoint, endPoint]);

// 带属性创建
axis = axis3d([0, 0, 0], [5, 0, 0]) <<
    strokeColor: 'red',
    withLabel: true,
    name: 'x'
>>;
```

## 参数

### 方式一：两个点数组

| 参数 | 类型 | 描述 |
|------|------|------|
| `start` | Array | 起点坐标，长度为 3 的数组 `[x, y, z]` |
| `end` | Array | 终点坐标，长度为 3 的数组 `[x, y, z]` |

### 方式二：使用函数

| 参数 | 类型 | 描述 |
|------|------|------|
| `start` | Function | 返回起点坐标的函数 |
| `end` | Function | 返回终点坐标的函数 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 2 | 线宽 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 轴的名称 |
| `lastArrow` | Boolean/Object | true | 是否在终点显示箭头 |
| `visible` | Boolean | true | 是否可见 |
| `dash` | Number | 0 | 虚线样式 |
| `ticks` | Object | - | 刻度设置 |

### 刻度属性

```js
// 设置刻度
axis = axis3d(start, end) <<
    ticks: <<
        visible: true,
        strokeColor: 'black',
        strokeWidth: 1,
        tickLength: 5,
        tickEnds: [0, 1],
        tickDistance: 1
    >>
>>;
```

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `visible` | Boolean | false | 是否显示刻度 |
| `strokeColor` | String | '#000000' | 刻度颜色 |
| `strokeWidth` | Number | 1 | 刻度线宽 |
| `tickLength` | Number | 5 | 刻度长度（像素） |
| `tickEnds` | Array | [0, 1] | 刻度范围 |
| `tickDistance` | Number | 1 | 刻度间距 |

## 示例

### 1. 创建基本 3D 轴

```js
// 在 3D 视图中创建
view = view3d(
    [[-4, -4], [8, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 创建 x 轴
xAxis = view.create('axis3d', [[0, 0, 0], [5, 0, 0]]) <<
    strokeColor: 'red',
    name: 'x'
>>;
```

### 2. 创建三个坐标轴

```js
view = view3d(
    [[-6, -3], [10, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center',
    withLabel: true
>>;

// x 轴（红色）
xAxis = view.create('axis3d', [[0, 0, 0], [4, 0, 0]]) <<
    strokeColor: 'red',
    name: 'x',
    lastArrow: true
>>;

// y 轴（绿色）
yAxis = view.create('axis3d', [[0, 0, 0], [0, 4, 0]]) <<
    strokeColor: 'green',
    name: 'y',
    lastArrow: true
>>;

// z 轴（蓝色）
zAxis = view.create('axis3d', [[0, 0, 0], [0, 0, 4]]) <<
    strokeColor: 'blue',
    name: 'z',
    lastArrow: true
>>;
```

### 3. 带标签的 3D 轴

```js
view = view3d(
    [[-6, -3], [10, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 带标签的 x 轴
xAxis = view.create('axis3d', [[0, 0, 0], [5, 0, 0]]) <<
    withLabel: true,
    name: 'x-axis',
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

### 4. 带刻度的 3D 轴

```js
view = view3d(
    [[-6, -3], [10, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 带刻度的轴
axis = view.create('axis3d', [[0, 0, 0], [5, 0, 0]]) <<
    strokeColor: 'black',
    ticks: <<
        visible: true,
        strokeColor: 'gray',
        tickLength: 5,
        tickDistance: 1
    >>
>>;
```

### 5. 自定义起点和终点的轴

```js
// 从点 (1, 2, 3) 到点 (4, 2, 3) 的轴
axis = view.create('axis3d', [[1, 2, 3], [4, 2, 3]]) <<
    strokeColor: 'purple',
    name: 'custom',
    lastArrow: true
>>;
```

### 6. 动态 3D 轴

```js
// 创建滑块
length = slider(1, 5, 0.1);

// 长度可变的轴
dynamicAxis = view.create('axis3d', [
    [0, 0, 0],
    function() { return [V(length), 0, 0]; }
]) <<
    strokeColor: 'blue',
    name: 'dynamic'
>>;
```

### 7. 与 3D 点组合

```js
view = view3d(
    [[-6, -3], [10, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center'
>>;

// 创建原点
O = view.create('point3d', [0, 0, 0]) <<
    name: 'O',
    size: 5,
    strokeColor: 'black'
>>;

// 创建轴上的点
P = view.create('point3d', [3, 0, 0]) <<
    name: 'P',
    size: 4,
    strokeColor: 'red'
>>;

// 创建轴
axis = view.create('axis3d', [O, P]) <<
    strokeColor: 'red',
    lastArrow: true
>>;
```

### 8. 虚线 3D 轴

```js
// 虚线轴（用于辅助线）
dashedAxis = view.create('axis3d', [[0, 0, 0], [3, 3, 3]]) <<
    strokeColor: 'gray',
    dash: 1,
    strokeWidth: 1
>>;
```

## 注意事项

1. **箭头方向**：`lastArrow: true` 在轴的终点显示箭头，表示正方向
2. **标签位置**：标签通常显示在轴的末端箭头附近
3. **中心坐标轴**：当 `axesPosition: 'center'` 时，轴从原点 (0,0,0) 开始
4. **继承 Arrow**：Axis3D 继承自 Arrow，因此可以使用所有 Arrow 的属性
5. **刻度显示**：使用 `ticks` 属性可以添加刻度标记

## 相关元素

- [Axes3D](./Axes3D.md) - 3D 坐标轴容器
- [Arrow](./Arrow.md) - 箭头
- [Line3D](./Line3D.md) - 3D 直线
- [Point3D](./Point3D.md) - 3D 点
- [Ticks](./Ticks.md) - 刻度
