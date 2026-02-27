# MajorSector 优扇形

<!-- USAGE_FREQUENCY: common -->

## 描述

优扇形是圆心角大于或等于 180 度（π 弧度）的扇形。优扇形由圆心、半径点和角度点三个点定义，从半径点开始，逆时针绘制到角度点结束，包含填充区域。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建优扇形
sec = majorsector(center, radiusPoint, anglePoint);

// 带属性创建
sec = majorsector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    strokeColor: 'blue'
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| center | Point | 圆心（扇形顶点） |
| radiusPoint | Point | 半径点（定义半径和起点） |
| anglePoint | Point | 角度点（定义终点） |

**注意**：
- 优扇形从 radiusPoint 开始，逆时针绘制到 anglePoint 结束
- 优扇形的圆心角大于或等于 180 度

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fillColor` | String | '#ffff00' | 填充颜色 |
| `fillOpacity` | Number | 0.8 | 填充透明度 |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `visible` | Boolean | true | 是否可见 |
| `arc` | Object | - | 圆弧子元素属性 |
| `center` | Object | - | 圆心属性 |
| `radiusPoint` | Object | - | 半径点属性 |
| `anglePoint` | Object | - | 角度点属性 |

### 圆弧子元素 (arc)

优扇形包含一个圆弧子元素，可以单独设置其属性：

```js
sec = majorsector(O, A, B) <<
    arc: <<
        visible: true,
        strokeColor: 'red',
        strokeWidth: 2
    >>
>>;
```

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `Area()` | 无 | 获取优扇形面积 |
| `L()` | 无 | 获取弧长 |
| `Perimeter()` | 无 | 获取周长（弧长 + 2×半径） |
| `Value()` | unit: String | 获取弧长或角度 |
| `Value('radians')` | 无 | 获取角度（弧度） |
| `Value('degrees')` | 无 | 获取角度（度） |
| `Radius()` | 无 | 获取半径 |

## 示例

### 1. 创建基本优扇形

```js
// 三个点定义优扇形
O = point(1.5, 5);    // 圆心
A = point(1, 0.5);    // 半径点（起点）
B = point(5, 3);      // 角度点（终点）

// 创建优扇形
sec = majorsector(O, A, B);

// 自定义填充
sec = majorsector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 2. 优扇形与劣扇形对比

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(0, 2);  // 90 度位置

// 劣扇形（小于 180 度）
minorSector = sector(O, A, B) <<
    selection: 'minor',
    fillColor: 'lightblue',
    fillOpacity: 0.5
>>;

// 优扇形（大于 180 度）- 相同的点，不同的扇形类型
majorSector = majorsector(O, A, B) <<
    fillColor: 'lightgreen',
    fillOpacity: 0.5
>>;

// 显示区别
text(-3, 3, "Blue: Minor Sector, Green: Major Sector");
```

### 3. 设置优扇形样式

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(-1, -1);  // 225 度位置

// 不同样式的优扇形
sec1 = majorsector(O, A, B) <<
    fillColor: 'lightyellow',
    fillOpacity: 0.6
>>;

sec2 = majorsector(O, A, B) <<
    fillColor: 'pink',
    fillOpacity: 0.4,
    strokeColor: 'red',
    strokeWidth: 2
>>;

sec3 = majorsector(O, A, B) <<
    fillColor: 'lightblue',
    fillOpacity: 0.3,
    arc: <<
        visible: true,
        strokeColor: 'blue',
        strokeWidth: 3
    >>
>>;
```

### 4. 获取优扇形属性

```js
O = point(0, 0);
A = point(3, 0);
B = point(0, -3);  // 270 度

sec = majorsector(O, A, B);

// 获取半径
r = sec.Radius();  // 3

// 获取面积
area = sec.Area();  // PI * 9 * 3/4

// 获取弧长
arcLen = sec.L();  // 3 * 3*PI/2

// 获取周长（弧长 + 2*半径）
perimeter = sec.Perimeter();  // 3*3*PI/2 + 6

// 获取角度（度）
angle = sec.Value('degrees');  // 270

// 显示值
text(1, 4, "Area: " + area.toFixed(2));
text(1, 3.5, "Perimeter: " + perimeter.toFixed(2));
text(1, 3, "Angle: " + angle.toFixed(1) + "°");
```

### 5. 动态优扇形

```js
// 固定圆心和起点
O = point(0, 0);
A = point(2, 0);

// 可移动的角度点
B = point(0, -2);

// 动态优扇形
sec = majorsector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 实时更新面积和周长
areaText = text(1, 3, function() {
    return "Area: " + sec.Area().toFixed(2);
});

perimeterText = text(1, 2.5, function() {
    return "Perimeter: " + sec.Perimeter().toFixed(2);
});

// 显示角度
angleText = text(1, 2, function() {
    return "Angle: " + sec.Value('degrees').toFixed(1) + "°";
});
```

