# Sector 扇形

## 描述

扇形是圆的一部分面积，由两条半径和一段圆弧围成。扇形由圆心、半径点和角度点三个点定义，始终从半径点逆时针绘制到角度点。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建扇形
sec = sector(center, radiusPoint, anglePoint);

// 带属性创建
sec = sector(O, A, B) <<
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

**注意**：扇形从 radiusPoint 开始，逆时针绘制到 anglePoint 结束。

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fillColor` | String | '#ffff00' | 填充颜色 |
| `fillOpacity` | Number | 0.8 | 填充透明度 |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `visible` | Boolean | true | 是否可见 |
| `selection` | String | 'auto' | 扇形类型：'minor', 'major', 'auto' |
| `arc` | Object | - | 圆弧子元素属性 |
| `center` | Object | - | 圆心属性 |
| `radiusPoint` | Object | - | 半径点属性 |
| `anglePoint` | Object | - | 角度点属性 |
| `label` | Object | - | 标签属性 |

### 扇形类型 (selection)

| 值 | 描述 |
|----|------|
| `'minor'` | 劣扇形（小于半圆） |
| `'major'` | 优扇形（大于半圆） |
| `'auto'` | 自动选择（默认） |

### 圆弧子元素 (arc)

扇形包含一个圆弧子元素，可以单独设置其属性：

```js
sec = sector(O, A, B) <<
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
| `Area()` | 无 | 获取扇形面积 |
| `L()` | 无 | 获取弧长 |
| `Perimeter()` | 无 | 获取周长（弧长 + 2×半径） |
| `Value()` | unit: String | 获取弧长或角度 |
| `Value('radians')` | 无 | 获取角度（弧度） |
| `Value('degrees')` | 无 | 获取角度（度） |
| `Radius()` | 无 | 获取半径 |
| `hasPointSector(x, y)` | x, y: Number | 检查点是否在扇形内 |

## 示例

### 1. 创建基本扇形

```js
// 三个点定义扇形
O = point(1.5, 5);    // 圆心
A = point(1, 0.5);    // 半径点（起点）
B = point(5, 3);      // 角度点（终点）

// 创建扇形
sec = sector(O, A, B);

// 自定义填充
sec = sector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 2. 设置扇形样式

```js
// 彩色扇形
sec1 = sector(O, A, B) <<
    fillColor: 'lightblue',
    fillOpacity: 0.6,
    strokeColor: 'darkblue'
>>;

// 无描边扇形
sec2 = sector(O, C, D) <<
    fillColor: 'pink',
    strokeWidth: 0
>>;

// 仅边框扇形
sec3 = sector(O, E, F) <<
    fillColor: 'none',
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

### 3. 劣扇形与优扇形

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(0, 2);  // 90 度位置

// 劣扇形（默认）
minorSector = sector(O, A, B) <<
    selection: 'minor',
    fillColor: 'lightblue'
>>;

// 优扇形
majorSector = sector(O, A, B) <<
    selection: 'major',
    fillColor: 'lightgreen'
>>;
```

### 4. 获取扇形属性

```js
O = point(0, 0);
A = point(3, 0);
B = point(0, 3);  // 90 度

sec = sector(O, A, B);

// 获取半径
r = sec.Radius();  // 3

// 获取面积
area = sec.Area();  // PI * 9 / 4

// 获取弧长
arcLen = sec.L();  // 3 * PI / 2

// 获取周长（弧长 + 2*半径）
perimeter = sec.Perimeter();  // 3*PI/2 + 6

// 获取角度（度）
angle = sec.Value('degrees');  // 90

// 显示值
text(1, 4, "Area: " + sec.Area().toFixed(2));
text(1, 3.5, "Perimeter: " + sec.Perimeter().toFixed(2));
```

### 5. 动态扇形

```js
// 固定圆心和起点
O = point(0, 0);
A = point(2, 0);

// 可移动的角度点
B = point(0, 2);

