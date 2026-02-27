# API 文档分类清单

本文档将 114 个 API 元素按使用频率分为三类：**core**（核心）、**common**（常用）、**advanced**（高级）。

> 分类标准：
> - **core**: 最基础的 20 个元素，90% 的构造都会使用
> - **common**: 常用的 30 个元素，用于常见几何构造
> - **advanced**: 高级/ specialized 的 64 个元素，用于特殊场景

---

## Core - 核心元素 (20 个)

这些是最基础、最常用的元素：

| 元素名 | 文件 | 描述 |
|--------|------|------|
| Point | Point.md | 点 |
| Line | Line.md | 直线 |
| Segment | Segment.md | 线段 |
| Circle | Circle.md | 圆 |
| Polygon | Polygon.md | 多边形 |
| Text | Text.md | 文本标签 |
| Slider | Slider.md | 滑块 |
| Angle | Angle.md | 角度 |
| Midpoint | Midpoint.md | 中点 |
| Intersection | Intersection.md | 交点 |
| Perpendicular | Perpendicular.md | 垂线 |
| Parallel | Parallel.md | 平行线 |
| Arc | Arc.md | 圆弧 |
| Sector | Sector.md | 扇形 |
| Functiongraph | Functiongraph.md | 函数图像 |
| Glider | Glider.md | 滑点 |
| Transform | Transformation.md | 变换 |
| Locus | Tracecurve.md | 轨迹 |
| Button | Button.md | 按钮 |
| Checkbox | Checkbox.md | 复选框 |

---

## Common - 常用元素 (30 个)

这些是常见的几何构造元素：

| 元素名 | 文件 | 描述 |
|--------|------|------|
| PerpendicularPoint | PerpendicularPoint.md | 垂足 |
| PerpendicularSegment | PerpendicularSegment.md | 垂线段 |
| Projection | Orthogonalprojection.md | 投影 |
| Circumcircle | Circumcircle.md | 外接圆 |
| Circumcenter | Circumcenter.md | 外心 |
| Incircle | Incircle.md | 内切圆 |
| Incenter | Incenter.md | 内心 |
| Semicircle | Semicircle.md | 半圆 |
| MajorArc | MajorArc.md | 优弧 |
| MinorArc | MinorArc.md | 劣弧 |
| MajorSector | MajorSector.md | 优扇形 |
| MinorSector | MinorSector.md | 劣扇形 |
| Ticks | Ticks.md | 刻度 |
| Stepfunction | Stepfunction.md | 阶跃函数 |
| Tangent | Tangent.md | 切线 |
| Bisector | Bisector.md | 角平分线 |
| Median | - | 中线（使用 Segment+Midpoint） |
| Centroid | - | 重心（使用 Intersection） |
| Orthocenter | - | 垂心（使用 Intersection） |
| Vector | - | 向量（使用 Arrow） |
| Curve | Curve.md | 曲线 |
| Image | Image.md | 图片 |
| Arrow | Arrow.md | 箭头 |
| HalfLine | - | 射线 |
| Locus | Tracecurve.md | 轨迹 |
| Angle | Angle.md | 角度 |
| ReflexAngle | ReflexAngle.md | 优角 |
| NonReflexAngle | NonReflexAngle.md | 劣角 |
| Slopetriangle | Slopetriangle.md | 斜率三角形 |
| Integral | Integral.md | 积分 |

---

## Advanced - 高级元素 (64 个)

这些是 specialized 或 3D 相关的元素：

### 3D 元素 (17 个)

| 元素名 | 文件 | 描述 |
|--------|------|------|
| Point3D | Point3D.md | 3D 点 |
| Line3D | Line3D.md | 3D 直线 |
| Circle3D | Circle3D.md | 3D 圆 |
| Curve3D | Curve3D.md | 3D 曲线 |
| Face3D | Face3D.md | 3D 面 |
| Axis3D | Axis3D.md | 3D 轴 |
| Axes3D | Axes3D.md | 3D 坐标系 |
| Text3D | Text3D.md | 3D 文本 |
| Sphere3D | Sphere3D.md | 3D 球体 |
| Plane3D | Plane3D.md | 3D 平面 |
| Polygon3D | Polygon3D.md | 3D 多边形 |
| Polyhedron3D | Polyhedron3D.md | 3D 多面体 |
| IntersectionCircle3D | IntersectionCircle3D.md | 3D 圆交点 |
| IntersectionLine3D | IntersectionLine3D.md | 3D 线交点 |
| Transformation3D | Transformation3D.md | 3D 变换 |
| View3D | View3D.md | 3D 视图 |
| Ticks3D | Ticks3D.md | 3D 刻度 |
| ParametricSurface3D | ParametricSurface3D.md | 3D 参数曲面 |
| Vectorfield3D | Vectorfield3D.md | 3D 向量场 |

