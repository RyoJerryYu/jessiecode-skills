# MajorArc 优弧

## 描述

优弧是圆上大于或等于 180 度（π 弧度）的圆弧部分。优弧由圆心、半径点和角度点三个点定义，从半径点开始，逆时针绘制到角度点结束。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建优弧
arc = majorarc(center, radiusPoint, anglePoint);

// 带属性创建
arc = majorarc(O, A, B) <<
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
- 优弧从 radiusPoint 开始，逆时针绘制到 anglePoint 结束
- 优弧的圆心角大于或等于 180 度

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

### 1. 创建基本优弧

```js
// 三个点定义优弧
O = point(2, 2);     // 圆心
A = point(1, 0.5);   // 半径点（起点）
B = point(3.5, 1);   // 角度点（终点）

// 创建优弧
arc = majorarc(O, A, B);

// 设置样式
arc = majorarc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;
```

### 2. 优弧与劣弧对比

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

### 3. 设置优弧样式

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(-1, 1);  // 135 度位置

// 不同样式的优弧
arc1 = majorarc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

arc2 = majorarc(O, A, B) <<
    strokeColor: 'red',
    dash: 1,
    strokeWidth: 2
>>;

arc3 = majorarc(O, A, B) <<
    strokeColor: 'green',
    strokeWidth: 5
>>;
```

### 4. 动态优弧

```js
// 固定圆心和半径点
O = point(0, 0);
A = point(2, 0);

// 可移动的角度点
B = point(0, 2);

// 动态优弧
arc = majorarc(O, A, B) <<
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

### 5. 优弧与完整圆

```js
// 圆心和半径点
O = point(0, 0);
A = point(2, 0);

// 当角度点与半径点重合时
B = point(2, 0);  // 与 A 重合

// 完整圆（优弧的特殊情况）
fullCircle = majorarc(O, A, B);

// 或者使用 circle
circle = circle(O, A);

// 显示说明
text(-3, 3, "When start=end: Full Circle");
```

### 6. 优弧与扇形组合

```js
// 定义点
O = point(0, 0);
A = point(2, 0);
B = point(-1, -1.732);  // 240 度位置

// 优弧
majorArc = majorarc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 优扇形（填充区域）
majorSector = majorsector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.3
>>;

// 半径线
r1 = segment(O, A) << strokeColor: 'red' >>;
r2 = segment(O, B) << strokeColor: 'red' >>;
```

### 7. 获取优弧属性

```js
O = point(0, 0);
A = point(3, 0);
B = point(0, -3);  // 270 度（优弧）

arc = majorarc(O, A, B);

// 获取半径
r = arc.Radius();  // 3

// 获取弧长
len = arc.Value('length');  // 3 * 3*PI/2

// 获取角度（弧度）
angleRad = arc.Value('radians');  // 3*PI/2

// 获取角度（度）
angleDeg = arc.Value('degrees');  // 270

// 显示值
text(1, 4, "Radius: " + r);
text(1, 3.5, "Angle: " + angleDeg.toFixed(1) + "°");
text(1, 3, "Length: " + len.toFixed(2));
```

### 8. 同心优弧

```js
// 共同圆心
O = point(0, 0);

// 不同半径的点
A1 = point(1, 0);
A2 = point(2, 0);
A3 = point(3, 0);

// 共同角度点
B = point(0, -1);  // 270 度位置

// 同心优弧
arc1 = majorarc(O, A1, B) << strokeColor: 'red' >>;
arc2 = majorarc(O, A2, B) << strokeColor: 'blue' >>;
arc3 = majorarc(O, A3, B) << strokeColor: 'green' >>;
```

### 9. 圆周角定理演示（优弧情况）

```js
// 圆
O = point(0, 0);
A = point(2, 0);
c = circle(O, A);

// 优弧对应的圆心角
B = point(-1, -1.732);  // 240 度位置
majorArc = majorarc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 圆上任意点（在劣弧上）
P = point(1, 1.732);  // 60 度位置

// 圆心角（优弧对应的角）
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

### 10. 半圆作为优弧的特例

```js
// 圆心和半径点
O = point(0, 0);
A = point(2, 0);

// 角度点在对面（180 度）
B = point(-2, 0);

// 半圆（既是劣弧也是优弧的边界情况）
semicircle = majorarc(O, A, B) <<
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

### 11. 参数化优弧

```js
// 使用曲线创建参数化优弧
// 圆心 (0, 0)，半径 2，从 0 度到 270 度（优弧）

// 参数方程
fx = function(t) { return 2 * cos(t); };
fy = function(t) { return 2 * sin(t); };

// 创建曲线（优弧）
arc = curve(fx, fy, 0, 3*PI/2);

// 或使用标准 majorarc 函数
O = point(0, 0);
A = point(2, 0);
B = point(0, -2);  // 270 度位置
arc2 = majorarc(O, A, B);
```

## 注意事项

1. **方向**：优弧始终从半径点逆时针绘制到角度点
2. **角度范围**：优弧的圆心角大于或等于 180 度
3. **与劣弧区别**：劣弧小于 180 度，优弧大于或等于 180 度
4. **半圆情况**：当角度为 180 度时，是优弧和劣弧的边界情况
5. **完整圆**：当起点和终点重合时，可能绘制完整圆

## 相关元素

- [MinorArc](./MinorArc.md) - 劣弧
- [Arc](./Arc.md) - 圆弧
- [MajorSector](./MajorSector.md) - 优扇形
- [Circle](./Circle.md) - 圆
- [Semicircle](./Semicircle.md) - 半圆