### 6. 显示圆弧边框

```js
O = point(0, 0);
A = point(2, 0);
B = point(-1, -1.732);  // 240 度

// 优扇形，显示圆弧
sec = majorsector(O, A, B) <<
    fillColor: 'lightyellow',
    fillOpacity: 0.5,
    arc: <<
        visible: true,
        strokeColor: 'red',
        strokeWidth: 3
    >>
>>;

// 半径线
r1 = segment(O, A) << strokeColor: 'blue', strokeWidth: 2 >>;
r2 = segment(O, B) << strokeColor: 'blue', strokeWidth: 2 >>;
```

### 7. 多个优扇形组合（饼图）

```js
// 圆心
O = point(0, 0);

// 数据（总和为 1），使用优扇形展示大部分
data = [0.6, 0.4];
colors = ['red', 'blue'];

// 创建点
P0 = point(2, 0);
P1 = point(2 * cos(0.6 * 2 * PI), 2 * sin(0.6 * 2 * PI));

// 优扇形（60%）
sec1 = majorsector(O, P0, P1) <<
    fillColor: colors[0],
    fillOpacity: 0.5
>>;

// 劣扇形（40%）
sec2 = sector(O, P1, P0) <<
    fillColor: colors[1],
    fillOpacity: 0.5
>>;
```

### 8. 优扇形与角度的关系

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(-1, -1.732);  // 240 度

// 优扇形
sec = majorsector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 角度（使用 Angle 元素）
ang = angle(A, O, B) <<
    radius: 0.8,
    type: 'sector',
    fillColor: 'lightblue'
>>;

// 显示关系
text(1, 3, "Sector Area: " + sec.Area().toFixed(2));
text(1, 2.5, "Angle: " + ang.Value('degrees') + "°");
```

### 9. 优扇形变换

```js
// 原始优扇形
sec1 = majorsector(point(-3, -3), point(-2, -3), point(-4, -4)) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    strokeColor: 'black'
>>;

// 创建缩放变换
scale = transform(1.5, 1.5) << type: 'scale' >>;

// 变换后的优扇形
sec2 = curve(sec1, scale) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    strokeColor: 'black'
>>;
```

### 10. 半圆扇形作为特例

```js
// 圆心和半径点
O = point(0, 0);
A = point(2, 0);

// 角度点在对面（180 度）
B = point(-2, 0);

// 半圆扇形（既是劣扇形也是优扇形的边界情况）
semiSector1 = majorsector(O, A, B) <<
    fillColor: 'lightblue',
    fillOpacity: 0.5
>>;

// 或使用 sector 的 selection 属性
semiSector2 = sector(O, A, B) <<
    selection: 'major',
    fillColor: 'lightgreen',
    fillOpacity: 0.5
>>;

text(-3, 3, "180°: Boundary case");
```

### 11. 同心优扇形（圆环扇形）

```js
// 共同圆心
O = point(0, 0);

// 外圆点
A1 = point(3, 0);
B1 = point(0, -3);  // 270 度

// 内圆点
A2 = point(2, 0);
B2 = point(0, -2);  // 270 度

// 外优扇形
outerSec = majorsector(O, A1, B1) <<
    fillColor: 'blue',
    fillOpacity: 0.5
>>;

// 内优扇形（覆盖外层中心部分）
innerSec = majorsector(O, A2, B2) <<
    fillColor: 'white',
    fillOpacity: 1
>>;

// 结果：圆环扇形
```

## 注意事项

1. **方向**：优扇形始终从半径点逆时针绘制到角度点
2. **角度范围**：优扇形的圆心角大于或等于 180 度
3. **子元素圆弧**：优扇形包含一个圆弧子元素 `sec.arc`，可以单独访问和设置
4. **面积计算**：面积 = (角度/2π) × πr² = 角度 × r² / 2
5. **周长计算**：周长 = 弧长 + 2 × 半径
6. **与劣扇形区别**：劣扇形小于 180 度，优扇形大于或等于 180 度
7. **半圆情况**：当角度为 180 度时，是优扇形和劣扇形的边界情况

## 相关元素

- [Sector](./Sector.md) - 扇形
- [MajorArc](./MajorArc.md) - 优弧
- [MinorSector](./MinorSector.md) - 劣扇形
- [Angle](./Angle.md) - 角度
- [Circle](./Circle.md) - 圆
