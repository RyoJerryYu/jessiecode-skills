# JessieCode Writer 技能参考索引

本文档提供了 `jessiecode-writer` 技能所使用的参考资源的完整索引。

---

## 语法规则

- [grammar.md](grammar.md) - 完整的 JessieCode 语法规则参考

### 语法快速查找

| 主题 | 章节 |
|------|------|
| 数据类型 | [第 1 章](grammar.md#1-数据类型-datatypes) |
| 运算符 | [第 2 章](grammar.md#2-运算符-operators) |
| 注释 | [第 3 章](grammar.md#3-注释-comments) |
| 控制结构 | [第 4 章](grammar.md#4-控制结构-control-structures) |
| 预定义常量 | [第 5 章](grammar.md#5-预定义常量-predefined-constants) |
| 预定义函数 | [第 6 章](grammar.md#6-预定义函数-predefined-functions) |
| 元素创建 | [第 7 章](grammar.md#7-元素创建-element-creation) |
| 访问元素 | [第 8 章](grammar.md#8-访问元素-accessing-elements) |
| 属性和方法 | [第 9 章](grammar.md#9-元素属性和方法) |
| 常见错误 | [第 12 章](grammar.md#12-常见错误) |

---

## API 文档

API 文档按 JSXGraph 元素名称字母顺序组织，共 **112 个** 元素文档。

### 基础元素

| 元素 | 文档 |
|------|------|
| Point | [Point.md](api/Point.md) |
| Line | [Line.md](api/Line.md) |
| Segment | [Segment.md](api/Segment.md) |
| Circle | [Circle.md](api/Circle.md) |
| Polygon | [Polygon.md](api/Polygon.md) |
| Text | [Text.md](api/Text.md) |
| Slider | [Slider.md](api/Slider.md) |
| Angle | [Angle.md](api/Angle.md) |

### 交点相关

| 元素 | 文档 |
|------|------|
| Intersection | [Intersection.md](api/Intersection.md) |
| Midpoint | [Midpoint.md](api/Midpoint.md) |
| Perpendicular | [Perpendicular.md](api/Perpendicular.md) |
| Parallel | [Parallel.md](api/Parallel.md) |
| Bisector | [Bisector.md](api/Bisector.md) |

### 圆相关

| 元素 | 文档 |
|------|------|
| Circle | [Circle.md](api/Circle.md) |
| Circumcircle | [Circumcircle.md](api/Circumcircle.md) |
| Arc | [Arc.md](api/Arc.md) |
| Sector | [Sector.md](api/Sector.md) |

### 3D 元素

| 元素 | 文档 |
|------|------|
| Point3D | [Point3D.md](api/Point3D.md) |
| Line3D | [Line3D.md](api/Line3D.md) |
| Circle3D | [Circle3D.md](api/Circle3D.md) |
| Plane3D | [Plane3D.md](api/Plane3D.md) |
| Sphere3D | [Sphere3D.md](api/Sphere3D.md) |
| Functiongraph3D | [Functiongraph3D.md](api/Functiongraph3D.md) |
| View3D | [View3D.md](api/View3D.md) |

### 完整列表

查看 [api/](api/) 目录获取全部 112 个元素文档。

---

## 示例代码

### 官方示例（24 个）

来自 JessieCode 官方仓库的示例。

| 编号 | 名称 | 文档 |
|------|------|------|
| 01 | 欧拉线 | [01-euler-line.md](examples/from-official/01-euler-line.md) |
| 02 | 创建者属性值 | [02-creators.md](examples/from-official/02-creators.md) |
| 03 | 映射函数 | [03-map-function.md](examples/from-official/03-map-function.md) |
| 04 | 美元符号语法 | [04-dollar-syntax.md](examples/from-official/04-dollar-syntax.md) |
| 05 | 函数示例 | [05-functions.md](examples/from-official/05-functions.md) |
| 06 | 综合示例 | [06-jessiecode.md](examples/from-official/06-jessiecode.md) |
| 07 | 条件表达式 | [07-merge-props.md](examples/from-official/07-merge-props.md) |
| 08 | 属性合并 | [08-conditions.md](examples/from-official/08-conditions.md) |
| 09 | 赋值操作 | [09-assign.md](examples/from-official/09-assign.md) |
| 10 | 编译器示例 | [10-compiler.md](examples/from-official/10-compiler.md) |
| 11 | UTF-8 字符 | [11-utf8.md](examples/from-official/11-utf8.md) |
| 12 | 生成项 | [12-genTerm.md](examples/from-official/12-genTerm.md) |
| 13 | 数字类型 | [13-numbers.md](examples/from-official/13-numbers.md) |
| 14 | Jison 解析器 | [14-jison.md](examples/from-official/14-jison.md) |
| 15 | 导入模块 | [15-import.md](examples/from-official/15-import.md) |
| 16 | 日志输出 | [16-log.md](examples/from-official/16-log.md) |
| 17 | 表达式滑块 | [17-exprslider.md](examples/from-official/17-exprslider.md) |
| 18 | Gaetano 几何 | [18-gaetano-g.md](examples/from-official/18-gaetano-g.md) |
| 19 | 条件类型 | [19-conditional.md](examples/from-official/19-conditional.md) |
| 20 | 作用域链 | [20-scopechain.md](examples/from-official/20-scopechain.md) |
| 21 | 基准测试 | [21-jcbench.md](examples/from-official/21-jcbench.md) |
| 22 | 空字符串 | [22-emptystring.md](examples/from-official/22-emptystring.md) |
| 23 | 过滤器 | [23-filters.md](examples/from-official/23-filters.md) |
| 24 | 多行注释 | [24-multiline.md](examples/from-official/24-multiline.md) |

### 用户示例（14 个）

来自用户的 JessieCode 示例。

#### 基础几何示例（02-Examples/）

| 编号 | 名称 | 文档 |
|------|------|------|
| 01 | 三角形外心 | [01-circumcenter.md](examples/from-user/01-circumcenter.md) |
| 02 | 三角形内心 | [02-incenter.md](examples/from-user/02-incenter.md) |
| 03 | 三角形重心 | [03-centroid.md](examples/from-user/03-centroid.md) |
| 04 | 三角形垂心 | [04-orthocenter.md](examples/from-user/04-orthocenter.md) |
| 05 | 二次函数与切线 | [05-quadratic-tangent.md](examples/from-user/05-quadratic-tangent.md) |
| 06 | 二次函数与积分 | [06-quadratic-integral.md](examples/from-user/06-quadratic-integral.md) |
| 07 | 完全四边形 | [07-complete-quadrilateral.md](examples/from-user/07-complete-quadrilateral.md) |
| 08 | 二元函数三维图像 | [08-bivariate-function-3d.md](examples/from-user/08-bivariate-function-3d.md) |

#### 进阶展示（04-Cool Showcase/）

| 编号 | 名称 | 文档 |
|------|------|------|
| 09 | 割圆八线 | [09-trig-eight-lines.md](examples/from-user/09-trig-eight-lines.md) |
| 10 | 欧拉线 | [10-euler-line.md](examples/from-user/10-euler-line.md) |
| 11 | 角平分线性质 | [11-angle-bisector-perpendicular-circumcircle.md](examples/from-user/11-angle-bisector-perpendicular-circumcircle.md) |
| 12 | 立方体投影 | [12-cube-projection.md](examples/from-user/12-cube-projection.md) |
| 13 | 二元函数切平面 | [13-bivariate-tangent-plane.md](examples/from-user/13-bivariate-tangent-plane.md) |
| 14 | dy 与 delta y 的区别 | [14-dy-vs-delta-y.md](examples/from-user/14-dy-vs-delta-y.md) |

---

## 使用建议

### 快速开始

1. 阅读 [instructions.md](../instructions.md) 了解技能使用方法
2. 查阅 [grammar.md](grammar.md) 学习 JessieCode 语法
3. 参考 [examples/](examples/) 中的示例代码
4. 根据需要查阅 [api/](api/) 中的元素文档

### 按主题查找示例

| 主题 | 示例 |
|------|------|
| 三角形四心 | 外心、内心、重心、垂心（用户示例 01-04） |
| 欧拉线 | 官方示例 01、用户示例 10 |
| 函数图像 | 官方示例 03、05、17 |
| 3D 图形 | 用户示例 08、12、13 |
| 微积分 | 用户示例 06、13、14 |
| 属性语法 | 官方示例 02、07、08、19 |

---

## 版本信息

- 版本：v1.0
- 语法文档版本：基于 JessieCode 1.0+
- API 文档数量：112 个元素
- 示例代码数量：38 个（官方 24 + 用户 14）
