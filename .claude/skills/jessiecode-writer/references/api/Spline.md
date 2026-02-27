# Spline 样条曲线

<!-- USAGE_FREQUENCY: advanced -->

## 描述

（自然）三次样条曲线（函数图像）插值一组点。创建由样本点 p_1 到 p_n 定义的动态样条插值曲线。

*定义于：* [curve.js](./src/src_base_curve.js.md)
继承自 [JXG.Curve](./JXG.Curve.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
   → **[JXG.Curve](./JXG.Curve.md)**
      → **Spline**

## JessieCode 语法

```js
// 通过点数组创建样条曲线
s = spline([P1, P2, P3, P4, P5]);

// 通过坐标数组创建
s = spline([[x1, y1], [x2, y2], [x3, y3]]);

// 使用分离的坐标数组创建
s = spline([[x1, x2, x3], [y1, y2, y3]]);

// 带属性创建
s = spline(points) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;
```

## 参数

### 方式一：点数组

| 参数 | 类型 | 描述 |
|------|------|------|
| points | Array | 点数组，样条曲线将插值这些点。可以是以下格式： |

点数组可以是以下格式：
- JSXGraph 点对象数组
- 坐标对数组
- 返回坐标对的函数数组
- 包含 x 坐标数组和 y 坐标数组的数组

坐标数组的单个条目可以是数字或返回数字的函数。

### 方式二：坐标数组

| 参数 | 类型 | 描述 |
|------|------|------|
| coordinates | Array | 坐标数组，可以是 `[[x1,y1], [x2,y2], ...]` 或 `[[x1,x2,...], [y1,y2,...]]` |

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线，3=点划线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `createPoints` | Boolean | true | 是否将数据点转换为可视的 JSXGraph 点 |
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
s = spline(coords) <<
    createPoints: true,
    points: <<
        strokeColor: 'red',
        size: 4,
        withLabel: true
    >>
>>;
```

## 示例

### 1. 创建基本样条曲线

```js
// 创建控制点
P1 = point(-2, 2) << size: 4, face: 'o' >>;
P2 = point(0, -1) << size: 4, face: 'o' >>;
P3 = point(2, 0) << size: 4, face: 'o' >>;
P4 = point(4, 1) << size: 4, face: 'o' >>;

// 创建样条曲线
s = spline([P1, P2, P3, P4]) << strokeWidth: 3 >>;
```

### 2. 使用坐标数组创建

```js
// 坐标对数组格式
coords1 = [[-2, 2], [0, -1], [2, 0], [4, 1]];
s1 = spline(coords1) << strokeColor: 'blue' >>;

// 分离的 X,Y 数组格式
coords2 = [[-2, 0, 2, 4], [2, -1, 0, 1]];
s2 = spline(coords2) <<
    strokeColor: 'red',
    isArrayOfCoordinates: false
>>;
```

### 3. 设置曲线样式

```js
// 蓝色粗曲线
s1 = spline(points) <<
    strokeColor: 'blue',
    strokeWidth: 4
>>;

// 虚线样条
s2 = spline(points) <<
    dash: 1,
    strokeColor: 'gray'
>>;

// 半透明曲线
s3 = spline(points) <<
    strokeColor: 'green',
    opacity: 0.5
>>;
```

### 4. 显示/隐藏控制点

```js
// 显示控制点（默认）
s1 = spline(coords) <<
    createPoints: true,
    points: <<
        strokeColor: 'red',
        size: 4
    >>
>>;

// 不显示控制点，只显示曲线
s2 = spline(coords) <<
    createPoints: false
>>;
```

### 5. 动态样条曲线

```js
// 创建可拖动的点
A = point(-2, 2);
B = point(0, -1);
C = point(2, 0);
D = point(4, 1);

// 曲线随点移动
s = spline([A, B, C, D]) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 拖动任意控制点，曲线会实时更新
```

### 6. 使用函数创建动态点

```js
// 创建滑块
t = slider(0, 2*PI, 0.01);

// 一个点沿圆周运动
P1 = point(-2, 2);
P2 = point(function() { return cos(V(t)); },
         function() { return sin(V(t)); });
P3 = point(2, 0);
P4 = point(4, 1);

// 样条曲线随动点变化
s = spline([P1, P2, P3, P4]);
```

### 7. 完整示例

```js
// 创建一组点
p = [];
p[0] = point(-2, 2) << size: 4, face: 'o' >>;
p[1] = point(0, -1) << size: 4, face: 'o' >>;
p[2] = point(2, 0) << size: 4, face: 'o' >>;
p[3] = point(4, 1) << size: 4, face: 'o' >>;

// 创建自然三次样条曲线
c = spline(p) << strokeWidth: 3 >>;
```

## 注意事项

1. **至少需要 2 个点**：创建样条曲线至少需要 2 个控制点
2. **自然三次样条**：默认使用自然边界条件（端点处二阶导数为 0）
3. **曲线穿过控制点**：样条曲线会精确穿过所有控制点
4. **动态更新**：当控制点移动时，曲线会自动更新
5. **坐标格式**：使用坐标数组时，注意 `isArrayOfCoordinates` 的设置
6. **继承属性**：Spline 继承自 Curve，因此可以使用所有 Curve 的属性

## 相关元素

- [Curve](./Curve.md) - 曲线基类
- [Cardinalspline](./Cardinalspline.md) - 基数样条曲线
- [Metapostspline](./Metapostspline.md) - MetaPost 样条曲线
- [Functiongraph](./Functiongraph.md) - 函数图像
- [Beziercurve](./Beziercurve.md) - 贝塞尔曲线
