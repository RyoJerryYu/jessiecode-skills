# Line 直线

<!-- USAGE_FREQUENCY: core -->

## 描述

直线由两个点或三个坐标定义。通过设置额外属性，直线可以用作箭头或坐标轴。

## JessieCode 语法

```js
// 通过两个点创建直线
l = line(A, B);

// 通过坐标创建直线 (ax + by + c = 0)
l = line(a, b, c);

// 带属性创建
l = line(A, B) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    dash: 1,
    withLabel: true
>>;

// 创建射线（单向无限延伸）
ray = halfline(A, B);
```

## 参数

### 方式一：两个点

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point/Array/Function | 第一个点 |
| point2 | Point/Array/Function | 第二个点 |

### 方式二：三个坐标（直线方程）

| 参数 | 类型 | 描述 |
|------|------|------|
| a | Number/Function | 直线方程系数：a*z + b*x + c*y = 0 |
| b | Number/Function | 直线方程系数 |
| c | Number/Function | 直线方程系数 |

**注意**：对于所有有限点，z 被归一化为 1，所以方程实际上是 `a + b*x + c*y = 0`

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线，3=点划线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `straightFirst` | Boolean | true | 是否在第一个点方向无限延伸 |
| `straightLast` | Boolean | true | 是否在第二个点方向无限延伸 |
| `firstArrow` | Boolean/Object | false | 是否在起点显示箭头 |
| `lastArrow` | Boolean/Object | false | 是否在终点显示箭头 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 直线名称 |

### 箭头属性

```js
// 简单箭头
l = line(A, B) << lastArrow: true >>;

// 自定义箭头
l = line(A, B) <<
    lastArrow: <<
        type: 1,
        size: 10
    >>
>>;
```

| 箭头类型 | 描述 |
|----------|------|
| `type: 1` | 标准箭头（默认） |
| `type: 2-6` | 不同样式的箭头 |
| `type: 7` | 曲线默认箭头 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `L()` | 无 | 获取直线方程的值 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `L(line)` | 获取直线方程的值 | `L(l)` |

## 示例

### 1. 创建基本直线

```js
// 通过两个点创建直线
A = point(1, 1);
B = point(4, 3);
l = line(A, B);

// 通过坐标创建直线 (x - 2y + 1 = 0)
l = line(1, -2, 1);
```

### 2. 设置直线样式

```js
// 蓝色粗线
l1 = line(A, B) <<
    strokeColor: 'blue',
    strokeWidth: 4
>>;

// 虚线
l2 = line(C, D) <<
    dash: 1,
    strokeColor: 'gray'
>>;

// 点线
l3 = line(E, F) <<
    dash: 2
>>;
```

### 3. 射线和线段

```js
// 射线（从 A 经过 B 无限延伸）
ray = halfline(A, B);

// 线段（有限长度）
seg = segment(A, B);

// 使用 straightFirst/straightLast 控制
l1 = line(A, B) <<
    straightFirst: false,
    straightLast: false
>>;  // 实际效果同 segment
```

### 4. 带箭头的直线（向量）

```js
// 末端箭头
v = line(A, B) <<
    lastArrow: true,
    strokeWidth: 3
>>;

// 两端箭头
v2 = line(C, D) <<
    firstArrow: true,
    lastArrow: true
>>;

// 自定义箭头大小
v3 = line(E, F) <<
    lastArrow: <<
        type: 1,
        size: 12
    >>
>>;
```

### 5. 坐标轴

```js
// 创建 x 轴
xAxis = line(0, 0, 1, 0) <<
    strokeColor: 'black',
    lastArrow: true,
    withLabel: true,
    name: 'x'
>>;

// 创建 y 轴
yAxis = line(0, 0, 0, 1) <<
    strokeColor: 'black',
    lastArrow: true,
    withLabel: true,
    name: 'y'
>>;
```

### 6. 动态直线

```js
// 创建滑块
a = slider(0, 5, 0.1);

// 创建一个点随滑块移动
P = point(a, 0);

// 直线随点移动
l = line(P, point(0, 1));

// 或使用函数
Q = point(function() { return a; }, 0);
```

### 7. 直线变换

```js
// 创建反射直线
mirrorLine = line(0, 0, 1, 1);

// 创建变换
reflect = transform(mirrorLine) << type: 'reflect' >>;

// 反射另一条直线
l1 = line(1, -5, 1);
l2 = line(l1, reflect);
```

### 8. 直线的交点

```js
// 创建两条直线
l1 = line(point(0, 0), point(4, 4));
l2 = line(point(0, 4), point(4, 0));

// 创建交点
P = intersection(l1, l2, 0);  // 0 表示第一个交点
```

## 注意事项

1. **无限延伸**：默认情况下直线向两端无限延伸，使用 `straightFirst: false` 和 `straightLast: false` 可以限制
2. **直线方程**：使用三坐标方式创建时，方程为 `a + b*x + c*y = 0`
3. **箭头类型**：`firstArrow` 和 `lastArrow` 可以是布尔值或对象
4. **射线**：使用 `halfline(A, B)` 创建从 A 出发经过 B 的射线

## 相关元素

- [Segment](./Segment.md) - 线段
- [Halfline](./Halfline.md) - 射线
- [Arrow](./Arrow.md) - 箭头
- [Axis](./Axis.md) - 坐标轴
- [Parallel](./Parallel.md) - 平行线
- [Perpendicular](./Perpendicular.md) - 垂线
