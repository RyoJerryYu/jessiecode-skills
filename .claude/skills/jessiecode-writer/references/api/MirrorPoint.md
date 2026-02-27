# MirrorPoint 镜像点

<!-- USAGE_FREQUENCY: advanced -->

## 描述

镜像点是 [MirrorElement](./MirrorElement.md) 的一种特殊情况。

它由一个点关于另一个点的反射（对称）确定。具体来说，给定两个点 p1 和 p2，镜像点 mp 是 p2 关于 p1 的中心对称点，即 p1 是 p2 和 mp 的中点。

**继承关系：**

- `JXG.CoordsElement` → `JXG.GeometryElement` → `JXG.Point` → `MirrorPoint`

## JessieCode 语法

```js
// 通过两个点创建镜像点
// mp 是 p2 关于 p1 的对称点
mp = mirrorpoint(p1, p2);

// 带属性创建
mp = mirrorpoint(p1, p2) <<
    strokeColor: 'red',
    fillColor: 'pink',
    size: 5,
    withLabel: true,
    name: "M"
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| p1 | Point | 反射中心点（对称中心） |
| p2 | Point | 被反射的点（原始点） |

**说明：** 创建的镜像点是 p2 关于 p1 的中心对称点。p1 是 p2 和镜像点的中点。

## 属性

镜像点继承自 Point，因此拥有 Point 的所有属性。常用属性如下：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小（像素或用户坐标） |
| `sizeUnit` | String | 'screen' | 大小单位：'screen' 或 'user' |
| `face` | String | 'circle' | 点的样式 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 点的名称 |
| `visible` | Boolean | true | 是否可见 |
| `fixed` | Boolean | true | 是否固定（镜像点通常是固定的） |
| `showInfobox` | Boolean | true | 是否显示信息框 |

## 方法

镜像点继承自 Point，因此拥有 Point 的所有方法：

| 方法 | 参数 | 描述 |
|------|------|------|
| `X()` | 无 | 获取 x 坐标 |
| `Y()` | 无 | 获取 y 坐标 |
| `move(dx, dy)` | dx, dy: Number | 移动点（镜像点通常不可移动） |
| `HasPoint(p)` | p: Point | 判断点 p 是否与该点重合 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `X(M)` | 获取镜像点 M 的 x 坐标 | `X(mp)` |
| `Y(M)` | 获取镜像点 M 的 y 坐标 | `Y(mp)` |
| `dist(P, Q)` | 计算两点距离 | `dist(p2, mp)` |

## 示例

### 1. 创建基本镜像点

```js
// 创建两个原始点
p1 = point(3, 3);  // 反射中心
p2 = point(6, 1);  // 被反射的点

// 创建镜像点：p2 关于 p1 的对称点
mp = mirrorpoint(p1, p2);
// mp 的坐标将是 (0, 5)，因为 p1(3,3) 是 p2(6,1) 和 mp(0,5) 的中点
```

### 2. 设置镜像点样式

```js
// 创建带样式的镜像点
mp = mirrorpoint(p1, p2) <<
    strokeColor: 'red',
    fillColor: 'pink',
    size: 6,
    face: 'circle',
    withLabel: true,
    name: "M"
>>;
```

### 3. 镜像点的动态效果

```js
// 创建可拖动的点
A = point(2, 2);
B = point(4, 1);

// 创建镜像点
M = mirrorpoint(A, B);

// 当拖动 A 或 B 时，M 会自动更新位置
// M 始终是 B 关于 A 的对称点
```

### 4. 验证中点关系

```js
// 创建原始点和镜像点
p1 = point(3, 3);
p2 = point(6, 1);
mp = mirrorpoint(p1, p2);

// 验证：p1 是 p2 和 mp 的中点
// p2 的坐标：(6, 1)
// mp 的坐标：(0, 5)
// 中点坐标：((6+0)/2, (1+5)/2) = (3, 3) = p1
```

### 5. 构建对称图形

```js
// 创建三角形
A = point(1, 1);
B = point(4, 1);
C = point(2, 4);

// 创建对称中心
O = point(0, 0);

// 创建三角形的镜像点
A_prime = mirrorpoint(O, A);
B_prime = mirrorpoint(O, B);
C_prime = mirrorpoint(O, C);

// 连接原始三角形和镜像三角形
tri1 = polygon(A, B, C);
tri2 = polygon(A_prime, B_prime, C_prime);
```

### 6. 使用坐标创建

```js
// 直接使用坐标创建点，然后创建镜像点
p1 = point(0, 0);  // 原点作为对称中心
p2 = point(5, 3);  // 第一象限的点

// 镜像点在第三象限
mp = mirrorpoint(p1, p2);  // mp 坐标为 (-5, -3)
```

## 注意事项

1. **计算原理**：镜像点 mp 是 p2 关于 p1 的中心对称点，满足 `p1 = (p2 + mp) / 2`，即 `mp = 2 * p1 - p2`

2. **动态更新**：当 p1 或 p2 被拖动时，镜像点会自动更新位置

3. **固定属性**：镜像点通常是固定的（fixed: true），不能直接拖动

4. **与反射的区别**：`mirrorpoint` 是点关于点的对称；点关于直线的对称使用其他方法

5. **父对象要求**：必须提供两个有效的 Point 对象作为参数

## 相关元素

- [Point](./Point.md) - 点
- [MirrorElement](./MirrorElement.md) - 镜像元素
- [Reflection](./Reflection.md) - 反射变换
- [Midpoint](./Midpoint.md) - 中点
- [Transform](./Transform.md) - 变换
