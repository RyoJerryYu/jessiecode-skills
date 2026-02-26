# Inequality 不等式区域

## 描述

不等式区域表示线性不等式或函数图像不等式的解集所对应的区域。例如，形式为 y <= f(x) 的不等式。

*定义于：* [composition.js](./src/src_element_composition.js.md)
*继承自：* [JXG.Curve](./JXG.Curve.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
&nbsp;&nbsp;&nbsp;↳ **[JXG.Curve](./JXG.Curve.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **Inequality**

## JessieCode 语法

```js
// 基于直线创建不等式区域（直线下方区域）
ineq = inequality(l);

// 基于直线创建不等式区域（直线上方区域）
ineq = inequality(l) << inverse: true >>;

// 基于函数图像创建不等式区域
ineq = inequality(f);

// 带属性创建
ineq = inequality(l) <<
    fillColor: 'blue',
    fillOpacity: 0.3,
    inverse: true
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| line | Line | 直线对象，区域为该直线下方的不等式区域 |
| functiongraph | Functiongraph | 函数图像对象，区域为该函数图像下方的不等式区域 |

### 父元素组合说明

**直线 (Line)**
- 绘制的区域将是该直线下方的区域
- 使用属性 `inverse: true` 时，显示"大于或等于"的不等式区域

**函数图像 (Functiongraph)**
- 绘制的区域将是该函数图像下方的区域
- 使用属性 `inverse: true` 时，显示"大于或等于"的不等式区域

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fillColor` | String | '#FFFF00' | 填充颜色 |
| `fillOpacity` | Number | 0.3 | 填充透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `inverse` | Boolean | false | 是否反转不等式方向 |

### 关键属性

#### inverse（布尔值）

默认情况下，不等式为"小于（或等于）"。设置为 `true` 时，将考虑"大于（或等于）"的不等式。

*定义于：* [options.js](./src/src_options.js.md)

**默认值：** `false`

```js
// 小于等于（默认）
ineq1 = inequality(l);

// 大于等于
ineq2 = inequality(l) << inverse: true >>;
```

## 方法

继承自 [JXG.Curve](./JXG.Curve.md) 和 [JXG.GeometryElement](./JXG.GeometryElement.md) 的方法。

## 示例

### 1. 基于两点连线创建不等式区域

```js
// 创建两个点
p = point(1, 3);
q = point(-2, -4);

// 创建直线
l = line(p, q);

// 创建不等式区域（直线下方）
ineq = inequality(l);
```

### 2. 基于直线方程创建不等式区域

```js
// 绘制不等式
//     y >= 2/3 x + 1
// 或
//     0 >= -3y + 2x + 1

// 使用直线方程系数创建直线 (1 + 2x - 3y = 0)
l = line(1, 2, -3);

// 创建上方区域（inverse: true 表示大于等于）
ineq = inequality(l) << inverse: true >>;
```

### 3. 基于函数图像创建不等式区域

```js
// 创建正弦函数图像
f = functiongraph('sin(x)', -2*PI, 2*PI);

// 函数图像下方区域（y <= sin(x)）
ineq_lower = inequality(f);

// 函数图像上方区域（y >= sin(x)）
ineq_greater = inequality(f) <<
    inverse: true,
    fillColor: 'yellow'
>>;
```

### 4. 设置填充样式

```js
// 创建直线
l = line(0, 0, 1, 1);

// 半透明红色区域
ineq1 = inequality(l) <<
    fillColor: 'red',
    fillOpacity: 0.2
>>;

// 半透明蓝色区域（上方）
ineq2 = inequality(l) <<
    fillColor: 'blue',
    fillOpacity: 0.3,
    inverse: true
>>;
```

### 5. 多个不等式区域（线性规划）

```js
// 创建多条直线
l1 = line(0, 1, -2);   // y = -x/2
l2 = line(0, -1, 1);   // y = x
l3 = line(-4, 0, 1);   // y = 4

// 创建多个不等式区域
ineq1 = inequality(l1) << fillColor: 'red', fillOpacity: 0.2 >>;
ineq2 = inequality(l2) << fillColor: 'green', fillOpacity: 0.2, inverse: true >>;
ineq3 = inequality(l3) << fillColor: 'blue', fillOpacity: 0.2 >>;
```

### 6. 动态不等式区域

```js
// 创建滑块
m = slider(-2, 2, 0.1);
b = slider(-3, 3, 0.1);

// 创建动态直线
l = line(0, 0, 1, m);  // 初始直线

// 或使用函数创建动态点
P = point(function() { return 0; }, function() { return b; });
Q = point(function() { return 1; }, function() { return m + b; });
l = line(P, Q);

// 创建动态不等式区域
ineq = inequality(l) << fillOpacity: 0.3 >>;
```

## 注意事项

1. **不等式方向**：默认显示"小于等于"区域，使用 `inverse: true` 显示"大于等于"区域
2. **填充样式**：可以通过 `fillColor` 和 `fillOpacity` 自定义区域的填充颜色和透明度
3. **依赖元素**：不等式区域依赖于直线或函数图像，当父元素变化时区域会自动更新
4. **创建方式**：在 JessieCode 中直接使用 `inequality()` 函数创建，无需调用 `board.create()`

## 相关元素

- [Line](./Line.md) - 直线
- [Functiongraph](./Functiongraph.md) - 函数图像
- [Curve](./Curve.md) - 曲线
- [Polygon](./Polygon.md) - 多边形
