# MirrorElement 镜像元素

<!-- USAGE_FREQUENCY: advanced -->

## 描述

将一个点、直线、圆、曲线、多边形关于给定点进行反射。

*定义于：* [composition.js](./src/src_element_composition.js.md)
*继承自* [JXG.GeometryElement](./JXG.GeometryElement.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
      ↳ **MirrorElement**

## JessieCode 语法

```js
// 基本语法 - 创建点关于点的镜像
A = point(-3, -1);
mirrorPoint = point(-1, -1);
A' = mirrorelement(A, mirrorPoint);

// 创建直线关于点的镜像
l1 = line(1, -5, 1);
l2 = mirrorelement(l1, mirrorPoint);

// 创建曲线关于点的镜像
cu1 = curve([-3, -3, -2.5, -3, -3, -2.5], [-3, -2, -2, -2, -2.5, -2.5]) << strokeWidth: 3 >>;
cu2 = mirrorelement(cu1, mirrorPoint) << strokeColor: 'red', strokeWidth: 3 >>;

// 创建多边形关于点的镜像
pol1 = polygon([[-6,-2], [-4,-4], [-5,-0.5]]);
pol2 = mirrorelement(pol1, mirrorPoint);

// 创建圆关于点的镜像
c1 = circle([-6,-6], [-6, -5]);
c2 = mirrorelement(c1, mirrorPoint);

// 带属性创建
A' = mirrorelement(A, mirrorPoint) <<
    strokeColor: 'red',
    fillColor: 'pink',
    withLabel: true,
    name: "A'"
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| p1 | Point/Line/Circle/Curve/Polygon | 要被反射的元素（点、直线、圆、曲线、多边形） |
| p2 | Point | 反射中心点 |

### 父元素组合说明

| 父元素组合 | 描述 |
|-----------|------|
| `p1` (Point/Line/Circle/Curve/Polygon), `p2` (Point) | 构造的元素是 p1 关于 p2 的镜像 |

## 属性

MirrorElement 继承 [JXG.GeometryElement](./JXG.GeometryElement.md) 的所有属性，常用属性如下：

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

### 特定元素的属性

根据被反射的元素类型，可以设置相应的特定属性：

- **点**：`size`, `face`, `fixed` 等
- **直线/曲线**：`dash`, `straightFirst`, `straightLast` 等
- **圆**：`fillOpacity`, `strokeOpacity` 等
- **多边形**：`fillOpacity`, `borders` 等

## 示例

### 1. 点关于点的镜像

```js
// 反射中心点
mirror = point(-1, -1) << color: '#aaaaaa' >>;

// 原始点
A = point(-3, -1) << name: "A" >>;

// 镜像点
A' = mirrorelement(A, mirror) << name: "A'" >>;
```

### 2. 直线关于点的镜像

```js
// 反射中心点
mirror = point(-1, -1) << color: '#aaaaaa' >>;

// 原始直线
l1 = line(1, -5, 1);

// 镜像直线
l2 = mirrorelement(l1, mirror);
```

### 3. 曲线关于点的镜像

```js
// 反射中心点
mirror = point(-1, -1) << color: '#aaaaaa' >>;

// 原始曲线
cu1 = curve([-3, -3, -2.5, -3, -3, -2.5], [-3, -2, -2, -2, -2.5, -2.5]) << strokeWidth: 3 >>;

// 镜像曲线（红色）
cu2 = mirrorelement(cu1, mirror) << strokeColor: 'red', strokeWidth: 3 >>;
```

### 4. 多边形关于点的镜像

```js
// 反射中心点
mirror = point(-1, -1) << color: '#aaaaaa' >>;

// 原始多边形
pol1 = polygon([[-6,-2], [-4,-4], [-5,-0.5]]);

// 镜像多边形
pol2 = mirrorelement(pol1, mirror);
```

### 5. 圆关于点的镜像

```js
// 反射中心点
mirror = point(-1, -1) << color: '#aaaaaa' >>;

// 原始圆
c1 = circle([-6,-6], [-6, -5]);

// 镜像圆
c2 = mirrorelement(c1, mirror);
```

### 6. 圆弧关于点的镜像

```js
// 反射中心点
mirror = point(-1, -1) << color: '#aaaaaa' >>;

// 原始圆弧（红色）
a1 = arc([1, 1], [0, 1], [1, 0]) << strokeColor: 'red' >>;

// 镜像圆弧（红色）
a2 = mirrorelement(a1, mirror) << strokeColor: 'red' >>;
```

### 7. 扇形关于点的镜像

```js
// 反射中心点
mirror = point(-1, -1) << color: '#aaaaaa' >>;

// 原始扇形（黄色）
s1 = sector([[-3.5,-3], [-3.5, -2], [-3.5,-4]]) <<
    anglePoint: << visible: true >>,
    center: << visible: true >>,
    radiusPoint: << visible: true >>,
    fillColor: 'yellow',
    strokeColor: 'black'
>>;

// 镜像扇形（半透明黄色）
s2 = mirrorelement(s1, mirror) << fillColor: 'yellow', strokeColor: 'black', fillOpacity: 0.5 >>;
```

### 8. 角关于点的镜像

```js
// 反射中心点
mirror = point(-1, -1) << color: '#aaaaaa' >>;

// 原始角
an1 = angle([[-4,3.9], [-3, 4], [-3, 3]]);

// 镜像角
an2 = mirrorelement(an1, mirror);
```

### 9. 综合示例：多种元素的镜像

```js
// 反射中心点
mirror = point(-1, -1) << color: '#aaaaaa' >>;

// 点及其镜像
p1 = point(-3, -1) << name: "A" >>;
q1 = mirrorelement(p1, mirror) << name: "A'" >>;

// 直线及其镜像
l1 = line(1, -5, 1);
l2 = mirrorelement(l1, mirror);

// 曲线及其镜像
cu1 = curve([-3, -3, -2.5, -3, -3, -2.5], [-3, -2, -2, -2, -2.5, -2.5]) << strokeWidth: 3 >>;
cu2 = mirrorelement(cu1, mirror) << strokeColor: 'red', strokeWidth: 3 >>;

// 多边形及其镜像
pol1 = polygon([[-6,-2], [-4,-4], [-5,-0.5]]);
pol2 = mirrorelement(pol1, mirror);

// 圆及其镜像
c1 = circle([-6,-6], [-6, -5]);
c2 = mirrorelement(c1, mirror);
```

## 注意事项

1. **反射中心**：镜像元素需要一个反射中心点（Point 类型）
2. **可反射的元素类型**：支持点、直线、圆、曲线、多边形、圆弧、扇形、角等
3. **属性继承**：镜像元素可以设置自己的属性，不会自动继承原元素的属性
4. **动态更新**：当原元素或反射中心点移动时，镜像元素会自动更新位置
5. **创建方式**：使用 `board.create('mirrorelement', [p1, p2])` 或 JessieCode 语法 `mirrorelement(p1, p2)`

## 相关元素

- [Point](./Point.md) - 点
- [Line](./Line.md) - 直线
- [Circle](./Circle.md) - 圆
- [Curve](./Curve.md) - 曲线
- [Polygon](./Polygon.md) - 多边形
- [Arc](./Arc.md) - 圆弧
- [Sector](./Sector.md) - 扇形
- [Angle](./Angle.md) - 角
- [Transformation](./Transformation.md) - 变换
