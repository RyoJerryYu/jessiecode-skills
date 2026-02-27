# Normal 法线

<!-- USAGE_FREQUENCY: advanced -->

## 描述

法线是垂直于直线或垂直于圆、曲线的切线的直线。

*定义于:* [line.js](./src/src_base_line.js.md)
*继承自:* [JXG.Line](./JXG.Line.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
&nbsp;&nbsp;&nbsp;↳ **[JXG.Line](./JXG.Line.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **Normal**

## JessieCode 语法

```js
// 创建垂直于直线的法线
n = normal(line, point);

// 创建垂直于圆的法线
n = normal(circle, point);

// 创建垂直于曲线的法线
n = normal(curve, point);

// 使用滑点创建法线
n = normal(gliderPoint);

// 带属性创建
n = normal(line, point) <<
    strokeColor: 'red',
    strokeWidth: 2,
    dash: 1
>>;
```

## 参数

### 方式一：对象 + 点

| 参数 | 类型 | 描述 |
|------|------|------|
| o | Line/Circle/Curve/Turtle | 要垂直的对象（直线、圆、曲线或画笔） |
| p | Point | 法线经过的点，该点在对象上 |

### 方式二：滑点 (Glider)

| 参数 | 类型 | 描述 |
|------|------|------|
| p | Glider | 滑点，法线垂直于滑点所在的对象 |

**说明**：构造的直线经过点 p 且垂直于对象在该点的切线。

## 属性

法线继承自 [JXG.Line](./Line.md)，因此可以使用直线的所有属性。

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线，3=点划线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 法线名称 |

### 特殊属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `point` | Point | 法线的辅助点属性 |

## 方法

法线继承自 [JXG.Line](./Line.md)，因此可以使用直线的所有方法。

## 示例

### 1. 创建垂直于直线的法线

```js
// 创建一条直线
A = point(1, 1);
B = point(4, 3);
l = line(A, B);

// 在直线上创建一个点
P = point(2.5, 2);
P.glide(l);  // 使点 P 在直线 l 上滑动

// 创建过点 P 且垂直于直线 l 的法线
n = normal(l, P);
```

### 2. 创建垂直于圆的法线

```js
// 创建圆心和一个定义半径的点
center = point(2.0, 2.0);
radiusPoint = point(3.0, 2.0);

// 创建圆
c = circle(center, radiusPoint);

// 在圆上创建一个点
P = point(3.0, 2.0);

// 创建过点 P 且垂直于圆 c 的法线（即经过圆心的直线）
n = normal(c, P);
```

### 3. 创建垂直于曲线的法线

```js
// 创建参数曲线 (心形线)
crv = curve(
    function(t) { return 2 * cos(t) - cos(2 * t); },
    function(t) { return 2 * sin(t) - sin(2 * t); },
    0, 2 * PI
);

// 在曲线上创建一个滑点
P = glider(crv);

// 创建过点 P 且垂直于曲线 crv 的法线
n = normal(crv, P);
```

### 4. 使用滑点创建法线

```js
// 创建一条直线
A = point(-3, -3);
B = point(3, 3);
l = line(A, B);

// 在直线上创建滑点
P = glider(l);

// 直接通过滑点创建法线
n = normal(P);
```

### 5. 设置法线样式

```js
// 创建直线和滑点
A = point(0, 0);
B = point(4, 0);
l = line(A, B);
P = glider(l);

// 创建红色虚线法线
n = normal(l, P) <<
    strokeColor: 'red',
    strokeWidth: 2,
    dash: 1,
    withLabel: true,
    name: 'n'
>>;
```

### 6. 圆的法线应用

```js
// 创建圆
center = point(0, 0);
radiusPoint = point(2, 0);
c = circle(center, radiusPoint);

// 在圆上创建滑点
P = glider(c);

// 创建法线（经过圆心和点 P）
n = normal(c, P);

// 创建切线（垂直于法线）
t = tangent(c, P);
```

### 7. 动态法线演示

```js
// 创建滑块控制角度
alpha = slider(0, 2 * PI, 0.01);

// 创建单位圆
center = point(0, 0);
radiusPoint = point(1, 0);
c = circle(center, radiusPoint);

// 在圆上创建动点
P = point(function() { return cos(V(alpha)); },
          function() { return sin(V(alpha)); });

// 创建法线
n = normal(c, P);

// 创建切线
t = tangent(c, P);
```

## 注意事项

1. **法线的定义**：法线是垂直于给定对象（直线、圆、曲线）在给定点的切线的直线
2. **圆的法线**：圆上任意点的法线总是经过圆心
3. **直线的法线**：直线的法线与该直线垂直
4. **曲线的法线**：曲线在某点的法线垂直于该点的切线
5. **滑点用法**：可以直接使用滑点 (Glider) 创建法线，系统会自动获取滑点所在的对象
6. **继承关系**：Normal 继承自 JXG.Line，因此具有直线的所有属性和方法

## 相关元素

- [Line](./Line.md) - 直线
- [Tangent](./Tangent.md) - 切线
- [Perpendicular](./Perpendicular.md) - 垂线
- [Parallel](./Parallel.md) - 平行线
- [Circle](./Circle.md) - 圆
- [Curve](./Curve.md) - 曲线
- [Glider](./Glider.md) - 滑点
