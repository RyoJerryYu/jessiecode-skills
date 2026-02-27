# Arrow 箭头

## 描述

箭头是带箭头的线段。本质上是 [Line](./Line.md) 元素的封装，将 `straightFirst` 和 `straightLast` 属性设为 `false`，并将 `lastArrow` 设为 `true`。

## JessieCode 语法

```js
// 基本语法 - 通过两个点创建箭头
a = arrow(A, B);

// 通过坐标创建箭头
a = arrow(x1, y1, x2, y2);

// 带属性创建
a = arrow(A, B) <<
    strokeColor: 'red',
    strokeWidth: 3,
    lastArrow: <<
        type: 1,
        size: 12
    >>
>>;
```

## 参数

### 方式一：两个点

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point/Array | 第一个点（起点） |
| point2 | Point/Array | 第二个点（终点） |

### 方式二：四个坐标

| 参数 | 类型 | 描述 |
|------|------|------|
| x1 | Number | 起点 x 坐标 |
| y1 | Number | 起点 y 坐标 |
| x2 | Number | 终点 x 坐标 |
| y2 | Number | 终点 y 坐标 |

## 属性

Arrow 元素继承 [Line](./Line.md) 的所有属性，常用属性如下：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `lastArrow` | Boolean/Object | true | 是否在终点显示箭头 |
| `firstArrow` | Boolean/Object | false | 是否在起点显示箭头 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 箭头名称 |
| `id` | String | 自动生成 | 元素的唯一 ID |

### 箭头属性 (lastArrow / firstArrow)

```js
// 简单箭头
a = arrow(A, B) << lastArrow: true >>;

// 自定义箭头
a = arrow(A, B) <<
    lastArrow: <<
        type: 1,
        size: 12
    >>
>>;
```

| 箭头类型 | 描述 |
|----------|------|
| `type: 1` | 标准箭头（默认） |
| `type: 2-6` | 不同样式的箭头 |
| `type: 7` | 曲线默认箭头 |

| 属性 | 类型 | 描述 |
|------|------|------|
| `type` | Number | 箭头样式类型 |
| `size` | Number | 箭头大小 |

## 方法

Arrow 元素继承 [Line](./Line.md) 的所有方法。

## 示例

### 1. 创建基本箭头

```js
// 通过两个点创建箭头
A = point(1, 1);
B = point(4, 3);
a = arrow(A, B);

// 通过坐标创建箭头
a2 = arrow(0, 0, 3, 2);
```

### 2. 设置箭头样式

```js
// 红色粗箭头
a1 = arrow(A, B) <<
    strokeColor: 'red',
    strokeWidth: 4
>>;

// 蓝色箭头
a2 = arrow(C, D) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 带透明度的箭头
a3 = arrow(E, F) <<
    strokeColor: 'green',
    opacity: 0.5
>>;
```

### 3. 自定义箭头大小

```js
// 大箭头
a1 = arrow(A, B) <<
    lastArrow: <<
        type: 1,
        size: 15
    >>
>>;

// 小箭头
a2 = arrow(C, D) <<
    lastArrow: <<
        type: 1,
        size: 8
    >>
>>;
```

### 4. 双向箭头

```js
// 两端都有箭头
a = arrow(A, B) <<
    firstArrow: true,
    lastArrow: true
>>;

// 自定义两端箭头
a2 = arrow(C, D) <<
    firstArrow: <<
        type: 1,
        size: 10
    >>,
    lastArrow: <<
        type: 2,
        size: 12
    >>
>>;
```

### 5. 带标签的箭头

```js
// 显示箭头名称
a = arrow(A, B) <<
    withLabel: true,
    name: 'v'
>>;

// 自定义标签
a2 = arrow(C, D) <<
    withLabel: true,
    name: '向量 AB'
>>;
```

### 6. 动态箭头

```js
// 创建滑块
t = slider(0, 2*PI, 0.01);

// 创建动点
P = point(function() { return cos(V(t)); },
          function() { return sin(V(t)); });

// 箭头指向动点
O = point(0, 0);
a = arrow(O, P);
```

### 7. 向量表示

```js
// 原点
O = point(0, 0);

// 向量终点
A = point(3, 2);

// 用箭头表示向量
v = arrow(O, A) <<
    strokeColor: 'blue',
    strokeWidth: 3,
    lastArrow: <<
        type: 1,
        size: 12
    >>,
    withLabel: true,
    name: 'v'
>>;
```

### 8. 多个箭头

```js
// 创建多个点
A = point(1, 1);
B = point(3, 2);
C = point(5, 1);

// 创建箭头链
a1 = arrow(A, B) << strokeColor: 'red' >>;
a2 = arrow(B, C) << strokeColor: 'blue' >>;
a3 = arrow(A, C) << strokeColor: 'green', dash: 1 >>;
```

## 注意事项

1. **箭头方向**：默认箭头指向第二个点（终点），使用 `lastArrow: true`
2. **双向箭头**：同时设置 `firstArrow: true` 和 `lastArrow: true` 可创建双向箭头
3. **与 Line 的区别**：Arrow 是 Line 的特殊形式，自动设置 `straightFirst: false` 和 `straightLast: false`
4. **箭头样式**：使用 `type` 属性选择不同的箭头样式，`size` 属性控制箭头大小

## 相关元素

- [Line](./Line.md) - 直线
- [Segment](./Segment.md) - 线段
- [Halfline](./Halfline.md) - 射线
- [Point](./Point.md) - 点
