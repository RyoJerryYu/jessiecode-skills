# MinorArc 劣弧

## 描述

劣弧是圆上小于或等于 180 度（π 弧度）的圆弧部分。劣弧由圆心、半径点和角度点三个点定义，从半径点开始，逆时针绘制到角度点结束。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建劣弧
arc = minorarc(center, radiusPoint, anglePoint);

// 带属性创建
arc = minorarc(O, A, B) <<
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

**注意**：
- 劣弧从 radiusPoint 开始，逆时针绘制到 anglePoint 结束
- 劣弧的圆心角小于或等于 180 度

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `visible` | Boolean | true | 是否可见 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `Value()` | unit: String | 获取弧长或角度 |
| `Value('length')` | 无 | 获取弧长 |
| `Value('radians')` | 无 | 获取角度（弧度） |
| `Value('degrees')` | 无 | 获取角度（度） |
| `Radius()` | 无 | 获取半径 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `radius(arc)` | 获取圆弧半径 | `radius(arc)` |

## 示例

### 1. 创建基本劣弧

```js
// 三个点定义劣弧
O = point(2, 2);     // 圆心
A = point(1, 0.5);   // 半径点（起点）
B = point(3.5, 1);   // 角度点（终点）

// 创建劣弧
arc = minorarc(O, A, B);

// 设置样式
arc = minorarc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;
```

### 2. 劣弧与优弧对比

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(0, 2);  // 90 度位置

// 劣弧（小于 180 度）
minorArc = minorarc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 优弧（大于 180 度）- 相同的点，不同的弧类型
majorArc = majorarc(O, A, B) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 显示区别
text(-3, 3, "Blue: Minor Arc, Red: Major Arc");
```

### 3. 设置劣弧样式

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(1, 1.732);  // 60 度位置

// 不同样式的劣弧
arc1 = minorarc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

arc2 = minorarc(O, A, B) <<
    strokeColor: 'red',
    dash: 1,
    strokeWidth: 2
>>;

arc3 = minorarc(O, A, B) <<
    strokeColor: 'green',
    strokeWidth: 4
>>;
```

### 4. 动态劣弧

```js
// 固定圆心和半径点
O = point(0, 0);
A = point(2, 0);

// 可移动的角度点（限制在劣弧范围内）
B = point(0, 2);

// 动态劣弧
arc = minorarc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 显示角度
angleText = text(1, 3, function() {
    return "Angle: " + arc.Value('degrees').toFixed(1) + "°";
});

// 显示弧长
lengthText = text(1, 2.5, function() {
    return "Length: " + arc.Value('length').toFixed(2);
});
```

### 5. 劣弧与扇形组合

```js
// 定义点
O = point(0, 0);
A = point(2, 0);
B = point(1, 1.732);  // 60 度位置

// 劣弧
minorArc = minorarc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 扇形（填充区域）
sector = sector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.3
>>;

// 半径线
r1 = segment(O, A) << strokeColor: 'red' >>;
r2 = segment(O, B) << strokeColor: 'red' >>;
```

### 6. 获取劣弧属性

```js
O = point(0, 0);
A = point(3, 0);
B = point(0, 3);  // 90 度

arc = minorarc(O, A, B);

// 获取半径
r = arc.Radius();  // 3

// 获取弧长
len = arc.Value('length');  // 3 * PI/2

// 获取角度（弧度）
angleRad = arc.Value('radians');  // PI/2

// 获取角度（度）
angleDeg = arc.Value('degrees');  // 90

// 显示值
text(1, 4, "Radius: " + r);
text(1, 3.5, "Angle: " + angleDeg.toFixed(1) + "°");
text(1, 3, "Length: " + len.toFixed(2));
```

### 7. 同心劣弧

```js
// 共同圆心
O = point(0, 0);

// 不同半径的点
A1 = point(1, 0);
A2 = point(2, 0);
A3 = point(3, 0);

// 共同角度点
B = point(0, 2);  // 90 度位置

// 同心劣弧
arc1 = minorarc(O, A1, B) << strokeColor: 'red' >>;
arc2 = minorarc(O, A2, B) << strokeColor: 'blue' >>;
arc3 = minorarc(O, A3, B) << strokeColor: 'green' >>;
```

### 8. 圆周角定理演示（劣弧情况）

```js
// 圆
O = point(0, 0);
A = point(2, 0);
c = circle(O, A);

// 劣弧对应的圆心角
B = point(1, 1.732);  // 60 度位置
minorArc = minorarc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 圆上任意点（在优弧上）
P = point(-1, 1.732);  // 120 度位置

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

// 显示关系：圆心角 = 2 × 圆周角
text(-3, 3, "Center: " + centerAngle.Value('degrees') + "°");
text(-3, 2.5, "Inscribed: " + inscribedAngle.Value('degrees') + "°");
```

### 9. 半圆作为劣弧的特例

```js
// 圆心和半径点
O = point(0, 0);
A = point(2, 0);

// 角度点在对面（180 度）
B = point(-2, 0);

// 半圆（既是劣弧也是优弧的边界情况）
semicircle = minorarc(O, A, B) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;

// 或者使用 semicircle
semicircle2 = semicircle(O, A) <<
    strokeColor: 'blue',
    dash: 1
>>;

text(-3, 3, "180°: Boundary case");
```

### 10. 参数化劣弧

```js
// 使用曲线创建参数化劣弧
// 圆心 (0, 0)，半径 2，从 0 度到 90 度（劣弧）

// 参数方程
fx = function(t) { return 2 * cos(t); };
fy = function(t) { return 2 * sin(t); };

// 创建曲线（劣弧）
arc = curve(fx, fy, 0, PI/2);

// 或使用标准 minorarc 函数
O = point(0, 0);
A = point(2, 0);
B = point(0, 2);  // 90 度位置
arc2 = minorarc(O, A, B);
```

### 11. 等弧长的劣弧

```js
// 共同圆心
O = point(0, 0);

// 创建多个 60 度的劣弧（像切蛋糕）
A0 = point(2, 0);
A1 = point(2 * cos(PI/3), 2 * sin(PI/3));
A2 = point(2 * cos(2*PI/3), 2 * sin(2*PI/3));
A3 = point(2 * cos(PI), 2 * sin(PI));
A4 = point(2 * cos(4*PI/3), 2 * sin(4*PI/3));
A5 = point(2 * cos(5*PI/3), 2 * sin(5*PI/3));

// 6 个 60 度的劣弧
arc1 = minorarc(O, A0, A1) << strokeColor: 'red' >>;
arc2 = minorarc(O, A1, A2) << strokeColor: 'blue' >>;
arc3 = minorarc(O, A2, A3) << strokeColor: 'green' >>;
arc4 = minorarc(O, A3, A4) << strokeColor: 'orange' >>;
arc5 = minorarc(O, A4, A5) << strokeColor: 'purple' >>;
arc6 = minorarc(O, A5, A0) << strokeColor: 'pink' >>;
```

## 注意事项

1. **方向**：劣弧始终从半径点逆时针绘制到角度点
2. **角度范围**：劣弧的圆心角小于或等于 180 度
3. **与优弧区别**：劣弧小于 180 度，优弧大于 180 度
4. **半圆情况**：当角度为 180 度时，是劣弧和优弧的边界情况
5. **默认行为**：使用 `arc` 函数创建时，默认根据角度自动选择劣弧或优弧

## 相关元素

- [MajorArc](./MajorArc.md) - 优弧
- [Arc](./Arc.md) - 圆弧
- [Sector](./Sector.md) - 扇形
- [Circle](./Circle.md) - 圆
- [Semicircle](./Semicircle.md) - 半圆