// 动态扇形
sec = sector(O, A, B) <<
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
```

### 6. 显示圆弧

```js
O = point(0, 0);
A = point(2, 0);
B = point(1.414, 1.414);  // 45 度

// 扇形，显示圆弧
sec = sector(O, A, B) <<
    fillColor: 'lightyellow',
    arc: <<
        visible: true,
        strokeColor: 'red',
        strokeWidth: 3
    >>
>>;
```

### 7. 多个扇形组合（饼图）

```js
// 圆心
O = point(0, 0);
A = point(2, 0);

// 数据（总和为 1）
data = [0.3, 0.25, 0.25, 0.2];
colors = ['red', 'blue', 'green', 'orange'];

// 计算累积角度
cumAngle = 0;
for (i = 0; i < 4; i = i + 1) {
    cumAngle = cumAngle + data[i] * 2 * PI;
    // 创建点
    px = 2 * cos(cumAngle);
    py = 2 * sin(cumAngle);
    point(px, py);  // 存储为变量供后续使用
}

// 实际使用时需要为每个扇形创建单独的点
P0 = point(2, 0);
P1 = point(2 * cos(0.3 * 2 * PI), 2 * sin(0.3 * 2 * PI));
P2 = point(2 * cos(0.55 * 2 * PI), 2 * sin(0.55 * 2 * PI));
P3 = point(2 * cos(0.8 * 2 * PI), 2 * sin(0.8 * 2 * PI));

// 扇形
sec1 = sector(O, P0, P1) << fillColor: colors[0] >>;
sec2 = sector(O, P1, P2) << fillColor: colors[1] >>;
sec3 = sector(O, P2, P3) << fillColor: colors[2] >>;
sec4 = sector(O, P3, P0) << fillColor: colors[3] >>;
```

### 8. 扇形与角度的关系

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(1, 1.732);  // 60 度

// 扇形
sec = sector(O, A, B) <<
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

### 9. 扇形变换

```js
// 原始扇形
sec1 = sector(point(-3.5, -3), point(-3.5, -2), point(-3.5, -4)) <<
    fillColor: 'yellow',
    strokeColor: 'black',
    center: << visible: true >>,
    radiusPoint: << visible: true >>,
    anglePoint: << visible: true >>
>>;

// 创建缩放变换
scale = transform(2, 1.5) << type: 'scale' >>;

// 变换后的扇形
sec2 = curve(sec1, scale) <<
    fillColor: 'yellow',
    strokeColor: 'black'
>>;
```

### 10. 弓形（扇形减去三角形）

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(0, 2);

// 扇形
sec = sector(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 三角形
tri = polygon(O, A, B) <<
    fillColor: 'white'
>>;

// 弓形 = 扇形 - 三角形（视觉上）
// 注意：JessieCode 中没有直接的布尔运算
// 可以通过图层顺序实现视觉效果
```

### 11. 圆环扇形

```js
// 共同圆心
O = point(0, 0);

// 外圆点
A1 = point(3, 0);
B1 = point(0, 3);

// 内圆点
A2 = point(2, 0);
B2 = point(0, 2);

// 外扇形
outerSec = sector(O, A1, B1) <<
    fillColor: 'blue',
    fillOpacity: 0.5
>>;

// 内扇形（覆盖外层中心部分）
innerSec = sector(O, A2, B2) <<
    fillColor: 'white',
    fillOpacity: 1
>>;

// 结果：圆环扇形
```

## 注意事项

1. **方向**：扇形始终从半径点逆时针绘制到角度点
2. **子元素圆弧**：扇形包含一个圆弧子元素 `sec.arc`，可以单独访问和设置
3. **面积计算**：面积 = (角度/2π) × πr² = 角度 × r² / 2
4. **周长计算**：周长 = 弧长 + 2 × 半径
5. **与圆弧区别**：扇形有填充区域，圆弧只有边框

## 相关元素

- [Arc](./Arc.md) - 圆弧
- [Angle](./Angle.md) - 角度
- [Circle](./Circle.md) - 圆
- [Polygon](./Polygon.md) - 多边形
