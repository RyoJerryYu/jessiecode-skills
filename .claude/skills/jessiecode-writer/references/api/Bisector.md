# Bisector 角平分线

## 描述

角平分线是一条将角分成两个相等角度的直线。它由三个点 A、B、C 定义，平分角 ABC。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建角平分线
b = bisector(A, B, C);

// 带属性创建
b = bisector(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    withLabel: true
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point | 角的第一边上的点 |
| point2 | Point | 角的顶点（角平分线经过此点） |
| point3 | Point | 角的第二边上的点 |

**注意**：角平分线平分的是由点 point1、point2、point3 构成的角，即角 point1-point2-point3

## 属性

角平分线继承自 [Line](./Line.md)，因此支持所有直线属性。

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 角平分线名称 |

### 特殊属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `point` | Object | 角平分线辅助点的属性配置 |

## 示例

### 1. 创建基本角平分线

```js
// 定义三个点
A = point(6, 4);
B = point(3, 2);  // 顶点
C = point(1, 7);

// 创建角平分线（平分角 ABC）
b = bisector(A, B, C);
```

### 2. 设置角平分线样式

```js
A = point(0, 0);
B = point(2, 2);  // 顶点
C = point(4, 0);

// 蓝色虚线角平分线
b = bisector(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    dash: 1,
    withLabel: true,
    name: 'b'
>>;
```

### 3. 三角形内角平分线

```js
// 创建三角形三个顶点
A = point(0, 0);
B = point(5, 0);
C = point(2, 4);

// 创建三条边的角平分线
bA = bisector(B, A, C) << strokeColor: 'red' >>;    // 角 A 的平分线
bB = bisector(A, B, C) << strokeColor: 'green' >>;  // 角 B 的平分线
bC = bisector(A, C, B) << strokeColor: 'blue' >>;   // 角 C 的平分线

// 三条角平分线交于一点（内心）
```

### 4. 动态角平分线

```js
// 创建可拖动的点
A = point(1, 1);
B = point(3, 2);  // 顶点
C = point(5, 1);

// 角平分线随点移动而动态更新
b = bisector(A, B, C) <<
    strokeColor: 'orange',
    strokeWidth: 3
>>;
```

### 5. 角平分线定理演示

```js
// 创建三角形
A = point(0, 0);
B = point(6, 0);
C = point(2, 5);

// 角 A 的平分线
b = bisector(B, A, C) << strokeColor: 'red' >>;

// 创建边 BC
a = segment(B, C) << strokeColor: 'gray' >>;

// 角平分线与对边的交点
D = intersection(b, a, 0);

// 根据角平分线定理：BD/DC = AB/AC
```

## 注意事项

1. **点的顺序**：三个点的顺序很重要，第二个点是角的顶点
2. **继承直线**：角平分线本质是直线，继承所有直线属性和方法
3. **动态更新**：当三个点中的任意一个被拖动时，角平分线会自动更新
4. **辅助点**：角平分线内部会创建一个辅助点来确定方向

## 相关元素

- [Line](./Line.md) - 直线
- [Segment](./Segment.md) - 线段
- [Angle](./Angle.md) - 角
- [Triangle](./Triangle.md) - 三角形
- [Intersection](./Intersection.md) - 交点
