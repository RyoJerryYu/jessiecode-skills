# 二元函数三维图像 (3D Graph of Bivariate Function)

## 图形描述

展示二元函数 f(x,y) = sin(x) + sin(y) 的三维曲面图像。使用三维坐标系和透视投影来呈现函数的空间形态。

## JessieCode 代码

```js
bound = [-10, 10];
view = view3d([-7, -7], [14, 14], [bound, bound, bound]) <<
    xPlaneRear: << visible: false >>,
    yPlaneRear: << visible: false >>,
    projection: 'central'
>>;

F = function(x, y) { return sin(x) + sin(y); };
functiongraph3d(view, F, bound, bound) << strokeWidth: 0.5, stepsU: 70, stepsV: 70 >>;
```

## 知识点

- **二元函数**：z = f(x,y)，两个自变量一个因变量
- **三维曲面**：二元函数的图像是空间中的曲面
- **透视投影**：使用中心投影（central projection）模拟人眼观察效果
- **网格密度**：stepsU 和 stepsV 控制曲面网格的精细程度
- **三角函数叠加**：sin(x) + sin(y) 形成波浪状曲面

## 涉及元素

| 元素 | JessieCode API | 说明 |
|------|----------------|------|
| view3d | `view3d(pos, size, bounds)` | 创建三维视图 |
| function | `function(x,y){...}` | 定义二元函数 |
| functiongraph3d | `functiongraph3d(view, f, boundX, boundY)` | 创建三维函数图像 |
| 样式属性 | `<<visible: false>>` | 隐藏坐标平面 |
| 样式属性 | `<<projection: "central">>` | 设置透视投影 |
| 样式属性 | `<<strokeWidth:0.5,stepsU:70,stepsV:70>>` | 设置线宽和网格密度 |

---
*来源：02-Examples/31-二元函数三维图像.md*
