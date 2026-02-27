# Tracecurve 轨迹曲线

## 描述

轨迹曲线是一种简单的_locus curve_（轨迹曲线），显示依赖于滑动点的动点所形成的运动轨迹。

*定义于：* [curve.js](./src/src_base_curve.js.md)。
*继承自：* [JXG.Curve](./JXG.Curve.md)。

## JessieCode 语法

```js
// 基本语法 - 创建轨迹曲线
curve = tracecurve(glider, tracer);

// 带属性创建
curve = tracecurve(glider, tracer) <<
    strokeColor: 'red',
    strokeWidth: 2,
    numberPoints: 200
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| glider | Point | 滑动点（在某个路径上移动的点） |
| tracer | Point | 被追踪轨迹的点（依赖于滑动点） |

**说明：**
- `glider`：滑动点，通常是在圆、线段或其他曲线上的点
- `tracer`：被追踪的点，其位置依赖于滑动点，当滑动点移动时，该点形成的轨迹被记录下来

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 轨迹曲线的描边颜色 |
| `strokeWidth` | Number | 3 | 轨迹曲线的线宽（像素） |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `numberPoints` | Number | 100 | 评估的数据点数量 |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线 |

### 专用属性

#### numberPoints

评估的数据点数量，控制轨迹曲线的精细程度。

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `numberPoints` | Number | 100 | 轨迹曲线上采样的点数 |

**说明：** 数值越大，轨迹曲线越平滑，但计算量也越大。

```js
// 使用更多采样点获得更平滑的轨迹
curve = tracecurve(glider, tracer) <<
    numberPoints: 200
>>;
```

## 示例

### 1. 基本轨迹曲线

```js
// 创建一个圆
c1 = circle([0, 0], [2, 0]);

// 创建一个固定点
p1 = point(-3, 1);

// 创建圆上的滑动点
g1 = glider(2, 1, c1);

// 连接滑动点和固定点的线段
s1 = segment(g1, p1);

// 线段的中点
p2 = midpoint(s1);

// 创建中点的轨迹曲线
curve = tracecurve(g1, p2);
```

### 2. 设置轨迹样式

```js
// 红色轨迹
c1 = circle([0, 0], [3, 0]);
g1 = glider(3, 0, c1);
p1 = point(-3, 0);
s1 = segment(g1, p1);
p2 = midpoint(s1);

curve = tracecurve(g1, p2) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;

// 虚线轨迹
curve2 = tracecurve(g1, p2) <<
    strokeColor: 'blue',
    dash: 1
>>;
```

### 3. 椭圆轨迹

```js
// 创建两个同心圆
c1 = circle([0, 0], 3);
c2 = circle([0, 0], 2);

// 在大圆上的滑动点
g1 = glider(3, 0, c1);

// 创建从原点到滑动点的射线
r1 = halfline([0, 0], g1);

// 射线与小圆的交点
i1 = intersection(r1, c2, 0);

// 创建椭圆轨迹点
p1 = point(function() { return X(i1); },
           function() { return Y(g1); });

// 轨迹曲线
curve = tracecurve(g1, p1) <<
    strokeColor: 'green',
    strokeWidth: 2
>>;
```

### 4. 使用滑块控制

```js
// 创建滑块控制滑动点位置
t = slider(0, 2*PI, 0.01);

// 参数曲线上的点
c1 = circle([0, 0], [2, 0]);
g1 = point(function() { return 2*cos(V(t)); },
           function() { return 2*sin(V(t)); });

// 追踪点
p1 = point(0, 0);
s1 = segment(g1, p1);
m1 = midpoint(s1);

// 创建轨迹
curve = tracecurve(g1, m1) <<
    numberPoints: 150
>>;
```

### 5. 心脏线轨迹

```js
// 基圆
baseCircle = circle([0, 0], [1, 0]);

// 滚动圆
rollingCircle = circle([2, 0], [3, 0]);

// 滑动点在基圆上
gliderPoint = glider(1, 0, baseCircle);

// 追踪点（在滚动圆上）
tracerPoint = point(function() {
    var angle = X(gliderPoint);
    return [3*cos(angle) - cos(3*angle),
            3*sin(angle) - sin(3*angle)];
});

// 心脏线轨迹
cardioid = tracecurve(gliderPoint, tracerPoint) <<
    strokeColor: 'purple',
    strokeWidth: 2,
    numberPoints: 200
>>;
```

## 注意事项

1. **需要滑动点**：轨迹曲线必须依赖于一个滑动点（glider），滑动点在其他几何对象上移动
2. **性能考虑**：`numberPoints` 值越大轨迹越平滑，但会增加计算负担，默认值 100 通常足够
3. **动态更新**：当滑动点移动时，轨迹曲线会自动更新
4. **依赖关系**：确保追踪点（tracer）确实依赖于滑动点，否则轨迹可能没有意义
5. **与 Curve 的区别**：`tracecurve` 专门用于创建轨迹，而 `curve` 用于创建一般参数曲线

## 相关元素

- [Curve](./Curve.md) - 一般曲线
- [Glider](./Glider.md) - 滑动点
- [Circle](./Circle.md) - 圆
- [Segment](./Segment.md) - 线段
- [Midpoint](./Midpoint.md) - 中点
- [Locus](./Locus.md) - 轨迹（如果存在）
