# Reflection 反射

<!-- USAGE_FREQUENCY: advanced -->

## 描述

将一个点、直线、圆、曲线、多边形关于给定直线进行反射。

## JessieCode 语法

```js
// 基本语法 - 创建点关于直线的反射
p1 = point(0, 4);
p2 = point(6, 1);
l1 = line(p1, p2);
p3 = point(3, 3);

// 创建点 p3 关于直线 l1 的反射点
rp1 = reflection(p3, l1);

// 创建直线关于直线的反射
l2 = line(1, -5, 1);
l3 = reflection(l2, l1);

// 创建曲线关于直线的反射
cu1 = curve([-3, -3, -2.5, -3, -3, -2.5], [-3, -2, -2, -2, -2.5, -2.5]) << strokeWidth: 3 >>;
cu2 = reflection(cu1, l1) << strokeColor: 'red', strokeWidth: 3 >>;

// 创建多边形关于直线的反射
pol1 = polygon([[-6,-3], [-4,-5], [-5,-1.5]]);
pol2 = reflection(pol1, l1);

// 创建圆关于直线的反射
c1 = circle([-2,-2], [-2, -1]);
c2 = reflection(c1, l1);

// 带属性创建
rp1 = reflection(p3, l1) <<
    strokeColor: 'red',
    fillColor: 'pink',
    withLabel: true,
    name: "P'"
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| p1 | Point/Line/Circle/Curve/Polygon/Arc/Sector/Angle | 要被反射的元素（点、直线、圆、曲线、多边形、圆弧、扇形、角） |
| p2 | Line | 反射轴（直线） |

### 父元素组合说明

| 父元素组合 | 描述 |
|-----------|------|
| `p1` (Point/Line/Circle/Curve/Polygon), `p2` (Line) | 构造的元素是 p1 关于直线 p2 的反射 |

### 异常

如果无法使用给定的父元素构造反射元素，将抛出异常。

## 属性

Reflection 继承 [JXG.GeometryElement](./JXG.GeometryElement.md) 的所有属性，常用属性如下：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 元素名称 |
| `id` | String | 自动生成 | 元素的唯一 ID |

### 特定属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `center` | Object | - | 圆的属性，即圆心坐标。当反射元素是圆且变换类型为 'Euclidean' 时使用 |
| `type` | String | 'Euclidean' | 变换类型。可选值：'Euclidean'（欧几里得）、'projective'（射影）。当值为 'Euclidean' 时，圆的反射仍是圆；否则为圆锥曲线 |

### 特定元素的属性

根据被反射的元素类型，可以设置相应的特定属性：

- **点**：`size`, `face`, `fixed` 等
- **直线/曲线**：`dash`, `straightFirst`, `straightLast` 等
- **圆**：`fillOpacity`, `strokeOpacity` 等
- **多边形**：`fillOpacity`, `borders` 等

## 示例

### 1. 点关于直线的反射

```js
// 创建反射轴
p1 = point(0, 4);
p2 = point(6, 1);
l1 = line(p1, p2);

// 原始点
p3 = point(3, 3);

// 创建反射点
rp1 = reflection(p3, l1);
```

### 2. 多元素反射

```js
// 反射轴
li = line(1, 1, 1) << strokeColor: '#aaaaaa' >>;

// 点及其反射
p1 = point(-3, -1) << name: "A" >>;
q1 = reflection(p1, li) << name: "A'" >>;

// 直线及其反射
l1 = line(1, -5, 1);
l2 = reflection(l1, li);

// 曲线及其反射（红色）
cu1 = curve([-3, -3, -2.5, -3, -3, -2.5], [-3, -2, -2, -2, -2.5, -2.5]) << strokeWidth: 3 >>;
cu2 = reflection(cu1, li) << strokeColor: 'red', strokeWidth: 3 >>;

// 多边形及其反射
pol1 = polygon([[-6,-3], [-4,-5], [-5,-1.5]]);
pol2 = reflection(pol1, li);

// 圆及其反射
c1 = circle([-2,-2], [-2, -1]);
c2 = reflection(c1, li);
```

### 3. 圆弧关于直线的反射

```js
// 反射轴
li = line(1, 1, 1);

// 原始圆弧（红色）
a1 = arc([1, 1], [0, 1], [1, 0]) << strokeColor: 'red' >>;

// 反射圆弧（红色）
a2 = reflection(a1, li) << strokeColor: 'red' >>;
```

### 4. 扇形关于直线的反射

```js
// 反射轴
li = line(1, 1, 1);

// 原始扇形（黄色）
s1 = sector([[-3.5,-3], [-3.5, -2], [-3.5,-4]]) <<
    anglePoint: << visible: true >>,
    center: << visible: true >>,
    radiusPoint: << visible: true >>,
    fillColor: 'yellow',
    strokeColor: 'black'
>>;

// 反射扇形（半透明黄色）
s2 = reflection(s1, li) << fillColor: 'yellow', strokeColor: 'black', fillOpacity: 0.5 >>;
```

### 5. 角关于直线的反射

```js
// 反射轴
li = line(1, 1, 1);

