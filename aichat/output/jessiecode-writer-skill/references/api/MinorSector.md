# MinorSector 劣扇形

## 描述

劣扇形是角度不超过 180 度（π 弧度）的扇形。它由圆心、半径点和角度点三个点定义。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建劣扇形
minorSec = minorsector(center, radiusPoint, anglePoint);

// 带属性创建
minorSec = minorsector(O, A, B) <<
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

**注意**：劣扇形从 radiusPoint 开始，逆时针绘制到 anglePoint 结束，角度始终小于或等于 180 度。

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

劣扇形包含一个圆弧子元素，可以单独设置其属性：

```js
minorSec = minorsector(O, A, B) <<
    arc: <<
        visible: true,
        strokeColor: 'red',
        strokeWidth: 2,
        lastArrow: << size: 4 >>,
        firstArrow: << size: 4 >>
    >>
>>;
```

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `Area()` | 无 | 获取劣扇形面积 |
| `L()` | 无 | 获取弧长 |
| `Perimeter()` | 无 | 获取周长（弧长 + 2×半径） |
| `Value()` | unit: String | 获取弧长或角度 |
| `Value('radians')` | 无 | 获取角度（弧度） |
| `Value('degrees')` | 无 | 获取角度（度） |
| `Radius()` | 无 | 获取半径 |
| `hasPointSector(x, y)` | x, y: Number | 检查点是否在劣扇形内 |

## 示例

### 1. 创建基本劣扇形

```js
// 三个点定义劣扇形
O = point(2.0, 2.0);    // 圆心
A = point(1.0, 0.5);    // 半径点（起点）
B = point(3.5, 1.0);    // 角度点（终点）

// 创建劣扇形
minorSec = minorsector(O, A, B);
```

### 2. 设置劣扇形样式

```js
A = point(3, -2);
B = point(-2, -2);
C = point(0, 4);

// 劣扇形，带自定义圆弧
angle = minorsector(B, A, C) <<
    strokeWidth: 0,
    arc: <<
        visible: true,
        strokeWidth: 3,
        lastArrow: << size: 4 >>,
        firstArrow: << size: 4 >>
    >>
>>;

// 隐藏圆弧箭头
angle.arc.setAttribute(<< lastArrow: false >>);
```

### 3. 劣扇形与优扇形对比

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(0, 2);  // 90 度位置

// 劣扇形（角度 <= 180 度）
minorSec = minorsector(O, A, B) <<
    fillColor: 'lightblue',
    fillOpacity: 0.5
>>;

// 注意：如果使用 sector 创建同样的点，当角度 > 180 度时会创建优扇形
```

### 4. 获取劣扇形属性

```js
O = point(0, 0);
A = point(3, 0);
B = point(0, 3);  // 90 度

minorSec = minorsector(O, A, B);

// 获取半径
r = minorSec.Radius();  // 3

// 获取面积
area = minorSec.Area();  // PI * 9 / 4

// 获取弧长
arcLen = minorSec.L();  // 3 * PI / 2

// 获取周长（弧长 + 2*半径）
perimeter = minorSec.Perimeter();  // 3*PI/2 + 6

// 获取角度（度）
angle = minorSec.Value('degrees');  // 90

// 显示值
text(1, 4, "Area: " + minorSec.Area().toFixed(2));
text(1, 3.5, "Perimeter: " + minorSec.Perimeter().toFixed(2));
```

### 5. 动态劣扇形

```js
// 固定圆心和起点
O = point(0, 0);
A = point(2, 0);

// 可移动的角度点（限制在劣扇形范围内）
B = point(0, 2);

// 动态劣扇形
minorSec = minorsector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 实时更新面积和周长
areaText = text(1, 3, function() {
    return "Area: " + minorSec.Area().toFixed(2);
});

perimeterText = text(1, 2.5, function() {
    return "Perimeter: " + minorSec.Perimeter().toFixed(2);
});
```

### 6. 劣扇形与角度

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(1, 1.732);  // 60 度

// 劣扇形
minorSec = minorsector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 显示角度值
angleText = text(1, 3, function() {
    return "Angle: " + minorSec.Value('degrees').toFixed(1) + "°";
});
```

### 7. 劣扇形变换

```js
// 原始劣扇形
minorSec1 = minorsector(point(-3.5, -3), point(-3.5, -2), point(-3.5, -4)) <<
    fillColor: 'yellow',
    strokeColor: 'black',
    center: << visible: true >>,
    radiusPoint: << visible: true >>,
    anglePoint: << visible: true >>
>>;

// 创建缩放变换
scale = transform(2, 1.5) << type: 'scale' >>;

// 变换后的劣扇形
minorSec2 = curve(minorSec1, scale) <<
    fillColor: 'yellow',
    strokeColor: 'black'
>>;
```

### 8. 劣扇形与圆弧组合

```js
// 定义点
O = point(0, 0);
A = point(2, 0);
B = point(1, 1.732);  // 60 度位置

// 劣扇形（填充区域）
minorSec = minorsector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.3
>>;

// 单独的圆弧（可用于强调边界）
arc = arc(O, A, B) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 半径线
r1 = segment(O, A) << strokeColor: 'red' >>;
r2 = segment(O, B) << strokeColor: 'red' >>;
```

### 9. 三角形内切劣扇形

```js
// 三角形顶点
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);

// 在顶点 B 处创建劣扇形（表示内角）
angleSector = minorsector(B, A, C) <<
    fillColor: 'lightblue',
    fillOpacity: 0.6,
    radius: 0.5
>>;

// 显示角度值
text(0, -2, "Angle at B: " + angleSector.Value('degrees').toFixed(1) + "°");
```

### 10. 多个劣扇形比较

```js
// 共同圆心
O = point(0, 0);
A = point(2, 0);

// 不同角度的点
B1 = point(0, 2);      // 90 度
B2 = point(-1, 1);     // 135 度
B3 = point(-2, 0);     // 180 度（半圆）

// 创建多个劣扇形
sec1 = minorsector(O, A, B1) << fillColor: 'red', fillOpacity: 0.3 >>;
sec2 = minorsector(O, A, B2) << fillColor: 'green', fillOpacity: 0.3 >>;
sec3 = minorsector(O, A, B3) << fillColor: 'blue', fillOpacity: 0.3 >>;

// 显示角度
text(1, 3, "90°: " + sec1.Area().toFixed(2));
text(1, 2.5, "135°: " + sec2.Area().toFixed(2));
text(1, 2, "180°: " + sec3.Area().toFixed(2));
```

## 注意事项

1. **角度限制**：劣扇形的角度始终小于或等于 180 度（π 弧度）
2. **方向**：劣扇形始终从半径点逆时针绘制到角度点
3. **子元素圆弧**：劣扇形包含一个圆弧子元素 `minorSec.arc`，可以单独访问和设置
4. **面积计算**：面积 = (角度/2π) × πr² = 角度 × r² / 2
5. **周长计算**：周长 = 弧长 + 2 × 半径
6. **与 Sector 区别**：`minorsector` 强制创建角度 ≤ 180°的扇形，而 `sector` 根据角度自动选择劣扇形或优扇形

## 相关元素

- [Sector](./Sector.md) - 扇形
- [MajorSector](./MajorSector.md) - 优扇形
- [Arc](./Arc.md) - 圆弧
- [Angle](./Angle.md) - 角度
- [Circle](./Circle.md) - 圆
