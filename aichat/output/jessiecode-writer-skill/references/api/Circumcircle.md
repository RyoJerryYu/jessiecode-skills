# Circumcircle 外接圆

## 描述

外接圆是通过三个点的唯一圆。给定三个不共线的点，存在且仅存在一个圆通过这三个点。外接圆的圆心是三角形三条边垂直平分线的交点（外心）。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建外接圆
c = circumcircle(A, B, C);

// 带属性创建
c = circumcircle(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    dash: 1
>>;

// 显示圆心
c = circumcircle(A, B, C) <<
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
| A | Point | 第一个点 |
| B | Point | 第二个点 |
| C | Point | 第三个点 |

**注意**：三个点不能共线，否则无法确定唯一的外接圆。

## 属性

外接圆继承自 Circle，因此具有所有圆的属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `fillOpacity` | Number | 0.0 | 填充透明度 |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线 |
| `opacity` | Number | 1.0 | 透明度 |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 圆名称 |
| `center` | Object | - | 圆心属性设置 |

### 圆心属性

```js
// 显示圆心
c = circumcircle(A, B, C) <<
    center: <<
        visible: true,
        strokeColor: 'red',
        fillColor: 'black',
        size: 5,
        face: '[]'
    >>
>>;
```

## 方法

外接圆继承自 Circle，因此具有所有圆的方法：

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

### 1. 创建基本外接圆

```js
// 创建三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 创建外接圆
c = circumcircle(A, B, C);

// 带样式的外接圆
c = circumcircle(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    dash: 1
>>;
```

### 2. 显示圆心和半径

```js
// 三角形顶点
A = point(1, 1);
B = point(5, 1);
C = point(3, 4);

// 外接圆，显示圆心
c = circumcircle(A, B, C) <<
    strokeColor: 'blue',
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
text(1, 5, function() {
    return "Radius: " + c.Radius().toFixed(3);
});
```

### 3. 动态外接圆

```js
// 可移动的三角形顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);  // 可以拖动

// 外接圆随顶点移动而更新
c = circumcircle(A, B, C) <<
    strokeColor: 'blue',
    dash: 1
>>;

// 显示圆心坐标
text(-3, 4, function() {
    return "Center: (" + c.X().toFixed(2) + ", " + c.Y().toFixed(2) + ")";
});

// 显示半径
text(-3, 3.5, function() {
    return "Radius: " + c.Radius().toFixed(3);
});
```

### 4. 不同类型三角形的外接圆

```js
// 锐角三角形 - 外心在三角形内部
A1 = point(-6, 2);
B1 = point(-2, 2);
C1 = point(-4, 5);
c1 = circumcircle(A1, B1, C1) << strokeColor: 'blue' >>;

// 直角三角形 - 外心在斜边中点
A2 = point(-1, 0);
B2 = point(3, 0);
C2 = point(-1, 3);
c2 = circumcircle(A2, B2, C2) << strokeColor: 'green' >>;

// 钝角三角形 - 外心在三角形外部
A3 = point(2, 0);
B3 = point(6, 0);
C3 = point(3, 1);
c3 = circumcircle(A3, B3, C3) << strokeColor: 'red' >>;
```

### 5. 外接圆与垂直平分线

```js
// 三角形顶点
A = point(1, 1);
B = point(5, 1);
C = point(3, 4);

// 外接圆
c = circumcircle(A, B, C) <<
    strokeColor: 'blue',
    dash: 1
>>;

// 三边中点
Mab = midpoint(A, B);
Mbc = midpoint(B, C);
Mca = midpoint(C, A);

// 垂直平分线
perpAB = perpendicular(Mab, line(A, B));
perpBC = perpendicular(Mbc, line(B, C));
perpCA = perpendicular(Mca, line(C, A));

// 设置垂直平分线样式
perpAB << dash: 1, strokeColor: 'gray' >>;
perpBC << dash: 1, strokeColor: 'gray' >>;
perpCA << dash: 1, strokeColor: 'gray' >>;

// 垂直平分线交于外心（圆心）
```

### 6. 外接圆半径公式

```js
// 三角形顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 外接圆
c = circumcircle(A, B, C);

// 计算三角形边长
a = dist(B, C);  // 边 a (对边 A)
b = dist(A, C);  // 边 b (对边 B)
c_side = dist(A, B);  // 边 c (对边 C)

// 计算三角形面积（海伦公式）
s = (a + b + c_side) / 2;
area = sqrt(s * (s - a) * (s - b) * (s - c_side));

// 外接圆半径公式：R = abc / (4 * 面积)
R_formula = (a * b * c_side) / (4 * area);

// 显示结果
text(1, 4, "Radius from formula: " + R_formula.toFixed(4));
text(1, 3.5, "Radius from circle: " + c.Radius().toFixed(4));
```

### 7. 外接圆与三角函数

```js
// 三角形顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 外接圆
c = circumcircle(A, B, C);
R = c.Radius();

// 计算角 A 的大小
angleA = angle(B, A, C);

// 正弦定理：a / sin(A) = 2R
a = dist(B, C);
R_from_sine = a / (2 * sin(angleA.Value('radians') / 2));

text(1, 5, "R = a / (2*sin(A)) = " + R_from_sine.toFixed(4));
text(1, 4.5, "Actual R = " + R.toFixed(4));
```

### 8. 多个外接圆比较

```js
// 固定两点
A = point(-3, 0);
B = point(3, 0);

// 不同的第三点
C1 = point(0, 2);
C2 = point(0, 3);
C3 = point(0, 4);
C4 = point(0, 5);

// 不同的外接圆
c1 = circumcircle(A, B, C1) << strokeColor: 'red', fillOpacity: 0.1 >>;
c2 = circumcircle(A, B, C2) << strokeColor: 'blue', fillOpacity: 0.1 >>;
c3 = circumcircle(A, B, C3) << strokeColor: 'green', fillOpacity: 0.1 >>;
c4 = circumcircle(A, B, C4) << strokeColor: 'orange', fillOpacity: 0.1 >>;
```

### 9. 外接圆与内切圆

```js
// 三角形顶点
A = point(0, 0);
B = point(5, 0);
C = point(2, 4);

// 外接圆
circum = circumcircle(A, B, C) <<
    strokeColor: 'blue',
    dash: 1
>>;

// 内切圆（如果 JessieCode 支持）
// incenter = anglebisector(A, B, C) 和 anglebisector(B, C, A) 的交点
// incircle = circle(incenter, ...)

// 显示外接圆半径
text(1, 5, "Circumradius: " + circum.Radius().toFixed(3));
```

### 10. 外接圆变换

```js
// 原始三角形
A = point(1, 1);
B = point(3, 1);
C = point(2, 3);

// 外接圆
c1 = circumcircle(A, B, C) <<
    strokeColor: 'blue',
    fillOpacity: 0.2
>>;

// 创建缩放变换
scale = transform(2, 1.5) << type: 'scale' >>;

// 变换后的三角形
A2 = curve(A, scale);
B2 = curve(B, scale);
C2 = curve(C, scale);

// 变换后的外接圆
c2 = circumcircle(A2, B2, C2) <<
    strokeColor: 'red',
    fillOpacity: 0.2
>>;
```

## 注意事项

1. **三点不共线**：三个点不能在同一直线上，否则无法确定唯一的外接圆
2. **唯一性**：给定三个不共线的点，存在且仅存在一个外接圆
3. **圆心位置**：
   - 锐角三角形：圆心在三角形内部
   - 直角三角形：圆心在斜边中点
   - 钝角三角形：圆心在三角形外部
4. **与 Circumcenter 的关系**：外接圆的圆心就是外心（circumcenter）
5. **填充效果**：设置 `fillColor` 和 `fillOpacity` 可以创建填充效果，用于可视化圆内区域

## 相关元素

- [Circumcenter](./Circumcenter.md) - 外心
- [CircumcircleArc](./CircumcircleArc.md) - 外接圆弧
- [CircumcircleSector](./CircumcircleSector.md) - 外接圆扇形
- [Circle](./Circle.md) - 圆
- [Incircle](./Incircle.md) - 内切圆
- [Arc](./Arc.md) - 圆弧
- [Sector](./Sector.md) - 扇形
