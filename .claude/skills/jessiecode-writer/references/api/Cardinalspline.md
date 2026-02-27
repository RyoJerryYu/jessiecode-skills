# Cardinalspline 基数样条曲线

## 描述

基数样条曲线（Cardinal Spline）通过给定的数据点集创建平滑的插值曲线。使用基数样条插值算法，曲线会精确穿过所有给定的控制点，同时在点与点之间生成平滑的过渡。

*继承自:* [Curve](./Curve.md)

## 继承关系

**[GeometryElement](./GeometryElement.md)**
   → **[Curve](./Curve.md)**
      → **Cardinalspline**

## JessieCode 语法

```js
// 通过点数组创建基数样条曲线
c = cardinalspline([P1, P2, P3, P4, P5]);

// 带张力参数
c = cardinalspline(points, tau);

// 带属性创建
c = cardinalspline(points, tau) <<
    strokeColor: 'blue',
    strokeWidth: 3,
    createPoints: true
>>;

// 使用坐标数组创建
c = cardinalspline([[x1, y1], [x2, y2], [x3, y3]]);

// 使用分离的坐标数组创建
c = cardinalspline([[x1, x2, x3], [y1, y2, y3]]);
```

## 参数

### 方式一：点数组 + 张力参数

| 参数 | 类型 | 描述 |
|------|------|------|
| points | Array | 点数组，可以是 JSXGraph 点、坐标对、或返回坐标的函数 |
| tau | Number/Function | 张力参数（可选），控制曲线的紧绷程度 |

### 方式二：坐标数组

| 参数 | 类型 | 描述 |
|------|------|------|
| coordinates | Array | 坐标数组，可以是 `[[x1,y1], [x2,y2], ...]` 或 `[[x1,x2,...], [y1,y2,...]]` |

### 张力参数 (tau)

张力参数控制曲线的"松紧"程度：

| tau 值 | 效果 |
|--------|------|
| `0` | 标准基数样条（默认） |
| `0.5` | 常用的平滑值 |
| `1` | 曲线更贴近控制点连线 |
| 接近 `0` | 曲线更圆滑 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线 |
| `createPoints` | Boolean | true | 是否将坐标数据转换为可视点 |
| `isArrayOfCoordinates` | Boolean | true | 坐标数组的格式解释方式 |
| `points` | Object | {} | 生成点的属性（当 createPoints 为 true 时） |

### 坐标数组格式属性

**`isArrayOfCoordinates`**

| 值 | 解释方式 |
|----|---------|
| `true` | `[[x0, y0], [x1, y1], ...]` - 坐标对数组 |
| `false` | `[[x0, x1, ...], [y0, y1, ...]]` - X 和 Y 分离的数组 |

### 生成点属性

**`createPoints`**: 控制是否将数据点转换为可视的 JSXGraph 点

**`points`**: 生成点的样式属性
```js
c = cardinalspline(coords) <<
    createPoints: true,
    points: <<
        strokeColor: 'red',
        size: 4,
        withLabel: true
    >>
>>;
```

## 示例

### 1. 创建基本基数样条曲线

```js
// 通过点数组创建
P1 = point(0, 0);
P2 = point(1, 4);
P3 = point(4, 5);
P4 = point(2, 3);
P5 = point(3, 0);

// 创建样条曲线
c = cardinalspline([P1, P2, P3, P4, P5]);
```

### 2. 使用坐标数组创建

```js
// 坐标对数组格式
coords1 = [[0, 0], [1, 4], [4, 5], [2, 3], [3, 0]];
c1 = cardinalspline(coords1);

// 分离的 X,Y 数组格式
coords2 = [[0, 1, 4, 2, 3], [0, 4, 5, 3, 0]];
c2 = cardinalspline(coords2) << isArrayOfCoordinates: false >>;
```

### 3. 设置张力参数

```js
// 固定张力值
c1 = cardinalspline(points, 0);    // 标准样条
c2 = cardinalspline(points, 0.5);  // 常用平滑值
c3 = cardinalspline(points, 1);    // 紧绷样条

// 使用滑块动态调整张力
tau = slider(-1, 1, 0.01, 0.5);
c = cardinalspline(points, V(tau)) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;
```

### 4. 设置曲线样式

```js
// 蓝色粗曲线
c1 = cardinalspline(points) <<
    strokeColor: 'blue',
    strokeWidth: 4
>>;

// 虚线曲线
c2 = cardinalspline(points) <<
    dash: 1,
    strokeColor: 'gray'
>>;

// 半透明曲线
c3 = cardinalspline(points) <<
    strokeColor: 'green',
    opacity: 0.5
>>;
```

### 5. 显示/隐藏控制点

```js
// 显示控制点（默认）
c1 = cardinalspline(coords) <<
    createPoints: true,
    points: <<
        strokeColor: 'red',
        size: 4
    >>
>>;

// 不显示控制点，只显示曲线
c2 = cardinalspline(coords) <<
    createPoints: false
>>;
```

### 6. 动态样条曲线

```js
// 创建可拖动的点
A = point(0, 0);
B = point(1, 4);
C = point(4, 5);
D = point(2, 3);

// 曲线随点移动
c = cardinalspline([A, B, C, D]) <<
    strokeColor: 'blue',
    createPoints: true
>>;

// 拖动任意控制点，曲线会实时更新
```

### 7. 使用函数创建动态点

```js
// 创建滑块
t = slider(0, 2*PI, 0.01);

// 一个点沿圆周运动
P1 = point(0, 0);
P2 = point(function() { return 2*cos(V(t)); },
         function() { return 2*sin(V(t)); });
P3 = point(3, 2);
P4 = point(1, -2);

// 样条曲线随动点变化
c = cardinalspline([P1, P2, P3, P4]);
```

### 8. 比较不同张力值

```js
// 基础点集
coords = [[0, 0], [2, 4], [4, 2], [6, 5], [8, 1]];

// 不同张力值的曲线
c0 = cardinalspline(coords, 0) <<
    strokeColor: 'red',
    strokeWidth: 2,
    createPoints: false
>>;

c05 = cardinalspline(coords, 0.5) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    createPoints: true
>>;

c1 = cardinalspline(coords, 1) <<
    strokeColor: 'green',
    strokeWidth: 2,
    createPoints: false
>>;

// 添加图例说明
text(0.5, 5.5, "tau=0 (红色)");
text(0.5, 5, "tau=0.5 (蓝色)");
text(0.5, 4.5, "tau=1 (绿色)");
```

## 注意事项

1. **至少需要 2 个点**：创建基数样条曲线至少需要 2 个控制点
2. **张力参数范围**：通常在 0 到 1 之间，但可以超出此范围获得特殊效果
3. **曲线穿过控制点**：与贝塞尔曲线不同，基数样条曲线会精确穿过所有控制点
4. **动态更新**：当控制点移动时，曲线会自动更新
5. **坐标格式**：使用坐标数组时，注意 `isArrayOfCoordinates` 的设置
6. **性能考虑**：大量控制点可能影响渲染性能

## 相关元素

- [Curve](./Curve.md) - 曲线基类
- [Beziercurve](./Beziercurve.md) - 贝塞尔曲线
- [B-spline](./B-spline.md) - B 样条曲线
- [Functiongraph](./Functiongraph.md) - 函数图像
