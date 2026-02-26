# 示例代码产出清单

## @JessieCode-examples/ 目录下的示例代码 (共 24 个)

### 几何图形示例

- [x] 01-euler-line.md - 欧拉线（垂心、重心、外心共线）
- [x] 06-jessiecode.md - JessieCode 综合示例（属性对象、动态点、外接圆等）
- [x] 18-gaetano-g.md - Gaetano 的几何示例（坐标系统、点约束）
- [x] 21-jcbench.md - 基准测试示例

### 函数与映射示例

- [x] 03-map-function.md - 映射函数（map 语法、微分、求值）
- [x] 05-functions.md - 函数示例（综合函数定义与使用）
- [x] 12-genTerm.md - 生成项（generateTerm 方法）
- [x] 17-exprslider.md - 表达式滑块（函数图像与滑块联动）

### 属性与样式示例

- [x] 02-creators.md - 创建者属性值（属性对象组合使用）
- [x] 08-conditions.md - 属性合并示例
- [x] 23-filters.md - 过滤器/字符串处理示例

### 变量与赋值示例

- [x] 09-assign.md - 赋值操作（连续赋值）
- [x] 11-utf8.md - UTF-8 字符（希腊字母等）
- [x] 13-numbers.md - 数字类型（NaN、Infinity 等）
- [x] 22-emptystring.md - 空字符串处理

### 条件与逻辑示例

- [x] 07-merge-props.md - 条件表达式示例
- [x] 19-conditional.md - 条件类型示例
- [x] 10-compiler.md - 编译器示例（条件返回）

### 作用域与函数示例

- [x] 20-scopechain.md - 作用域链
- [x] 24-multiline.md - 多行注释示例
- [x] 16-log.md - 日志输出（$log 函数）

### 导入与模块示例

- [x] 15-import.md - 导入模块（import 语句）

### 语法示例

- [x] 04-dollar-syntax.md - 美元符号语法（通过 ID 引用元素）
- [x] 14-jison.md - Jison 解析器示例（幂运算）

---

## @my-jessiecode-examples/ 目录下的示例代码 (共 14 个)

### 02-Examples/ 目录 (8 个)

- [x] 01-circumcenter.md - 三角形外心
- [x] 02-incenter.md - 三角形内心
- [x] 03-centroid.md - 三角形重心
- [x] 04-orthocenter.md - 三角形垂心
- [x] 05-quadratic-tangent.md - 二次函数与切线
- [x] 06-quadratic-integral.md - 二次函数与积分
- [x] 07-complete-quadrilateral.md - 完全四边形
- [x] 08-bivariate-function-3d.md - 二元函数三维图像

### 04-Cool Showcase/ 目录 (6 个)

- [x] 09-trig-eight-lines.md - 割圆八线
- [x] 10-euler-line.md - 欧拉线
- [x] 11-angle-bisector-perpendicular-circumcircle.md - 角平分线与中垂线交点位于外接圆上
- [x] 12-cube-projection.md - 立方体投影
- [x] 13-bivariate-tangent-plane.md - 二元函数切平面
- [x] 14-dy-vs-delta-y.md - 微分中 dy 与 delta y 的区别

---

## 产出统计

| 类别 | 总数 | 已完成 | 进行中 | 待完成 |
|------|------|--------|--------|--------|
| 官方示例 | 24 | 24 | 0 | 0 |
| 用户示例 | 14 | 14 | 0 | 0 |
| **总计** | **38** | **38** | **0** | **0 |

---

## 输出目录结构

```
aichat/output/04-examples/
├── README.md                  # 本文件（示例代码产出清单）
├── from-official/             # 官方示例翻译 (24 个)
│   ├── 01-euler-line.md
│   ├── 02-creators.md
│   ├── 03-map-function.md
│   ├── 04-dollar-syntax.md
│   ├── 05-functions.md
│   ├── 06-jessiecode.md
│   ├── 07-merge-props.md
│   ├── 08-conditions.md
│   ├── 09-assign.md
│   ├── 10-compiler.md
│   ├── 11-utf8.md
│   ├── 12-genTerm.md
│   ├── 13-numbers.md
│   ├── 14-jison.md
│   ├── 15-import.md
│   ├── 16-log.md
│   ├── 17-exprslider.md
│   ├── 18-gaetano-g.md
│   ├── 19-conditional.md
│   ├── 20-scopechain.md
│   ├── 21-jcbench.md
│   ├── 22-emptystring.md
│   ├── 23-filters.md
│   └── 24-multiline.md
└── from-user/                 # 用户示例翻译 (14 个)
    ├── 01-circumcenter.md
    ├── 02-incenter.md
    ├── 03-centroid.md
    ├── 04-orthocenter.md
    ├── 05-quadratic-tangent.md
    ├── 06-quadratic-integral.md
    ├── 07-complete-quadrilateral.md
    ├── 08-bivariate-function-3d.md
    ├── 09-trig-eight-lines.md
    ├── 10-euler-line.md
    ├── 11-angle-bisector-perpendicular-circumcircle.md
    ├── 12-cube-projection.md
    ├── 13-bivariate-tangent-plane.md
    └── 14-dy-vs-delta-y.md
```

---

## 每份文档格式

每份示例代码文档包含以下结构：

```markdown
# 标题 (Title)

## 图形描述

[代码所代表的图形意义描述]

## JessieCode 代码

```js
[完整的 JessieCode 代码]
```

## 知识点

- [知识点 1]
- [知识点 2]
- ...

## 涉及元素

| 元素 | 描述 | API 文档 |
|------|------|----------|
| Point | 点 | [Point](../../03-api/Point.md) |
| ... | ... | ... |
```
