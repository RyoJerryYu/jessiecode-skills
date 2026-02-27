# Semicircle 半圆弧

## 描述

半圆弧是一种特殊的弧，由两个点定义。这两个点分别是半圆弧的起点和终点，半圆弧经过这两点并以它们的中点为圆心。

## JessieCode 语法

```js
// 基本语法 - 通过两个点创建半圆弧
semicircle = semicircle(A, B);

// 带属性创建
semicircle = semicircle(A, B) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point | 第一个点（起点） |
| point2 | Point | 第二个点（终点） |

**注意**：半圆弧以两点连线的中点为圆心，以两点距离的一半为半径绘制。

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线，3=点划线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `center` | Object | - | 圆心点属性配置 |

### center 属性

用于配置半圆弧圆心点的显示属性。

```js
semicircle = semicircle(A, B) <<
    center: <<
        visible: true,
        strokeColor: 'red',
        size: 4
    >>
>>;
```

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `visible` | Boolean | false | 是否显示圆心 |
| `strokeColor` | String | '#000000' | 圆心颜色 |
| `size` | Number | 3 | 圆心大小 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `midpoint` | 无 | 获取两点之间的中点（圆心） |
| `Value()` | unit: String | 获取弧长或角度（继承自 Arc） |
| `Value('length')` | 无 | 获取弧长 |
| `Radius()` | 无 | 获取半径 |

## 示例

### 1. 创建基本半圆弧

```js
// 通过两个点创建半圆弧
A = point(-2, 0);
B = point(2, 0);

// 创建半圆弧
sc = semicircle(A, B);
```

### 2. 设置半圆弧样式

```js
// 自定义颜色和线宽
sc1 = semicircle(A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 虚线半圆弧
sc2 = semicircle(C, D) <<
    dash: 1,
    strokeColor: 'red'
>>;

// 点线半圆弧
sc3 = semicircle(E, F) <<
    dash: 2,
    strokeColor: 'green'
>>;
```

### 3. 显示圆心

```js
// 显示圆心的半圆弧
sc = semicircle(A, B) <<
    center: <<
        visible: true,
        strokeColor: 'red',
        size: 5,
        face: 'cross'
    >>
>>;
```

### 4. 动态半圆弧

```js
// 固定点 A
A = point(-2, 0);

// 可移动的点 B
B = point(2, 0);

// 动态半圆弧
sc = semicircle(A, B);

// 显示半径
radiusText = text(-2, 3, function() {
    var r = sc.Radius();
    return "Radius: " + r.toFixed(2);
});

// 显示弧长
lengthText = text(-2, 2.5, function() {
    var len = sc.Value('length');
    return "Length: " + len.toFixed(2);
});
```

### 5. 多个半圆弧组合

```js
// 创建多个半圆弧形成图案
A = point(-3, 0);
B = point(-1, 0);
C = point(1, 0);
D = point(3, 0);

// 上方半圆弧
sc1 = semicircle(A, B) << strokeColor: 'blue' >>;
sc2 = semicircle(B, C) << strokeColor: 'green' >>;
sc3 = semicircle(C, D) << strokeColor: 'red' >>;

// 下方半圆弧（使用负方向）
sc4 = semicircle(A, C) <<
    strokeColor: 'purple',
    dash: 1
>>;
```

### 6. 半圆弧与圆的组合

```js
// 定义直径两端点
A = point(-2, 0);
B = point(2, 0);

// 半圆弧
sc = semicircle(A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 完整圆（用于对比）
O = midpoint(A, B);  // 圆心
circle = circle(O, A) <<
    strokeColor: 'gray',
    dash: 1
>>;

// 直径线段
seg = segment(A, B) <<
    strokeColor: 'black',
    strokeWidth: 2
>>;
```

### 7. 半圆弧上的动点

```js
// 基础半圆弧
A = point(-3, 0);
B = point(3, 0);
sc = semicircle(A, B);

// 在半圆弧上创建滑点
P = glider(sc);

// 连接圆心和动点
O = midpoint(A, B);
radiusLine = segment(O, P) <<
    strokeColor: 'red',
    dash: 1
>>;

// 显示角度
angleText = text(-3, 4, function() {
    // 计算动点与水平方向的夹角
    var angle = Math.atan2(P.Y() - O.Y(), P.X() - O.X());
    return "Angle: " + (angle * 180 / Math.PI).toFixed(1) + "°";
});
```

### 8. 半圆弧面积演示

```js
// 半圆弧
A = point(-2, 0);
B = point(2, 0);
sc = semicircle(A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 半圆扇形（填充区域）
O = midpoint(A, B);
sector = sector(O, A, B) <<
    fillColor: 'lightblue',
    fillOpacity: 0.3,
    arc: << visible: false >>
>>;

// 显示面积
areaText = text(-2, 3, function() {
    var r = sc.Radius();
    var area = Math.PI * r * r / 2;
    return "Area: " + area.toFixed(2);
});
```

### 9. 半圆弧变换

```js
// 原始半圆弧
A = point(-2, 0);
B = point(2, 0);
sc1 = semicircle(A, B) <<
    strokeColor: 'red'
>>;

// 创建平移变换
translate = transform(3, 0) << type: 'translate' >>;

// 变换后的半圆弧
sc2 = semicircle(sc1, translate) <<
    strokeColor: 'blue'
>>;
```

### 10. 半圆弧与切线

```js
// 半圆弧
A = point(-3, 0);
B = point(3, 0);
sc = semicircle(A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 半圆弧上的点
P = glider(sc);

// 获取圆心
O = midpoint(A, B);

// 半径线
radiusLine = segment(O, P) <<
    strokeColor: 'gray',
    dash: 1
>>;

// 切线（垂直于半径）
tangentLine = tangent(P, sc) <<
    strokeColor: 'red',
    lastArrow: true
>>;
```

## 注意事项

1. **固定形状**：半圆弧始终是以两点连线为直径的半圆，不能像普通圆弧那样调整弧度
2. **方向**：半圆弧默认向上绘制（在两点连线的上方）
3. **继承关系**：半圆弧继承自 Arc，因此可以使用 Arc 的大部分方法和属性
4. **圆心**：可以通过 `center` 属性配置是否显示圆心
5. **与圆弧区别**：圆弧需要三个点定义（圆心、半径点、角度点），而半圆弧只需要两个点

## 相关元素

- [Arc](./Arc.md) - 圆弧
- [Circle](./Circle.md) - 圆
- [Sector](./Sector.md) - 扇形
- [Midpoint](./Midpoint.md) - 中点
- [Segment](./Segment.md) - 线段
