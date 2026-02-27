# Circle 圆

<!-- USAGE_FREQUENCY: core -->

## 描述

圆由圆心和半径定义。半径可以是数字、点、线段或另一个圆。

## JessieCode 语法

```js
// 通过圆心和半径（数字）创建
c = circle(center, radius);

// 通过圆心和圆周上的点创建
c = circle(center, pointOnCircle);

// 带属性创建
c = circle(O, A) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    dash: 1
>>;
```

## 参数

| 参数组合 | 类型 | 描述 |
|----------|------|------|
| center, radius | Point, Number | 圆心和半径（数字） |
| center, point | Point, Point | 圆心和圆周上的点 |
| center, line | Point, Line | 圆心和线段（线段长度为半径） |
| center, circle | Point, Circle | 圆心和另一个圆（使用其半径） |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `fillOpacity` | Number | 0.0 | 填充透明度 (0-1) |
| `dash` | Number | 0 | 虚线样式 |
| `opacity` | Number | 1.0 | 透明度 |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 圆名称 |
| `center` | Object | - | 圆心属性设置 |
| `point2` | Object | - | 圆周上点的属性设置 |

### 圆心属性

```js
// 显示圆心
c = circle(O, A) <<
    center: <<
        visible: true,
        strokeColor: 'red',
        size: 5
    >>
>>;
```

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `Radius()` | 无 | 获取半径 |
| `X()` | 无 | 获取圆心 x 坐标 |
| `Y()` | 无 | 获取圆心 y 坐标 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `radius(circle)` | 获取圆的半径 | `radius(c)` |
| `area(circle)` | 获取圆的面积 | `area(c)` |
| `perimeter(circle)` | 获取圆的周长 | `perimeter(c)` |

## 示例

### 1. 创建基本圆

```js
// 圆心和圆周上的点
O = point(0, 0);
A = point(2, 0);
c = circle(O, A);

// 圆心和半径（数字）
c = circle(O, 3);

// 直接使用坐标
c = circle(point(1, 1), 2);
```

### 2. 设置圆的样式

```js
// 蓝色圆
c1 = circle(O, A) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 虚线圆
c2 = circle(O, B) <<
    dash: 1,
    strokeColor: 'gray'
>>;

// 填充圆（圆环）
c3 = circle(O, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.3,
    strokeColor: 'orange',
    strokeWidth: 3
>>;
```

### 3. 显示圆心

```js
// 显示圆心
c = circle(O, A) <<
    center: <<
        visible: true,
        strokeColor: 'red',
        fillColor: 'black',
        size: 5,
        face: '[]'
    >>
>>;

// 或创建后单独设置
c = circle(O, A);
c.center.visible = true;
c.center.strokeColor = 'red';
```

### 4. 使用线段作为半径

```js
// 创建线段
A = point(2, 0);
B = point(3, 0);
seg = segment(A, B);

// 使用线段长度作为半径
O = point(0, 0);
c = circle(O, seg);
```

### 5. 同心圆

```js
// 共同圆心
O = point(0, 0);

// 创建多个同心圆
c1 = circle(O, 1) << strokeColor: 'red' >>;
c2 = circle(O, 2) << strokeColor: 'blue' >>;
c3 = circle(O, 3) << strokeColor: 'green' >>;
```

### 6. 动态圆

```js
// 创建滑块
r = slider(0, 5, 0.1);

// 固定圆心，半径可变
O = point(0, 0);
c = circle(O, function() { return V(r); });

// 或使用点作为半径
P = point(3, 0);
c = circle(O, P);
// 移动 P 点可以改变圆的大小
```

### 7. 从另一个圆创建

```js
// 原圆
c1 = circle(point(0, 0), 2);

// 相同半径的新圆
c2 = circle(point(4, 0), c1);

// 或使用函数获取半径
c3 = circle(point(8, 0), function() { return radius(c1); });
```

### 8. 圆与变换

```js
// 创建反射直线
mirror = line(0, 0, 1, 0);  // x 轴

// 创建反射变换
reflect = transform(mirror) << type: 'reflect' >>;

// 原圆
c1 = circle(point(1, 2), 1);

// 反射后的圆
c2 = circle(c1, reflect);
```

### 9. 获取圆的属性

```js
c = circle(point(2, 3), 4);

// 获取半径
r = radius(c);  // 4

// 获取面积
a = area(c);  // π * 16

// 获取周长
p = perimeter(c);  // 2 * π * 4

// 使用元素方法
r2 = c.Radius();  // 4
x = c.X();  // 2
y = c.Y();  // 3
```

### 10. 圆与其他元素的组合

```js
// 圆和内接多边形
O = point(0, 0);
A = point(2, 0);
c = circle(O, A);

// 创建正六边形的顶点
for (i = 0; i < 6; i = i + 1) {
    angle = i * PI / 3;
    point(cos(angle) * 2, sin(angle) * 2);
}
```

## 注意事项

1. **半径取绝对值**：如果半径是负数，会自动取绝对值
2. **填充圆**：设置 `fillColor` 和 `fillOpacity` 可以创建填充圆（圆环）
3. **动态半径**：半径可以是函数，用于创建动态圆
4. **圆心属性**：通过 `center` 属性可以控制圆心的显示和样式

## 相关元素

- [Arc](./Arc.md) - 圆弧
- [Sector](./Sector.md) - 扇形
- [Circumcircle](./Circumcircle.md) - 外接圆
- [Incircle](./Incircle.md) - 内切圆
- [Semicircle](./Semicircle.md) - 半圆
