# 立方体投影 (Cube Projection)

## 图形描述

展示一个立方体在三维空间中的投影。左侧是原始立方体，右侧是经过线性变换后的投影图像。拖动滑块可以旋转立方体，观察投影如何随角度变化。

## JessieCode 代码

```js
bound = [-5, 5];
view = view3d([-7, -7], [14, 14], [bound, bound, bound]) <<
    xPlaneRear: << visible: false >>,
    yPlaneRear: << visible: false >>,
    projection: 'central'
>>;
sli = slider([3, 8], [8, 8], [0, 1, 6]);

pStyle = << withLabel: true >>;
p0 = point3d(view, function() { return -4 + 2 * cos(sli.Value()); }, function() { return 2 * sin(sli.Value()); }, -sqrt(2)) pStyle;
p1 = point3d(view, function() { return -4 + 2 * cos(sli.Value() + PI / 2); }, function() { return 2 * sin(sli.Value() + PI / 2); }, -sqrt(2)) pStyle;
p2 = point3d(view, function() { return -4 + 2 * cos(sli.Value() + PI); }, function() { return 2 * sin(sli.Value() + PI); }, -sqrt(2)) pStyle;
p3 = point3d(view, function() { return -4 + 2 * cos(sli.Value() + 3 * PI / 2); }, function() { return 2 * sin(sli.Value() + 3 * PI / 2); }, -sqrt(2)) pStyle;


p0t = point3d(view, function() { return -4 + 2 * cos(sli.Value()); }, function() { return 2 * sin(sli.Value()); }, sqrt(2)) pStyle;
p1t = point3d(view, function() { return -4 + 2 * cos(sli.Value() + PI / 2); }, function() { return 2 * sin(sli.Value() + PI / 2); }, sqrt(2)) pStyle;
p2t = point3d(view, function() { return -4 + 2 * cos(sli.Value() + PI); }, function() { return 2 * sin(sli.Value() + PI); }, sqrt(2)) pStyle;
p3t = point3d(view, function() { return -4 + 2 * cos(sli.Value() + 3 * PI / 2); }, function() { return 2 * sin(sli.Value() + 3 * PI / 2); }, sqrt(2)) pStyle;

polygon3d(view, p0, p1, p2, p3);
polygon3d(view, p0t, p1t, p2t, p3t);
polygon3d(view, p0, p1, p1t, p0t);
polygon3d(view, p2, p3, p3t, p2t);

plane3d(view, [5, 0, 0], [0, 0, 1], [0, -2, 0]);

jStyle = << withLabel: false >>;
j0 = point3d(view, 5, function() { return 2 * sin(sli.Value()); }, function() { return -sqrt(2) + (9 - 2 * cos(sli.Value())) / 6; }) jStyle;
j1 = point3d(view, 5, function() { return 2 * sin(sli.Value() + PI / 2); }, function() { return -sqrt(2) + (9 - 2 * cos(sli.Value() + PI / 2)) / 6; }) jStyle;
j2 = point3d(view, 5, function() { return 2 * sin(sli.Value() + PI); }, function() { return -sqrt(2) + (9 - 2 * cos(sli.Value() + PI)) / 6; }) jStyle;
j3 = point3d(view, 5, function() { return 2 * sin(sli.Value() + 3 * PI / 2); }, function() { return -sqrt(2) + (9 - 2 * cos(sli.Value() + 3 * PI / 2)) / 6; }) jStyle;

j0t = point3d(view, 5, function() { return 2 * sin(sli.Value()); }, function() { return sqrt(2) + (9 - 2 * cos(sli.Value())) / 6; }) jStyle;
j1t = point3d(view, 5, function() { return 2 * sin(sli.Value() + PI / 2); }, function() { return sqrt(2) + (9 - 2 * cos(sli.Value() + PI / 2)) / 6; }) jStyle;
j2t = point3d(view, 5, function() { return 2 * sin(sli.Value() + PI); }, function() { return sqrt(2) + (9 - 2 * cos(sli.Value() + PI)) / 6; }) jStyle;
j3t = point3d(view, 5, function() { return 2 * sin(sli.Value() + 3 * PI / 2); }, function() { return sqrt(2) + (9 - 2 * cos(sli.Value() + 3 * PI / 2)) / 6; }) jStyle;

polygon3d(view, j0, j1, j2, j3);
polygon3d(view, j0t, j1t, j2t, j3t);
polygon3d(view, j0, j1, j1t, j0t);
polygon3d(view, j2, j3, j3t, j2t);

pjStyle = << color: 'gray', opacity: 0.5 >>;
line3d(view, p0, j0) pjStyle;
line3d(view, p1, j1) pjStyle;
line3d(view, p2, j2) pjStyle;
line3d(view, p3, j3) pjStyle;
line3d(view, p0t, j0t) pjStyle;
line3d(view, p1t, j1t) pjStyle;
line3d(view, p2t, j2t) pjStyle;
line3d(view, p3t, j3t) pjStyle;
```

## 知识点

- **三维视图**：使用 view3d 创建三维坐标系
- **三维点**：point3d 用于创建三维空间中的点
- **三维多边形**：polygon3d 用于创建三维空间中的多边形面
- **三维直线**：line3d 用于创建三维空间中的直线
- **平面**：plane3d 用于创建三维空间中的平面
- **透视投影**：central projection 模拟近大远小的视觉效果
- **参数方程**：使用三角函数参数方程描述圆形运动
- **线性变换**：展示三维物体到二维平面的投影变换

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| view3d | `view3d(pos, size, bounds)` | 创建三维视图 |
| point3d | `point3d(view, x, y, z)` | 创建三维点 |
| polygon3d | `polygon3d(view, p1, p2, ...)` | 创建三维多边形 |
| line3d | `line3d(view, p1, p2)` | 创建三维直线 |
| plane3d | `plane3d(view, point, normal, size)` | 创建三维平面 |
| slider | `slider(p1, p2, [min, max, step])` | 创建滑块控制器 |
| 三角函数 | `cos()`, `sin()`, `sqrt()`, `PI` | 数学函数和常量 |
| 动态函数 | `function(){return ...;}` | 创建动态计算的值 |

---
*来源：04-Cool Showcase/05-二元函数切平面.md（实际内容：立方体投影）*
