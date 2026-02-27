# Metapostspline 元样条曲线

<!-- USAGE_FREQUENCY: advanced -->

## 描述

使用来自 Metapost（由 Donald Knuth 和 John Hobby 开发）的样条曲线插值数据点。创建由样本点 p_1 到 p_n 定义的动态 Metapost 样条插值曲线。

*定义于：* [curve.js](./src/src_base_curve.js.md)
继承自 [JXG.Curve](./JXG.Curve.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
    ↳ **[JXG.Curve](./JXG.Curve.md)**
         ↳ **Metapostspline**

## JessieCode 语法

```js
// 通过点数组创建 Metapost 样条曲线
curve = metapostspline([P1, P2, P3, P4], controls);

// 通过坐标数组创建
curve = metapostspline([[x1, y1], [x2, y2], [x3, y3]], controls);

// 通过分离的 x 和 y 坐标数组创建
curve = metapostspline([[x1, x2, x3], [y1, y2, y3]], controls);

// 带属性创建
curve = metapostspline([points, controls]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 参数

### 父数组组合

| 参数 | 类型 | 描述 |
|------|------|------|
| board | Board | Metapost 样条曲线绘制的画板引用 |
| parents | Array | 包含两个条目的数组：第一个条目是要插值的点数组，第二个条目是包含控制值（如 tension、direction、curl）的 JavaScript 对象 |
| attributes | Object | 定义 Metapost 样条曲线的颜色、宽度等属性 |

### 点数组格式

第一个条目可以是以下格式之一：

- JSXGraph 点对象数组
- 坐标对对象
- 返回坐标对的函数数组
- 包含 x 坐标数组和 y 坐标数组的数组

所有坐标数组的单个条目可以是数字或返回数字的函数。

### 控制对象属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `tension` | Number/Function | 张力值，控制曲线的紧绷程度 |
| `direction` | Object | 指定某些点的方向角度 |
| `curl` | Object | 指定端点的卷曲程度 |
| `isClosed` | Boolean | 是否为闭合曲线 |

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线，3=点划线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |

### 专用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `createPoints` | Boolean | true | 控制当基数样条数据点以数组形式给定时，是否应转换为 JXG.Points |
| `isArrayOfCoordinates` | Boolean | true | 如果设为 true，提供的坐标被解释为 [[x_0, y_0], [x_1, y_1], ...]；如果数据由两个等长数组组成，则解释为 [[x_0, x_1, ..., x_n], [y_0, y_1, ..., y_n]] |
| `points` | Object | - | 当 createPoints 设为 true 时，由 Metapost 样条生成的点的属性 |

## 方法

继承自 [JXG.Curve](./Curve.md) 的方法。

## 示例

### 1. 创建基本 Metapost 样条曲线

```js
// 创建控制点
po = [];
po.push(point(-3, -3));
po.push(point(0, -3));
po.push(point(4, -5));
po.push(point(6, -2));

// 创建控制参数
controls = {
    tension: 1,
    isClosed: false
};

// 绘制 Metapost 样条曲线
cu = metapostspline([po, controls]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 2. 使用滑块动态控制张力

```js
// 创建滑块控制张力
tensionSlider = slider([-3, 6], [3, 6], [0, 1, 20]) << name: 'tension' >>;

// 创建控制点
po = [];
po.push(point(-3, -3));
po.push(point(0, -3));
po.push(point(4, -5));
po.push(point(6, -2));

// 创建带动态张力的样条曲线
controls = {
    tension: function() { return V(tensionSlider); }
};

cu = metapostspline([po, controls]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 3. 控制端点的卷曲程度

```js
// 创建滑块控制卷曲
curlSlider = slider([-3, 5], [3, 5], [0, 1, 30]) << name: 'curl A, D' >>;

// 创建控制点
po = [];
po.push(point(-3, -3));  // 点 0
po.push(point(0, -3));   // 点 1
po.push(point(4, -5));   // 点 2
po.push(point(6, -2));   // 点 3

// 设置端点的卷曲程度
controls = {
    curl: {
        0: function() { return V(curlSlider); },  // 起点卷曲
        3: function() { return V(curlSlider); }   // 终点卷曲
    },
    isClosed: false
};

cu = metapostspline([po, controls]) <<
    strokeColor: 'green',
    strokeWidth: 2
>>;
```

### 4. 控制特定点的方向

```js
// 创建滑块控制方向
dirSlider = slider([-3, 4], [3, 4], [-180, 0, 180]) << name: 'direction B' >>;

// 创建控制点
po = [];
po.push(point(-3, -3));
po.push(point(0, -3));   // 点 1 - 将控制方向
po.push(point(4, -5));
po.push(point(6, -2));

// 设置特定点的方向
controls = {
    direction: {
        1: function() { return V(dirSlider); }  // 控制点 1 的方向
    },
    isClosed: false
};

cu = metapostspline([po, controls]) <<
    strokeColor: 'purple',
    strokeWidth: 2
>>;
```

### 5. 创建闭合样条曲线

```js
// 创建控制点
po = [];
po.push(point(-2, 0));
po.push(point(0, 2));
po.push(point(2, 0));
po.push(point(0, -2));

// 创建闭合样条曲线
controls = {
    tension: 1,
    isClosed: true
};

cu = metapostspline([po, controls]) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

### 6. 使用坐标数组创建

```js
// 使用坐标对数组
coords = [[-3, -3], [0, -3], [4, -5], [6, -2]];

cu = metapostspline([coords, { isClosed: false }]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 或使用分离的 x 和 y 数组
xCoords = [-3, 0, 4, 6];
yCoords = [-3, -3, -5, -2];

cu2 = metapostspline([[xCoords, yCoords], { isClosed: false }]) <<
    strokeColor: 'green',
    strokeWidth: 2
>>;
```

### 7. 完整的动态控制示例

```js
// 创建所有控制滑块
tension = slider([-3, 6], [3, 6], [0, 1, 20]) << name: 'tension' >>;
curl = slider([-3, 5], [3, 5], [0, 1, 30]) << name: 'curl A, D' >>;
dir = slider([-3, 4], [3, 4], [-180, 0, 180]) << name: 'direction B' >>;

// 创建控制点
po = [];
po.push(point(-3, -3));
po.push(point(0, -3));
po.push(point(4, -5));
po.push(point(6, -2));

// 创建完整的控制对象
controls = {
    tension: function() { return V(tension); },
    direction: {
        1: function() { return V(dir); }
    },
    curl: {
        0: function() { return V(curl); },
        3: function() { return V(curl); }
    },
    isClosed: false
};

// 绘制 Metapost 样条曲线
cu = metapostspline([po, controls]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 注意事项

1. **控制参数**：`tension`（张力）控制曲线的紧绷程度，值越大曲线越直；`curl`（卷曲）控制端点的弯曲程度；`direction`（方向）指定特定点处的切线方向角度

2. **索引编号**：在 `direction` 和 `curl` 对象中，点的索引从 0 开始

3. **闭合曲线**：设置 `isClosed: true` 创建闭合样条曲线，此时起点和终点会平滑连接

4. **动态更新**：所有控制参数都可以是函数，用于创建动态交互的样条曲线

5. **数据格式**：点数据可以是 JSXGraph 点对象、坐标对数组、或分离的 x/y 坐标数组

6. **点的创建**：当 `createPoints: true` 时，会自动为数据点创建可见的 Point 元素

## 相关元素

- [Curve](./Curve.md) - 曲线
- [Cardinalspline](./Cardinalspline.md) - 基数样条曲线
- [Bezier](./Bezier.md) - 贝塞尔曲线
- [Functiongraph](./Functiongraph.md) - 函数图像
- [B-spline](./Bspline.md) - B 样条曲线
