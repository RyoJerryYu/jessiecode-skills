# ImplicitCurve 隐式曲线

## 描述

隐式曲线是由两个坐标变量（通常是 *x* 和 *y*）之间的隐式方程定义的平面曲线。例如，单位圆由隐式方程 x² + y² = 1 定义。一般来说，每条隐式曲线都由形式为 *f(x, y) = 0* 的方程定义，其中 *f* 是一个双变量函数。（来源：[Wikipedia](https://en.wikipedia.org/wiki/Implicit_curve)）

函数 *f* 的偏导数是可选的。如果未提供，则使用数值导数代替。这对于大多数实际应用场景已经足够好。但如果要提供，则必须同时提供两个偏导数。

如果隐式曲线算法失败，最有效的调整属性是 [ImplicitCurve#resolution_outer](../symbols/ImplicitCurve.html#resolution_outer)、[ImplicitCurve#resolution_inner](../symbols/ImplicitCurve.html#resolution_inner)、[ImplicitCurve#alpha_0](../symbols/ImplicitCurve.html#alpha_0)、[ImplicitCurve#h_initial](../symbols/ImplicitCurve.html#h_initial)、[ImplicitCurve#h_max](../symbols/ImplicitCurve.html#h_max) 和 [ImplicitCurve#qdt_box](./ImplicitCurve.md#qdt_box)。

*定义于：* [curve.js](./src/src_base_curve.js.md)。
继承自 [JXG.Curve](./JXG.Curve.md)。

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
   ↳ **[JXG.Curve](./JXG.Curve.md)**
         ↳ **ImplicitCurve**

## JessieCode 语法

```js
// 基本语法 - 通过函数创建隐式曲线
c = implicitcurve(f);

// 通过字符串表达式创建
c = implicitcurve('x^2 + y^2 - 1');

// 带偏导数创建（可选）
c = implicitcurve(f, dfx, dfy);

// 带定义域创建
c = implicitcurve(f, [x_min, x_max], [y_min, y_max]);

// 带属性创建
c = implicitcurve(f) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    resolution_outer: 20,
    resolution_inner: 20
>>;
```

## 参数

### 可能的父元素数组组合

| 参数 | 类型 | 描述 |
|------|------|------|
| f | Function/String | 方程 *f(x,y)=0* 左侧的双变量函数。如果 f 以字符串形式提供，则必须使用变量 'x' 和 'y' |
| dfx | Function/String | 可选，关于第一个变量的偏导数。如果 dfx 以字符串形式提供，则必须使用变量 'x' 和 'y' |
| dfy | Function/String | 可选，关于第二个变量的偏导数。如果 dfy 以字符串形式提供，则必须使用变量 'x' 和 'y' |
| rangex | Array/Function | 可选，长度为 2 的数组，形式为 [x_min, x_max]，设置隐式曲线 x 坐标的定义域。如果未提供，则使用画布的边界框（+ 属性 "margin"） |
| rangey | Array/Function | 可选，长度为 2 的数组，形式为 [y_min, y_max]，设置隐式曲线 y 坐标的定义域。如果未提供，则使用画布的边界框（+ 属性 "margin"） |

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `strokeOpacity` | Number | 1.0 | 描边透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 曲线名称 |

### 隐式曲线专用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `alpha_0` | Number | 0.05 | 两条连续切线之间的角度 α0：决定曲线的平滑度 |
| `delta_0` | Number | 0.05 | 预测点到曲线的允许距离（用户坐标单位） |
| `h_critical` | Number | 0.001 | 如果 h 低于此阈值（用户坐标单位），则退出该分量的跟踪阶段 |
| `h_initial` | Number | 0.1 | 初始步长（用户坐标单位） |
| `h_max` | Number | 0.5 | 最大步长（用户坐标单位） |
| `kappa_0` | Number | 0.2 | 期望牛顿迭代步数的倒数 |
| `loop_detection` | Boolean | true | 使用 Gosper 的循环检测器 |
| `loop_dir` | Number | 0.99 | 检测循环的最小 acos 角度值 |
| `loop_dist` | Number | 0.09 | 检测循环的允许距离（用户坐标单位乘以实际步长） |
| `margin` | Number | 1 | 定义 JSXGraph 画布周围的边距（用户坐标单位），隐式曲线在此范围内绘制 |
| `max_steps` | Number | 1024 | 隐式曲线一个分量的最大迭代次数 |
| `qdt_box` | Number | 0.2 | 在四叉树中搜索现有线段的盒子大小的一半（用户坐标单位） |
| `resolution_inner` | Number | 5 | 搜索隐式曲线分量的垂直分辨率（像素）。数值越小运行时间越长；数值越大可能遗漏分量。最小值为 0.01 |
| `resolution_outer` | Number | 5 | 搜索隐式曲线分量的垂直线之间的水平分辨率（像素）。数值越小运行时间越长；数值越大可能遗漏分量。最小值为 0.01 |
| `tol_0` | Number | JXG.Math.eps | 寻找分量跟踪阶段起点的容差 |
| `tol_cusp` | Number | 0.05 | 尖点/分岔检测的容差 |
| `tol_newton` | Number | 1.0e-7 | 牛顿迭代的容差 |
| `tol_progress` | Number | 0.0001 | 如果两个点之间的距离小于此值，则退出该分量的跟踪阶段 |

## 字段

| 字段 | 类型 | 描述 |
|------|------|------|
| `domain` | Array | 定义搜索 f(x,y)=0 的定义域。默认为 null，表示使用画布的边界框。使用 domain 时，visProp.margin 将被忽略 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `f()` | 无 | 方程 *f(x,y)=0* 左侧的双变量函数 |
| `dfx()` | 无 | 方程 *f(x,y)=0* 左侧关于第一个变量的偏导数。如果为 null，则使用数值导数 |
| `dfy()` | 无 | 方程 *f(x,y)=0* 左侧关于第二个变量的偏导数。如果为 null，则使用数值导数 |

## 示例

### 1. 创建基本隐式曲线

```js
// 创建椭圆曲线 x²/16 + y² = 1
var f = (x, y) => 1/16 * x^2 + y^2 - 1;
c = implicitcurve(f) <<
    strokeWidth: 3,
    strokeColor: 'red',
    strokeOpacity: 0.8
>>;
```

### 2. 动态隐式曲线

```js
// 创建滑块
a = slider([-3, 6], [3, 6], [-3, 1, 3]) <<
    name: 'a',
    stepWidth: 0.1
>>;

// 创建随滑块变化的隐式曲线
f = (x, y) => x^2 - 2*x*y - 2*x + (V(a) + 1)*y^2 + (4*V(a) + 2)*y + 4*V(a) - 3;
c = implicitcurve(f) <<
    strokeWidth: 3,
    strokeColor: 'red',
    strokeOpacity: 0.8,
    resolution_outer: 20,
    resolution_inner: 20
>>;
```

### 3. 使用字符串表达式

```js
// 使用字符串表达式创建曲线 |x*y| = 3
c = implicitcurve('abs(x*y) - 3') <<
    strokeWidth: 3,
    strokeColor: 'red',
    strokeOpacity: 0.8
>>;
```

### 4. 多条等值线

```js
// 创建多条等值线
niveauline = [0.5, 1, 1.5, 2];

// 使用循环创建多条曲线
for (i = 0; i < length(niveauline); i = i + 1) {
    c = implicitcurve(
        (x, y) => sqrt(x) * sqrt(y) - niveauline[i],
        [0.25, 3],  // x 定义域
        [0.5, 4]    // y 定义域
    ) <<
        strokeWidth: 2,
        strokeColor: 'red',
        strokeOpacity: (1 + i) / length(niveauline),
        needsRegularUpdate: false
    >>;
}
```

### 5. 带偏导数的隐式曲线

```js
// 定义函数 f(x,y) = x² + y² - 1（单位圆）
f = (x, y) => x^2 + y^2 - 1;

// 定义偏导数
dfx = (x, y) => 2*x;  // ∂f/∂x
dfy = (x, y) => 2*y;  // ∂f/∂y

// 创建带偏导数的隐式曲线（计算更快更准确）
c = implicitcurve(f, dfx, dfy) <<
    strokeWidth: 2,
    strokeColor: 'blue'
>>;
```

### 6. 调整分辨率属性

```js
// 对于复杂曲线，调整分辨率属性以获得更好的效果
f = (x, y) => sin(x) * cos(y) - 0.5;

c = implicitcurve(f) <<
    strokeWidth: 2,
    strokeColor: 'purple',
    resolution_outer: 10,   // 降低水平分辨率以加快计算
    resolution_inner: 10,   // 降低垂直分辨率以加快计算
    h_initial: 0.05,        // 减小初始步长
    h_max: 0.2              // 减小最大步长
>>;
```

### 7. 限制定义域

```js
// 只在特定范围内绘制曲线
f = (x, y) => x^2 - y^2 - 1;  // 双曲线

// 限制 x 和 y 的范围
c = implicitcurve(f, [-5, 5], [-3, 3]) <<
    strokeWidth: 2,
    strokeColor: 'green'
>>;
```

## 注意事项

1. **偏导数可选但推荐**：提供偏导数可以提高计算速度和准确性，但对于大多数情况数值导数已足够
2. **分辨率调整**：如果曲线显示不完整，尝试减小 `resolution_outer` 和 `resolution_inner` 的值
3. **定义域**：可以使用 `domain` 属性或参数形式 `[x_min, x_max], [y_min, y_max]` 限制曲线的绘制范围
4. **性能优化**：对于复杂曲线，调整 `h_initial`、`h_max` 和 `max_steps` 可以平衡性能和精度
5. **字符串表达式**：使用字符串形式时，必须使用变量名 'x' 和 'y'
6. **多条曲线**：可以通过循环创建多条等值线，设置 `needsRegularUpdate: false` 可以提高性能

## 相关元素

- [Curve](./Curve.md) - 曲线
- [Functiongraph](./Functiongraph.md) - 函数图像
- [Conic](./Conic.md) - 圆锥曲线
- [Circle](./Circle.md) - 圆
- [Ellipse](./Ellipse.md) - 椭圆
- [Hyperbola](./Hyperbola.md) - 双曲线
- [Parabola](./Parabola.md) - 抛物线
