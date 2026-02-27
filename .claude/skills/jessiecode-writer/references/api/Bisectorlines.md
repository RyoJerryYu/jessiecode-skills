# Bisectorlines 角平分线

<!-- USAGE_FREQUENCY: advanced -->

## 描述

角平分线由两条相交直线定义，生成两条相互垂直的角平分线。这两条角平分线将两条原始直线所形成的四个角各自平分。

## JessieCode 语法

```js
// 基本语法 - 创建两条直线的角平分线
bl = bisectorlines(l1, l2);

// 带属性创建
bl = bisectorlines(l1, l2) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    dash: 1
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| l1 | Line | 第一条直线 |
| l2 | Line | 第二条直线 |

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线，3=点划线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 元素名称 |

### 子元素属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `line1` | Object | 第一条角平分线的属性 |
| `line2` | Object | 第二条角平分线的属性 |

```js
// 分别设置两条角平分线的样式
bl = bisectorlines(l1, l2) <<
    line1: <<
        strokeColor: 'red',
        dash: 1
    >>,
    line2: <<
        strokeColor: 'blue',
        dash: 2
    >>
>>;
```

## 示例

### 1. 创建基本角平分线

```js
// 创建四个点
p1 = point(6.0, 4.0);
p2 = point(3.0, 2.0);
p3 = point(1.0, 7.0);
p4 = point(3.0, 0.0);

// 创建两条直线
l1 = line(p1, p2);
l2 = line(p3, p4);

// 创建角平分线
bl = bisectorlines(l1, l2);
```

### 2. 设置角平分线样式

```js
// 创建相交直线
A = point(0, 0);
B = point(4, 4);
C = point(4, 0);
D = point(0, 4);

l1 = line(A, B);
l2 = line(C, D);

// 红色角平分线
bl = bisectorlines(l1, l2) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;
```

### 3. 分别设置两条角平分线

```js
// 创建两条相交直线
l1 = line(point(0, 0), point(5, 0));
l2 = line(point(0, 0), point(3, 4));

// 角平分线 - 不同的样式
bl = bisectorlines(l1, l2) <<
    line1: <<
        strokeColor: 'blue',
        dash: 1,
        withLabel: true,
        name: 'b1'
    >>,
    line2: <<
        strokeColor: 'green',
        dash: 2,
        withLabel: true,
        name: 'b2'
    >>
>>;
```

### 4. 动态角平分线

```js
// 创建可拖动的点
A = point(1, 1);
B = point(4, 3);
C = point(2, 5);

// 创建两条直线
l1 = line(A, B);
l2 = line(A, C);

// 创建角平分线
bl = bisectorlines(l1, l2) <<
    strokeColor: 'red',
    visible: true
>>;

// 拖动点 A、B、C 时，角平分线会自动更新
```

### 5. 角平分线与三角形

```js
// 创建三角形顶点
A = point(1, 1);
B = point(5, 1);
C = point(3, 4);

// 创建三角形的边
a = line(B, C);
b = line(A, C);
c = line(A, B);

// 创建角 A 的角平分线
blA = bisectorlines(b, c) <<
    strokeColor: 'red',
    line1: << visible: false >>  // 只显示一条角平分线
>>;

// 创建角 B 的角平分线
blB = bisectorlines(a, c) <<
    strokeColor: 'blue',
    line1: << visible: false >>
>>;
```

### 6. 垂直直线的角平分线

```js
// 创建两条垂直直线
l1 = line(point(0, 0), point(4, 0));  // 水平线
l2 = line(point(0, 0), point(0, 4));  // 垂直线

// 角平分线是 y = x 和 y = -x
bl = bisectorlines(l1, l2) <<
    strokeColor: 'purple',
    strokeWidth: 2
>>;
```

## 注意事项

1. **两条角平分线**：`bisectorlines` 总是生成两条相互垂直的角平分线
2. **直线必须相交**：两条输入直线应该相交，否则无法定义角平分线
3. **复合元素**：角平分线是一个复合元素，由两条直线组成
4. **单独样式**：可以使用 `line1` 和 `line2` 属性分别设置两条角平分线的样式
5. **与 Bisector 的区别**：`bisector` 由三个点定义（角的顶点和两边上的点），而 `bisectorlines` 由两条直线定义

## 相关元素

- [Bisector](./Bisector.md) - 角平分线（三点定义）
- [Line](./Line.md) - 直线
- [Perpendicular](./Perpendicular.md) - 垂线
- [Parallel](./Parallel.md) - 平行线
- [Angle](./Angle.md) - 角度