### 圆锥曲线 (5 个)

| 元素名 | 文件 | 描述 |
|--------|------|------|
| Ellipse | Ellipse.md | 椭圆 |
| Hyperbola | Hyperbola.md | 双曲线 |
| Parabola | Parabola.md | 抛物线 |
| Conic | Conic.md | 圆锥曲线 |
| Arc (变体) | CircumcircleArc.md | 圆弧变体 |

### 特殊曲线 (12 个)

| 元素名 | 文件 | 描述 |
|--------|------|------|
| Cardinalspline | Cardinalspline.md | 基数样条 |
| Spline | Spline.md | 样条曲线 |
| Metapostspline | Metapostspline.md | MetaPost 样条 |
| Functiongraph3D | Functiongraph3D.md | 3D 函数图 |
| Derivative | Derivative.md | 导数 |
| Riemannsum | Riemannsum.md | 黎曼和 |
| Comb | Comb.md | 梳状图 |
| Tracecurve | Tracecurve.md | 轨迹曲线 |
| Slopefield | Slopefield.md | 斜率场 |
| Vectorfield | Vectorfield.md | 向量场 |
| ImplicitCurve | ImplicitCurve.md | 隐式曲线 |
| PolarLine | PolarLine.md | 极线 |

### 统计图表 (4 个)

| 元素名 | 文件 | 描述 |
|--------|------|------|
| Chart | Chart.md | 图表 |
| Boxplot | Boxplot.md | 箱线图 |
| Measurement | Measurement.md | 测量 |
| Legend | Legend.md | 图例 |

### 交互元素 (8 个)

| 元素名 | 文件 | 描述 |
|--------|------|------|
| Input | Input.md | 输入框 |
| Button | Button.md | 按钮 |
| Checkbox | Checkbox.md | 复选框 |
| Group | Group.md | 组 |
| ForeignObject | ForeignObject.md | 外部对象 |
| Turtle | Turtle.md | 海龟绘图 |
| Tapemeasure | Tapemeasure.md | 测量工具 |
| Inequality | Inequality.md | 不等式 |

### 其他高级元素 (18 个)

| 元素名 | 文件 | 描述 |
|--------|------|------|
| Arrowparallel | Arrowparallel.md | 平行箭头 |
| Bisectorlines | Bisectorlines.md | 角平分线（直线） |
| CircumcircleSector | CircumcircleSector.md | 外接圆扇形 |
| CurveDifference | CurveDifference.md | 曲线差集 |
| CurveIntersection | CurveIntersection.md | 曲线交集 |
| CurveUnion | CurveUnion.md | 曲线并集 |
| Grid | Grid.md | 网格 |
| Hatch | Hatch.md | 填充线 |
| Label | Label.md | 标签 |
| MirrorElement | MirrorElement.md | 镜像元素 |
| MirrorPoint | MirrorPoint.md | 镜像点 |
| Normal | Normal.md | 法线 |
| OtherIntersection | OtherIntersection.md | 其他交点 |
| Parallelogram | Parallelogram.md | 平行四边形 |
| Parallelpoint | Parallelpoint.md | 平行点 |
| PolePoint | PolePoint.md | 极点 |
| RadicalAxis | RadicalAxis.md | 根轴 |
| Reflection | Reflection.md | 反射 |
| RegularPolygon | RegularPolygon.md | 正多边形 |
| Smartlabel | Smartlabel.md | 智能标签 |
| TangentTo | TangentTo.md | 切线到 |

---

## 使用频率标签

每个 API 文档顶部应添加以下标签之一：

```markdown
<!-- USAGE_FREQUENCY: core -->
<!-- USAGE_FREQUENCY: common -->
<!-- USAGE_FREQUENCY: advanced -->
```

---

## 分类统计

| 分类 | 数量 | 占比 |
|------|------|------|
| core | 20 | 17.5% |
| common | 30 | 26.3% |
| advanced | 64 | 56.2% |
| **总计** | **114** | **100%** |

---

## 文档优化建议

1. **core 文档**：保持详细，包含多个实用示例
2. **common 文档**：保留核心语法 +1-2 个示例
3. **advanced 文档**：精简为关键语法+1 个示例，复杂属性指向 grammar.md

---

*生成日期：2026-02-27*
*基于改进计划 T1.4 任务*
