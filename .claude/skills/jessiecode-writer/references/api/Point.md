# Point 点

<!-- USAGE_FREQUENCY: core -->

## 描述

点是最基本的几何元素。可以创建自由点或固定点。

## JessieCode 语法

```js
// 基本语法 - 创建自由点
A = point(x, y);

// 创建固定点
P = point(3, 5);

// 使用函数创建约束点
Q = point(1, function() { return A.X(); });

// 带属性创建
A = point(1, 2) <<
    strokeColor: 'red',
    fillColor: 'black',
    size: 5,
    face: '[]',
    withLabel: true,
    name: 'A'
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number/Function | x 坐标（数字或返回数字的函数） |
| y | Number/Function | y 坐标（数字或返回数字的函数） |

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小（像素或用户坐标） |
| `sizeUnit` | String | 'screen' | 大小单位：'screen' 或 'user' |
| `face` | String | 'circle' | 点的样式 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 点的名称 |
| `id` | String | 自动生成 | 元素的唯一 ID |
| `visible` | Boolean | true | 是否可见 |
| `fixed` | Boolean | false | 是否固定（不可拖动） |
| `showInfobox` | Boolean | true | 是否显示信息框 |

### 点的样式 (face)

| 输入值 | 外观 |
|--------|------|
| `cross` | × |
| `circle` | ○ |
| `square` 或 `[]` | □ |
| `plus` | ＋ |
| `minus` | － |
| `diamond` | ◇ |
| `triangleup` 或 `^` | △ |
| `triangledown` 或 `v` | ▽ |
| `triangleleft` 或 `<` | ◁ |
| `triangleright` 或 `>` | ▷ |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `X()` | 无 | 获取 x 坐标 |
| `Y()` | 无 | 获取 y 坐标 |
| `move(dx, dy)` | dx, dy: Number | 移动点 |
| `glide(line)` | line: Line | 使点在直线上滑动 |
| `free()` | 无 | 释放点 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `X(P)` | 获取点 P 的 x 坐标 | `X(A)` |
| `Y(P)` | 获取点 P 的 y 坐标 | `Y(A)` |
| `dist(P, Q)` | 计算两点距离 | `dist(A, B)` |

## 示例

### 1. 创建基本点

```js
// 自由点 - 可以用鼠标拖动
A = point(1, 2);

// 固定点
B = point(3, 4) << fixed: true >>;
```

### 2. 设置点的样式

```js
// 红色大圆点
C = point(0, 0) <<
    strokeColor: 'red',
    fillColor: 'pink',
    size: 8,
    face: 'circle'
>>;

// 方形点
D = point(2, 2) <<
    face: '[]',
    size: 6
>>;

// 三角形点
E = point(-2, 2) <<
    face: '^',
    size: 6
>>;
```

### 3. 带标签的点

```js
// 显示标签
P = point(1, 1) <<
    withLabel: true,
    name: 'P'
>>;

// 自定义标签名称
Q = point(2, 2) <<
    withLabel: true,
    name: 'Q(2,2)'
>>;
```

### 4. 约束点

```js
// 点 B 的 y 坐标跟随点 A
A = point(1, 2);
B = point(3, function() { return A.Y(); });

// 点 C 在函数图像上
C = point(2, function() { return 2 * C.X() + 1; });
```

### 5. 点的吸附功能

```js
// 吸附到网格
G = point(1.3, 2.7) <<
    snapToGrid: true,
    snapSizeX: 1,
    snapSizeY: 1
>>;

// 吸附到其他点
H = point(0, 0) <<
    snapToPoints: true,
    attractorDistance: 0.5
>>;
```

### 6. 访问点的坐标

```js
A = point(3, 4);

// 使用全局函数
x1 = X(A);  // 3
y1 = Y(A);  // 4

// 使用元素方法
x2 = A.X();  // 3
y2 = A.Y();  // 4

// 计算距离
d = dist(A, B);
```

### 7. 动点

```js
// 创建滑块
t = slider(0, 2*PI, 0.01);

// 创建在圆上运动的点
P = point(function() { return cos(V(t)); },
          function() { return sin(V(t)); });
```

## 注意事项

1. **坐标可以是函数**：点的坐标可以是返回数字的函数，用于创建约束点
2. **大小单位**：`sizeUnit: 'screen'` 表示像素，`sizeUnit: 'user'` 表示用户坐标
3. **点的样式**：使用 `face` 属性设置点的外观
4. **信息框**：鼠标悬停时显示坐标信息，可通过 `showInfobox: false` 禁用

## 相关元素

- [Glider](./Glider.md) - 滑点
- [Midpoint](./Midpoint.md) - 中点
- [Intersection](./Intersection.md) - 交点
