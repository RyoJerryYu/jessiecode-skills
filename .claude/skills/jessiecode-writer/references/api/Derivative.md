# Derivative 导数

<!-- USAGE_FREQUENCY: common -->

## 描述

导数元素用于可视化给定曲线的（数值）导数函数图像。

*定义于:* [curve.js](./src/src_base_curve.js.md)。
*继承自:* [JXG.Curve](./JXG.Curve.md)。

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
&nbsp;&nbsp;&nbsp;↳ **[JXG.Curve](./JXG.Curve.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **Derivative**

## JessieCode 语法

```js
// 创建曲线的导数
d = derivative(curve);

// 带属性创建
d = derivative(cu) <<
    strokeColor: 'red',
    strokeWidth: 2,
    dash: 1
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| curve | Curve | 需要求导的曲线对象 |

### 父元素说明

| 父元素类型 | 描述 |
|------|------|
| `JXG.Curve` | 需要生成导数的曲线 |

## 属性

导数元素继承自 [Curve](./Curve.md)，因此可以使用曲线的所有属性。

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线，3=点划线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 导数曲线名称 |

## 示例

### 1. 创建 Cardinal 样条曲线的导数

```js
// 创建 Cardinal 样条曲线
var cu = board.create('cardinalspline', [[[-3,0], [-1,2], [0,1], [2,0], [3,1]], 0.5, 'centripetal'], {createPoints: false});

// 创建导数曲线
var d = board.create('derivative', [cu], {dash: 2});
```

### 2. 设置导数曲线的样式

```js
// JessieCode 语法
// 创建样条曲线
cu = cardinalspline([[-3,0], [-1,2], [0,1], [2,0], [3,1]], 0.5, 'centripetal') << createPoints: false >>;

// 创建红色虚线导数曲线
d = derivative(cu) <<
    strokeColor: 'red',
    strokeWidth: 2,
    dash: 1
>>;
```

### 3. 函数图像的导数

```js
// 创建函数曲线
f = functiongraph(function(x) { return x^3 - 2*x^2 + x; });

// 创建导数曲线
df = derivative(f) <<
    strokeColor: 'blue',
    withLabel: true,
    name: "f'"
>>;
```

### 4. 比较原函数与导数

```js
// 原函数 - 正弦曲线
f = functiongraph(function(x) { return sin(x); }) <<
    strokeColor: 'black',
    strokeWidth: 2
>>;

// 导数 - 余弦曲线
df = derivative(f) <<
    strokeColor: 'red',
    dash: 2,
    strokeWidth: 2
>>;

// 添加图例
label1 = text(-3, 1, "f(x) = sin(x)") <<
    strokeColor: 'black'
>>;

label2 = text(-3, 0.5, "f'(x) = cos(x)") <<
    strokeColor: 'red'
>>;
```

### 5. 参数曲线的导数

```js
// 创建参数曲线
c = curve(
    function(t) { return t^2; },
    function(t) { return t^3 - t; },
    -2, 2
);

// 创建导数
dc = derivative(c) <<
    strokeColor: 'green',
    dash: 1
>>;
```

### 6. 自定义导数显示范围

```js
// 创建原曲线
f = functiongraph(function(x) { return x^4 - 4*x^2; }, -3, 3);

// 创建导数并设置范围
df = derivative(f) <<
    strokeColor: 'blue',
    minX: -3,
    maxX: 3
>>;
```

### 7. 动态导数

```js
// 创建滑块
a = slider(-2, 2, 0.1);

// 创建含参数的函数曲线
f = functiongraph(function(x) { return x^3 + a*X()*x^2; });

// 导数会随滑块动态更新
df = derivative(f) <<
    strokeColor: 'red',
    dash: 2
>>;
```

### 8. 极值点可视化

```js
// 原函数
f = functiongraph(function(x) { return x^3 - 3*x; }, -3, 3);

// 导数
df = derivative(f) <<
    strokeColor: 'gray',
    dash: 2
>>;

// 创建导数的零点（原函数的极值点）
extrema = intersection(f, df, 0);
```

## 注意事项

1. **数值求导**：导数是通过数值方法计算的，对于某些特殊函数可能存在精度问题
2. **定义域**：导数曲线的定义域与原曲线相同
3. **继承属性**：导数元素继承自 Curve，可以使用曲线的所有样式属性
4. **性能考虑**：对于复杂曲线，数值求导可能需要较多计算资源
5. **不连续点**：如果原函数在某些点不可导，导数曲线在这些点可能显示异常

## 相关元素

- [Curve](./Curve.md) - 曲线
- [FunctionGraph](./FunctionGraph.md) - 函数图像
- [CardinalSpline](./CardinalSpline.md) - Cardinal 样条
- [Intersection](./Intersection.md) - 交点
- [Tangent](./Tangent.md) - 切线
