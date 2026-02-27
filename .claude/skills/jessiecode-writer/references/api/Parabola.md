# Parabola 抛物线

## 描述

抛物线是一种特殊的圆锥曲线，由一个点（焦点）和一条直线（准线）定义。抛物线上的任意点到焦点的距离等于到准线的距离。

## JessieCode 语法

```js
// 通过焦点和准线创建抛物线
parabola = parabola(focus, directrix);

// 带属性创建
parabola = parabola(F, l) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| focus | Point/Array | 焦点 |
| directrix | Line/Array | 准线（直线或两点） |

### 准线参数格式

准线可以是：
- `Line` 对象
- 两个点的数组 `[[x1,y1], [x2,y2]]`

## 属性

抛物线继承自 Conic，因此拥有 Conic 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |

## 示例

### 1. 创建基本抛物线

```js
// 焦点和准线
F = point(1, 1);
A = point(-1, 4);
B = point(-1, -4);
l = line(A, B);  // 准线

parabola1 = parabola(F, l);
```

### 2. 使用坐标数组

```js
// 焦点
F = point(3.25, 0);

// 准线（通过两点定义）
directrix = [[0.25, 1], [0.25, 0]];

parabola2 = parabola(F, directrix);
```

### 3. 抛物线定义演示

```js
// 焦点
F = point(2, 0) <<
    strokeColor: 'red',
    fillColor: 'red',
    size: 5
>>;

// 准线（y 轴）
A = point(0, -5);
B = point(0, 5);
directrix = line(A, B) << dash: 1 >>;

// 抛物线
p = parabola(F, directrix);

// 抛物线上的动点
P = glider(p);

// 到焦点的距离
PF = segment(P, F) << strokeColor: 'blue' >>;

// 到准线的距离（垂线段）
PDirectrix = perpendicularsegment(directrix, P) << strokeColor: 'green' >>;

// 显示距离相等
distText = text(1, 4, function() {
    return "PF = " + dist(P, F).toFixed(2);
});
```

### 4. 动态抛物线

```js
// 可移动的焦点
F = point(2, 0);

// 固定准线
A = point(0, -4);
B = point(0, 4);
l = line(A, B);

// 动态抛物线
parabola = parabola(F, l) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 顶点（焦点到准线垂线的中点）
V = perpendicularpoint(F, l);
```

### 5. 标准抛物线 y = ax²

```js
// 抛物线 y = x²
// 焦点 (0, 1/4a)，准线 y = -1/4a
// 当 a = 1 时：焦点 (0, 0.25)，准线 y = -0.25

focus = point(0, 0.25);
directrixPoints = [[-3, -0.25], [3, -0.25]];
directrix = line(directrixPoints[0], directrixPoints[1]) << dash: 1 >>;

parabola = parabola(focus, directrix);

// 或使用函数图像
graph = functiongraph(function(x) { return x * x; }, -3, 3) <<
    strokeColor: 'red'
>>;
```

### 6. 抛物线族

```js
// 固定准线
A = point(0, -5);
B = point(0, 5);
directrix = line(A, B);

// 不同焦点的抛物线族
F1 = point(1, 0);
F2 = point(2, 0);
F3 = point(3, 0);

p1 = parabola(F1, directrix) << strokeColor: 'red' >>;
p2 = parabola(F2, directrix) << strokeColor: 'blue' >>;
p3 = parabola(F3, directrix) << strokeColor: 'green' >>;
```

### 7. 抛物线的光学性质

```js
// 抛物线反射性质：平行于轴的光线经抛物线反射后汇聚于焦点

F = point(2, 0) <<
    strokeColor: 'red',
    fillColor: 'red',
    size: 6,
    name: 'F'
>>;

A = point(0, -4);
B = point(0, 4);
l = line(A, B);

p = parabola(F, l);

// 抛物线上的点
P = glider(p);

// 入射光线（水平）
// 反射光线（指向焦点）
// 需要通过切线/法线来演示
```

### 8. 抛物线顶点

```js
// 创建抛物线
F = point(3, 0);
A = point(0, -4);
B = point(0, 4);
directrix = line(A, B);

parabola = parabola(F, directrix);

// 顶点是焦点到准线垂线段的中点
V = perpendicularpoint(F, directrix);
V = midpoint(F, V);

// 对称轴
axis = line(F, V);
```

### 9. 滑块控制抛物线

```js
// 滑块控制焦点位置
fSlider = slider([-3, 4], [4, 4], [0, 2, 5]) << name: 'f' >>;

// 固定准线
directrix = line(point(0, -5), point(0, 5));

// 动态焦点
F = point(function() { return V(fSlider); }, 0);

// 动态抛物线
dynamicParabola = parabola(F, directrix);
```

### 10. 抛体运动轨迹

```js
// 抛体运动轨迹是抛物线
// y = -ax² + bx + c

// 初始速度和角度
v0Slider = slider([1, 4], [4, 4], [5, 10, 20]) << name: 'v₀' >>;
angleSlider = slider([1, 3.5], [3.5, 3.5], [PI/6, PI/4, PI/2]) << name: 'θ' >>;

// 重力加速度
g = 9.8;

// 轨迹方程（简化，假设从原点发射）
// y = x*tan(θ) - g*x²/(2*v0²*cos²(θ))
trajectory = functiongraph(
    function(x) {
        v0 = V(v0Slider);
        theta = V(angleSlider);
        return x * tan(theta) - (g * x * x) / (2 * v0 * v0 * cos(theta) * cos(theta));
    },
    0, 10
) << strokeColor: 'red', strokeWidth: 2 >>;
```

## 注意事项

1. **几何定义**：抛物线上任意点到焦点的距离等于到准线的距离
2. **离心率**：抛物线的离心率 e = 1
3. **顶点**：焦点到准线垂线段的中点
4. **对称轴**：过焦点且垂直于准线的直线

## 相关元素

- [Conic](./Conic.md) - 圆锥曲线（父类）
- [Ellipse](./Ellipse.md) - 椭圆
- [Hyperbola](./Hyperbola.md) - 双曲线
- [Functiongraph](./Functiongraph.md) - 函数图像
