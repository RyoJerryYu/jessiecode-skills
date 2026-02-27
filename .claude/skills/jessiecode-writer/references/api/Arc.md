# Arc 圆弧

<!-- USAGE_FREQUENCY: core -->

## 描述

圆弧是圆周的一部分。它由圆心、半径点和角度点三个点定义。圆弧始终从半径点逆时针绘制到角度点。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建圆弧
arc = arc(center, radiusPoint, anglePoint);

// 带属性创建
arc = arc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| center | Point | 圆心 |
| radiusPoint | Point | 半径点（定义半径和起点） |
| anglePoint | Point | 角度点（定义终点） |

**注意**：圆弧从 radiusPoint 开始，逆时针绘制到 anglePoint 结束。

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `visible` | Boolean | true | 是否可见 |
| `selection` | String | 'auto' | 弧的类型：'minor', 'major', 'auto' |
| `center` | Object | - | 圆心属性 |
| `radiusPoint` | Object | - | 半径点属性 |
| `anglePoint` | Object | - | 角度点属性 |

### 弧的类型 (selection)

| 值 | 描述 |
|----|------|
| `'minor'` | 劣弧（小于半圆） |
| `'major'` | 优弧（大于半圆） |
| `'auto'` | 自动选择（默认） |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `Value()` | unit: String | 获取弧长或角度 |
| `Value('length')` | 无 | 获取弧长 |
| `Value('radians')` | 无 | 获取角度（弧度） |
| `Value('degrees')` | 无 | 获取角度（度） |
| `Radius()` | 无 | 获取半径 |
| `hasPointSector(x, y)` | x, y: Number | 检查点是否在扇形内 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `radius(arc)` | 获取圆弧半径 | `radius(arc)` |

## 示例

### 1. 创建基本圆弧

```js
// 三个点定义圆弧
O = point(2, 2);     // 圆心
A = point(1, 0.5);   // 半径点（起点）
B = point(3.5, 1);   // 角度点（终点）

// 创建圆弧
arc = arc(O, A, B);

// 显示弧长
text(1, 6, "Arc length: " + arc.Value('length').toFixed(2));
```

### 2. 设置圆弧样式

```js
// 自定义颜色和线宽
arc1 = arc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 虚线圆弧
arc2 = arc(O, C, D) <<
    dash: 1,
    strokeColor: 'red'
>>;
```

### 3. 劣弧与优弧

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(0, 2);

// 劣弧（默认）
minorArc = arc(O, A, B) <<
    selection: 'minor',
    strokeColor: 'blue'
>>;

// 优弧
majorArc = arc(O, A, B) <<
    selection: 'major',
    strokeColor: 'red'
>>;
```

### 4. 动态圆弧

```js
// 固定圆心和半径点
O = point(0, 0);
A = point(2, 0);

// 可移动的角度点
B = point(0, 2);

// 动态圆弧
arc = arc(O, A, B);

// 显示角度
angleText = text(1, 3, function() {
    return "Angle: " + arc.Value('degrees').toFixed(1) + "°";
});

// 显示弧长
lengthText = text(1, 2.5, function() {
    return "Length: " + arc.Value('length').toFixed(2);
});
```

### 5. 圆弧与扇形的组合

```js
// 定义点
O = point(0, 0);
A = point(2, 0);
B = point(1, 1.732);  // 60 度位置

// 圆弧
arc = arc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 扇形（填充区域）
sector = sector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.3,
    arc: << visible: false >>
>>;

// 半径线
r1 = segment(O, A) << strokeColor: 'red' >>;
r2 = segment(O, B) << strokeColor: 'red' >>;
```

### 6. 获取圆弧属性

```js
O = point(0, 0);
A = point(3, 0);
B = point(0, 3);  // 90 度

arc = arc(O, A, B);

// 获取半径
r = arc.Radius();  // 3

// 获取弧长（默认）
len1 = arc.Value();  // 3 * PI/2

// 获取弧长（显式）
len2 = arc.Value('length');

// 获取角度（弧度）
angleRad = arc.Value('radians');  // PI/2

// 获取角度（度）
angleDeg = arc.Value('degrees');  // 90

// 获取角度（半圆单位）
angleSemi = arc.Value('semicircle');  // 0.5

// 获取角度（全圆单位）
angleFull = arc.Value('circle');  // 0.25
```

### 7. 同心圆弧

```js
// 共同圆心
O = point(0, 0);

// 不同半径的点
A1 = point(1, 0);
A2 = point(2, 0);
A3 = point(3, 0);

// 共同角度点
B = point(0, 1);  // 90 度

// 同心圆弧
arc1 = arc(O, A1, B) << strokeColor: 'red' >>;
arc2 = arc(O, A2, B) << strokeColor: 'blue' >>;
arc3 = arc(O, A3, B) << strokeColor: 'green' >>;
```

### 8. 圆弧变换

```js
// 原始圆弧
arc1 = arc(point(1, 1), point(0, 1), point(1, 0)) <<
    strokeColor: 'red'
>>;

// 创建缩放变换
scale = transform(2, 2) << type: 'scale' >>;

// 变换后的圆弧
arc2 = curve(arc1, scale) <<
    strokeColor: 'blue'
>>;
```

### 9. 圆周角演示

```js
// 圆
O = point(0, 0);
A = point(2, 0);
c = circle(O, A);

// 圆弧（圆心角对应的弧）
B = point(0, 2);
arc = arc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 圆上任意点（圆周角顶点）
P = glider(c);

// 圆心角
centerAngle = angle(A, O, B) <<
    radius: 0.5,
    fillColor: 'lightblue'
>>;

// 圆周角
inscribedAngle = angle(A, P, B) <<
    radius: 0.5,
    fillColor: 'lightgreen'
>>;

// 显示关系
text(-2, 2.5, "Center: " + centerAngle.Value('degrees') + "°");
text(-2, 2, "Inscribed: " + inscribedAngle.Value('degrees') + "°");
```

### 10. 参数化圆弧

```js
// 使用曲线创建参数化圆弧
// 圆心 (0, 0)，半径 2，从 0 度到 120 度

// 参数方程
fx = function(t) { return 2 * cos(t); };
fy = function(t) { return 2 * sin(t); };

// 创建曲线（圆弧）
arc = curve(fx, fy, 0, 2*PI/3);

// 或使用标准 arc 函数
O = point(0, 0);
A = point(2, 0);
B = point(-1, 1.732);  // 120 度位置
arc2 = arc(O, A, B);
```

## 注意事项

1. **方向**：圆弧始终从半径点逆时针绘制到角度点
2. **角度范围**：当角度点与半径点重合时，可能绘制完整圆或无弧线
3. **选择类型**：使用 `selection` 属性可以强制绘制劣弧或优弧
4. **曲线长度**：圆弧的曲线长度为 6
5. **与扇形区别**：圆弧只有边框，扇形有填充区域

## 相关元素

- [Sector](./Sector.md) - 扇形
- [Circle](./Circle.md) - 圆
- [Angle](./Angle.md) - 角度
- [Curve](./Curve.md) - 曲线
