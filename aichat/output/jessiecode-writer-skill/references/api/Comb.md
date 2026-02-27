# Comb 梳状标记

## 描述

梳状标记（Comb）用于可视化不等式的定义域。梳状元素由两个点定义，显示为一系列平行的斜线，常用于表示平面区域或不等式解集。

## JessieCode 语法

```js
// 基本语法 - 创建水平梳状标记
c = comb(point1, point2);

// 通过坐标创建
c = comb([x1, y1], [x2, y2]);

// 带属性创建
c = comb(A, B) <<
    width: 0.4,
    frequency: 0.2,
    angle: PI / 3,
    strokeColor: 'blue'
>>;

// 使用动态属性
c = comb(A, B) <<
    width: function() { return slider.Value(); },
    frequency: 0.1,
    angle: PI / 4
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point/Array/Function | 第一个点（Point 对象、坐标数组或返回点的函数） |
| point2 | Point/Array/Function | 第二个点（Point 对象、坐标数组或返回点的函数） |

**说明**：如果提供坐标数组而非 Point 对象，会自动创建固定的不可见点。也可以使用函数返回点或坐标数组。

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `width` | Number/Function | 0.4 | 梳状标记的宽度（高度） |
| `frequency` | Number/Function | 0.2 | 梳齿的频率（间距） |
| `angle` | Number/Function | PI / 3 | 梳齿的角度（弧度），默认为 60 度 |
| `reverse` | Boolean/Function | false | 是否从右向左显示梳齿 |
| `strokeColor` | String | '#000000' | 梳齿颜色 |
| `strokeWidth` | Number | 1 | 梳齿线宽 |
| `curve` | Object | - | 曲线相关属性（继承自 Curve） |

### 属性说明

**width（宽度）**
- 控制梳状标记的高度
- 可以是固定数值或返回数值的函数
- 默认值：0.4

**frequency（频率）**
- 控制梳齿之间的间距
- 值越小，梳齿越密集
- 默认值：0.2

**angle（角度）**
- 梳齿相对于基线的倾斜角度
- 以弧度为单位
- `PI / 3` = 60 度（默认）
- `PI / 4` = 45 度
- `PI / 2` = 90 度（垂直）

**reverse（反向）**
- `false`：从左向右（默认）
- `true`：从右向左

## 示例

### 1. 创建基本梳状标记

```js
// 简单的水平梳状标记，端点不可见
c = comb([1, 0], [3, 0]);

// 使用已有点创建
A = point(1, 0);
B = point(3, 0);
c = comb(A, B);
```

### 2. 设置梳状样式

```js
// 较宽的梳状标记，梳齿更密集
c1 = comb([0, 1], [4, 1]) <<
    width: 0.6,
    frequency: 0.1,
    strokeColor: 'blue'
>>;

// 45 度角的梳齿
c2 = comb([0, 0], [4, 0]) <<
    angle: PI / 4,
    width: 0.5,
    strokeColor: 'green'
>>;

// 垂直梳齿
c3 = comb([0, -1], [4, -1]) <<
    angle: PI / 2,
    frequency: 0.15
>>;
```

### 3. 在 x 轴上表示区间

```js
// 创建 x 轴
A = point(-5, 0);
B = point(5, 0);
xAxis = line(A, B) << lastArrow: true >>;

// 表示区间 [-3, -1]
P1 = glider(-3, 0, xAxis);
P2 = glider(-1, 0, xAxis);
c = comb(P1, P2) <<
    width: 0.4,
    frequency: 0.1,
    angle: PI / 3,
    strokeColor: 'red'
>>;
```

### 4. 动态梳状标记（使用滑块）

```js
// 创建滑块控制宽度和频率
s = slider([1, 3], [4, 3], [0.1, 0.3, 0.8]);

// 创建可在 x 轴上滑动的点
P1 = glider(-3, 0, xAxis);
P2 = glider(-1, 0, xAxis);

// 梳状属性随滑块变化
c = comb(P1, P2) <<
    width: function() { return 4 * s.Value(); },
    reverse: function() { return s.Value() < 0.5 ? false : true; },
    frequency: function() { return s.Value(); },
    angle: function() { return s.Value() * PI / 2; },
    curve: <<
        strokeColor: 'red'
    >>
>>;
```

### 5. 表示不等式区域

```js
// 表示 x > 2 的区域
startPoint = point(2, 0) << visible: false >>;
endPoint = point(6, 0) << visible: false >>;
c = comb(startPoint, endPoint) <<
    width: 0.5,
    frequency: 0.08,
    angle: PI / 4,
    strokeColor: 'gray',
    opacity: 0.7
>>;

// 标记边界点（空心表示不包含）
boundary = point(2, 0) <<
    face: 'circle',
    fillColor: 'white',
    size: 4
>>;
```

### 6. 反向梳状标记

```js
// 正常方向（左到右）
c1 = comb([1, 1], [4, 1]) <<
    width: 0.3,
    strokeColor: 'blue'
>>;

// 反向（右到左）
c2 = comb([1, 0], [4, 0]) <<
    width: 0.3,
    reverse: true,
    strokeColor: 'red'
>>;
```

### 7. 组合使用

```js
// 创建多条平行线表示多个区间
c1 = comb([0, 0], [2, 0]) << width: 0.3, frequency: 0.1 >>;
c2 = comb([0, 1], [2, 1]) << width: 0.3, frequency: 0.1 >>;
c3 = comb([0, 2], [2, 2]) << width: 0.3, frequency: 0.1 >>;

// 不同角度的梳状标记
c4 = comb([3, 0], [5, 0]) << angle: PI / 6, width: 0.4 >>;
c5 = comb([3, 1], [5, 1]) << angle: PI / 3, width: 0.4 >>;
c6 = comb([3, 2], [5, 2]) << angle: PI / 2, width: 0.4 >>;
```

## 注意事项

1. **梳状方向**：默认从左向右，使用 `reverse: true` 可从右向左
2. **角度单位**：`angle` 属性使用弧度，不是角度。`PI / 3` = 60 度
3. **频率与密度**：`frequency` 值越小，梳齿越密集
4. **继承 Curve**：Comb 继承自 Curve，可以使用曲线的相关属性
5. **动态属性**：所有属性都可以使用函数，实现动态效果
6. **端点可见性**：定义梳状的点默认不可见，除非显式设置 `visible: true`

## 相关元素

- [Curve](./Curve.md) - 曲线（父类）
- [Segment](./Segment.md) - 线段
- [Arc](./Arc.md) - 圆弧（用于表示区间）
- [SlopeTriangle](./SlopeTriangle.md) - 斜率三角形