// 原始角
an1 = angle([[-4, 3.9], [-3, 4], [-3, 3]]);

// 反射角
an2 = reflection(an1, li);
```

### 6. 设置反射点样式

```js
// 创建反射轴
p1 = point(0, 4);
p2 = point(6, 1);
l1 = line(p1, p2);

// 原始点
p3 = point(3, 3);

// 创建带样式的反射点
rp1 = reflection(p3, l1) <<
    strokeColor: 'red',
    fillColor: 'pink',
    size: 6,
    face: 'circle',
    withLabel: true,
    name: "P'"
>>;
```

### 7. 动态反射

```js
// 创建可拖动的点定义反射轴
A = point(0, 4);
B = point(6, 1);
l1 = line(A, B);

// 可拖动的原始点
P = point(3, 3);

// 创建反射点
RP = reflection(P, l1);

// 当拖动 A、B 或 P 时，反射点 RP 会自动更新位置
```

### 8. 使用变换创建反射

```js
// 创建反射轴
mirrorLine = line(0, 0, 1, 1);  // y = x

// 创建反射变换
reflect = transform(mirrorLine) << type: 'reflect' >>;

// 原始点
A = point(2, 0);

// 使用变换创建反射点
B = point(A, reflect);  // B = (0, 2)

// 或使用两点定义反射轴
p1 = point(-1, 0);
p2 = point(1, 0);
t2 = transform(p1, p2) << type: 'reflect' >>;  // 关于 x 轴反射
C = point(point(0, 2), t2);  // C = (0, -2)
```

### 9. 综合示例：完整反射演示

```js
// 反射轴
li = line(1, 1, 1) << strokeColor: '#aaaaaa' >>;

// 点及其反射
p1 = point(-3, -1) << name: "A" >>;
q1 = reflection(p1, li) << name: "A'", strokeColor: 'red' >>;

// 直线及其反射
l1 = line(1, -5, 1);
l2 = reflection(l1, li) << strokeColor: 'blue', dash: 1 >>;

// 曲线及其反射
cu1 = curve([-3, -3, -2.5, -3, -3, -2.5], [-3, -2, -2, -2, -2.5, -2.5]) << strokeWidth: 3 >>;
cu2 = reflection(cu1, li) << strokeColor: 'red', strokeWidth: 3 >>;

// 多边形及其反射
pol1 = polygon([[-6,-3], [-4,-5], [-5,-1.5]]) << fillColor: 'blue', fillOpacity: 0.3 >>;
pol2 = reflection(pol1, li) << fillColor: 'red', fillOpacity: 0.3 >>;

// 圆及其反射
c1 = circle([-2,-2], [-2, -1]) << strokeColor: 'green' >>;
c2 = reflection(c1, li) << strokeColor: 'orange' >>;

// 圆弧及其反射
a1 = arc([1, 1], [0, 1], [1, 0]) << strokeColor: 'purple' >>;
a2 = reflection(a1, li) << strokeColor: 'purple', dash: 1 >>;

// 扇形及其反射
s1 = sector([[-3.5,-3], [-3.5, -2], [-3.5,-4]]) <<
    anglePoint: << visible: true >>,
    center: << visible: true >>,
    radiusPoint: << visible: true >>,
    fillColor: 'yellow',
    strokeColor: 'black'
>>;
s2 = reflection(s1, li) << fillColor: 'yellow', strokeColor: 'black', fillOpacity: 0.5 >>;

// 角及其反射
an1 = angle([[-4, 3.9], [-3, 4], [-3, 3]]);
an2 = reflection(an1, li) << strokeColor: 'red' >>;
```

## 注意事项

1. **反射轴**：反射需要一条直线作为反射轴
2. **可反射的元素类型**：支持点、直线、圆、曲线、多边形、圆弧、扇形、角等
3. **属性继承**：反射元素可以设置自己的属性，不会自动继承原元素的属性
4. **动态更新**：当原元素或反射轴移动时，反射元素会自动更新位置
5. **变换类型**：使用 `type` 属性可以设置变换类型，'Euclidean'（默认）时圆的反射仍是圆，'projective' 时圆的反射可能是圆锥曲线
6. **与 MirrorElement 的区别**：`reflection` 是关于直线的反射；`mirrorelement` 是关于点的反射（中心对称）
7. **创建方式**：使用 `board.create('reflection', [p1, l1])` 或 JessieCode 语法 `reflection(p1, l1)`

## 相关元素

- [Point](./Point.md) - 点
- [Line](./Line.md) - 直线
- [Circle](./Circle.md) - 圆
- [Curve](./Curve.md) - 曲线
- [Polygon](./Polygon.md) - 多边形
- [Arc](./Arc.md) - 圆弧
- [Sector](./Sector.md) - 扇形
- [Angle](./Angle.md) - 角
- [MirrorElement](./MirrorElement.md) - 镜像元素（关于点的反射）
- [MirrorPoint](./MirrorPoint.md) - 镜像点
- [Transformation](./Transformation.md) - 变换
