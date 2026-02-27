# CircumcircleSector 外接圆扇形

<!-- USAGE_FREQUENCY: advanced -->

## 描述

外接圆扇形是一种扇形，其圆弧是通过三个点的外接圆弧。外接圆扇形与普通扇形的主要区别在于父元素的解释方式：首先由三个给定点确定外心，然后扇形从第一个点经过第二个点绘制到第三个点。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建外接圆扇形
sector = circumcirclesector(A, B, C);

// 带属性创建
sector = circumcirclesector(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    strokeColor: 'blue'
>>;

// 显示圆心
sector = circumcirclesector(A, B, C) <<
    center: <<
        visible: true,
        strokeColor: 'red',
        size: 5
    >>
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| A | Point | 第一个点（扇形起点） |
| B | Point | 第二个点（扇形经过的点） |
| C | Point | 第三个点（扇形终点） |

**注意**：扇形从点 A 开始，逆时针经过点 B，到点 C 结束。

## 属性

外接圆扇形继承自 Sector，因此具有所有扇形的属性：

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

### 扇形类型 (selection)

| 值 | 描述 |
|----|------|
| `'minor'` | 劣扇形（小于半圆） |
| `'major'` | 优扇形（大于半圆） |
| `'auto'` | 自动选择（默认） |

### 圆弧子元素 (arc)

扇形包含一个圆弧子元素，可以单独设置其属性：

```js
sector = circumcirclesector(A, B, C) <<
    arc: <<
        visible: true,
        strokeColor: 'red',
        strokeWidth: 2
    >>
>>;
```

## 方法

外接圆扇形继承自 Sector，因此具有所有扇形的方法：

| 方法 | 参数 | 描述 |
|------|------|------|
| `Area()` | 无 | 获取扇形面积 |
| `L()` | 无 | 获取弧长 |
| `Perimeter()` | 无 | 获取周长（弧长 + 2×半径） |
| `Value()` | unit: String | 获取弧长或角度 |
| `Value('radians')` | 无 | 获取角度（弧度） |
| `Value('degrees')` | 无 | 获取角度（度） |
| `Radius()` | 无 | 获取半径 |

## 示例

### 1. 创建基本外接圆扇形

```js
// 三个点定义外接圆扇形
A = point(1.5, 5);
B = point(1, 0.5);
C = point(5, 3);

// 创建外接圆扇形
sector = circumcirclesector(A, B, C);

// 带样式的外接圆扇形
sector = circumcirclesector(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    strokeColor: 'blue'
>>;
```

### 2. 显示圆心和半径

```js
// 三个点
A = point(1.5, 5);
B = point(1, 0.5);
C = point(5, 3);

// 外接圆扇形，显示圆心
sector = circumcirclesector(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    center: <<
        visible: true,
        strokeColor: 'red',
        fillColor: 'black',
        size: 5,
        withLabel: true,
        name: 'O'
    >>
>>;

// 显示半径
text(1, 6, function() {
    return "Radius: " + sector.Radius().toFixed(3);
});
```

### 3. 动态外接圆扇形

```js
// 可移动的点
A = point(2, 2);
B = point(1, 0.5);
C = point(3.5, 1);  // 可以拖动

// 外接圆扇形随点移动而更新
sector = circumcirclesector(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 显示面积
text(1, 3, function() {
    return "Area: " + sector.Area().toFixed(3);
});

// 显示周长
text(1, 2.5, function() {
    return "Perimeter: " + sector.Perimeter().toFixed(3);
});
```

### 4. 外接圆扇形与外接圆弧

```js
// 三角形顶点
A = point(1, 1);
B = point(5, 1);
C = point(3, 4);

// 外接圆扇形（填充区域）
sector = circumcirclesector(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 外接圆弧（仅边框）
arc = circumcirclearc(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 完整的外接圆
circumcircle = circumcircle(A, B, C) <<
    strokeColor: 'gray',
    dash: 1
>>;
```

### 5. 劣扇形与优扇形

```js
// 基础点
A = point(2, 0);
B = point(1, 1);
C = point(0, 2);

// 劣扇形（默认）
minorSector = circumcirclesector(A, B, C) <<
    selection: 'minor',
    fillColor: 'lightblue',
    fillOpacity: 0.5
>>;

// 优扇形
majorSector = circumcirclesector(A, B, C) <<
    selection: 'major',
    fillColor: 'lightgreen',
    fillOpacity: 0.5
>>;
```

### 6. 获取外接圆扇形属性

```js
// 三个点
A = point(1, 0);
B = point(0, 1);
C = point(-1, 0);

// 外接圆扇形
sector = circumcirclesector(A, B, C);

// 获取半径
r = sector.Radius();

// 获取面积
area = sector.Area();

// 获取弧长
arcLen = sector.L();

// 获取周长（弧长 + 2*半径）
perimeter = sector.Perimeter();

// 获取角度（度）
angle = sector.Value('degrees');

// 显示值
text(-2, 2, "Radius: " + r.toFixed(3));
text(-2, 1.5, "Area: " + area.toFixed(3));
text(-2, 1, "Perimeter: " + perimeter.toFixed(3));
text(-2, 0.5, "Angle: " + angle.toFixed(1) + "°");
```

### 7. 外接圆扇形样式设置

```js
// 三个点
A = point(1.5, 5);
B = point(1, 0.5);
C = point(5, 3);

// 自定义样式的外接圆扇形
sector = circumcirclesector(A, B, C) <<
    fillColor: 'lightyellow',
    fillOpacity: 0.6,
    strokeColor: 'darkblue',
    strokeWidth: 2,
    arc: <<
        visible: true,
        strokeColor: 'red',
        strokeWidth: 3
    >>,
    center: <<
        visible: true,
        strokeColor: 'green',
        size: 6
    >>
>>;
```

### 8. 多个外接圆扇形组合（饼图）

```js
// 圆心（外心）
O = point(0, 0);

// 圆上的点
A = point(2, 0);
B = point(0, 2);
C = point(-2, 0);
D = point(0, -2);

// 四个外接圆扇形组成一个完整的圆
// 注意：这里使用 circumcirclesector 需要三点确定
sector1 = circumcirclesector(O, A, B) << fillColor: 'red', fillOpacity: 0.5 >>;
sector2 = circumcirclesector(O, B, C) << fillColor: 'blue', fillOpacity: 0.5 >>;
sector3 = circumcirclesector(O, C, D) << fillColor: 'green', fillOpacity: 0.5 >>;
sector4 = circumcirclesector(O, D, A) << fillColor: 'orange', fillOpacity: 0.5 >>;
```

### 9. 外接圆扇形与角度

```js
// 三个点
A = point(2, 0);
B = point(1, 1.732);  // 60 度位置
C = point(0, 2);

// 外接圆扇形
sector = circumcirclesector(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 显示角度
text(1, 3, function() {
    return "Angle: " + sector.Value('degrees').toFixed(1) + "°";
});

// 显示面积与角度的关系
text(1, 2.5, function() {
    r = sector.Radius();
    angle = sector.Value('radians');
    return "Area = 0.5 * r² * θ = " + (0.5 * r * r * angle).toFixed(3);
});
```

### 10. 外接圆扇形变换

```js
// 原始外接圆扇形
A = point(1, 1);
B = point(0, 0);
C = point(2, 0);

sector1 = circumcirclesector(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    strokeColor: 'blue'
>>;

// 创建旋转变换
rotate = transform(PI/4, 0, 0) << type: 'rotate' >>;

// 变换后的扇形（需要用 curve 变换）
sector2 = curve(sector1, rotate) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    strokeColor: 'red'
>>;
```

### 11. 外接圆扇形与普通扇形对比

```js
// 先确定圆心
O = point(0, 0);
A = point(2, 0);
B = point(1, 1.732);  // 60 度位置

// 普通扇形（需要显式指定圆心）
sector1 = sector(O, A, B) <<
    fillColor: 'lightblue',
    fillOpacity: 0.5
>>;

// 外接圆扇形（自动确定圆心）
sector2 = circumcirclesector(O, A, B) <<
    fillColor: 'lightyellow',
    fillOpacity: 0.5
>>;

// 在这种情况下，两者是相同的，因为 O 已经是圆心
```

## 注意事项

1. **方向**：外接圆扇形始终从第一个点逆时针经过第二个点绘制到第三个点
2. **三点确定**：三个点唯一确定一个外接圆扇形
3. **与 Sector 的区别**：`circumcirclesector` 自动通过三点确定圆心和半径，而 `sector` 需要显式指定圆心
4. **选择类型**：使用 `selection` 属性可以强制绘制劣扇形或优扇形
5. **子元素圆弧**：扇形包含一个圆弧子元素 `sector.arc`，可以单独访问和设置
6. **面积计算**：面积 = (角度/2π) × πr² = 角度 × r² / 2（角度以弧度为单位）
7. **周长计算**：周长 = 弧长 + 2 × 半径

## 相关元素

- [Circumcenter](./Circumcenter.md) - 外心
- [Circumcircle](./Circumcircle.md) - 外接圆
- [CircumcircleArc](./CircumcircleArc.md) - 外接圆弧
- [Sector](./Sector.md) - 扇形
- [Arc](./Arc.md) - 圆弧
- [Circle](./Circle.md) - 圆
