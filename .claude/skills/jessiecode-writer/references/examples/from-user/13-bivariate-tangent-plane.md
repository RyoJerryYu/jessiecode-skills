# 二元函数切平面 (Tangent Plane of Bivariate Function)

## 图形描述

对于二元函数 $f(x,y) = x^2+y^2$，其一点上的全微分为：

$$
df = \frac{ \partial f }{ \partial x } dx + \frac{ \partial f }{ \partial y } dy = 2xdx+2ydy
$$

$(x_0, y_0)$ 处的切平面为：

$$
\begin{align}
&& P(x,y) - f(x_{0},y_{0}) &= \frac{ \partial f }{ \partial x }(x-x_{0}) + \frac{ \partial f }{ \partial y } (y-y_{0}) \\
\implies && P(x,y) &= 2x_{0}x + 2y_{0}y -x_{0}^2-y_{0}^2
\end{align}
$$

移动右下角横竖两个滑块，观察切平面的变化与 $\frac{ \partial f }{ \partial x }$，$\frac{ \partial f }{ \partial y }$ 的关系。

## JessieCode 代码

```js
bound = [-1, 1];
zbound = [0, 2];
planeStyle = <<
    fillOpacity: 0.2,
    mesh3d: <<
        stepWidthU: 0.2,
        stepWidthV: 0.2,
        strokeOpacity: 0.2
    >>
>>;
view = view3d([-7, -7], [14, 14], [bound, bound, zbound]) <<
    xPlaneRear: planeStyle,
    yPlaneRear: planeStyle,
    zPlaneRear: planeStyle,
    projection: 'central'
>>;

F = function(x, y) { return x^2 + y^2; };
fg = functiongraph3d(view, F, bound, bound) << strokeWidth: 0.5, stepsU: 70, stepsV: 70 >>;

px = slider([4, -8], [8, -8], [-1, 0, 1]);
py = slider([4, -8], [4, -4], [-1, 1, 1]);

PX = function() { return px.Value(); };
PY = function() { return py.Value(); };
PZ = function() { return F(px.Value(), py.Value()); };
P = point3d(view, PX, PY, PZ);

tanXY = function(x, y) {
    return 2 * PX() * x + 2 * PY() * y - PX() * PX() - PY() * PY();
};
functiongraph3d(view, tanXY, bound, bound);
```

## 知识点

- **二元函数**：z = f(x,y) = x² + y²，这是一个旋转抛物面
- **偏导数**：
  - ∂f/∂x = 2x：函数对 x 的变化率
  - ∂f/∂y = 2y：函数对 y 的变化率
- **全微分**：df = (∂f/∂x)dx + (∂f/∂y)dy = 2xdx + 2ydy
- **切平面方程**：P(x,y) = 2x₀x + 2y₀y - x₀² - y₀²
- **几何意义**：切平面在某点与曲面相切，局部近似曲面
- **三维可视化**：使用透视投影展示三维曲面和切平面

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| view3d | `view3d(pos, size, bounds)` | 创建三维视图 |
| function | `function(x,y){...}` | 定义二元函数 |
| functiongraph3d | `functiongraph3d(view, f, boundX, boundY)` | 创建三维函数图像 |
| point3d | `point3d(view, x, y, z)` | 创建三维点 |
| slider | `slider(p1, p2, [min, max, step])` | 创建滑块控制器 |
| 样式对象 | `planeStyle` | 定义平面样式并复用 |
| 样式属性 | `<<mesh3d: ...>>` | 设置三维网格属性 |
| 样式属性 | `<<projection: "central">>` | 设置透视投影 |

---
*来源：04-Cool Showcase/02-割圆八线.md（实际内容：二元函数切平面）*
