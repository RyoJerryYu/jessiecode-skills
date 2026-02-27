# JessieCode Writer Skill 改进实施方案

> **文档目的**：本方案基于 [分析报告](./jessiecode-writer-analysis.md) 中识别的 11 个问题，提供具体可执行的改进计划。
>
> **方案版本**：v1.0
>
> **制定日期**：2026-02-27

---

## 一、改进目标与范围

### 1.1 总体目标

基于 [分析报告](./jessiecode-writer-analysis.md) 的结论，通过系统性改进实现：

1. **修复文档一致性问题** - 消除参数说明不一致导致的代码错误
2. **优化 Token 效率** - 减少 50-70% 的 API 文档 token 消耗
3. **提升用户体验** - 降低新手学习门槛，提高示例检索效率
4. **提高代码质量** - 标准化示例代码，添加验证机制

### 1.2 改进范围

| 类别 | 改进项数 | 涉及文件 |
|------|---------|---------|
| 文档一致性修复 | 2 项 | `grammar.md`, `Intersection.md`, 用户示例 |
| API 文档优化 | 3 项 | `api/` 目录（112 个文件） |
| 新增文档 | 3 项 | `QUICKSTART.md`, `examples-index.md`, `VERSION.md` |
| 配置改进 | 2 项 | `SKILL.md`, `instructions.md` |
| 示例标准化 | 1 项 | `examples/` 目录（38 个文件） |

---

## 二、任务分解与依赖关系

### 2.1 任务总览

```
改进项目 (共 12 个子任务)
├── 阶段一：P0 核心修复 (4 个任务)
│   ├── T1.1: 修复 perpendicular 参数说明
│   ├── T1.2: 完善 intersection index 参数说明
│   ├── T1.3: 创建 QUICKSTART.md
│   └── T1.4: API 文档元素分类
├── 阶段二：P1 质量提升 (5 个任务)
│   ├── T2.1: 创建示例主题索引
│   ├── T2.2: 标准化示例代码风格
│   ├── T2.3: 添加版本兼容性说明
│   ├── T2.4: 精简高级元素 API 文档
│   └── T2.5: 为 API 文档添加频率标签
└── 阶段三：P2 长期优化 (3 个任务)
    ├── T3.1: 合并重复的 API 文档内容
    ├── T3.2: 添加测试用例框架
    └── T3.3: 增强 SKILL.md 配置
```

### 2.2 任务详情表

| 任务 ID | 任务名称 | 优先级 | 预估工时 | 依赖任务 | 是否可并行 |
|--------|---------|--------|---------|---------|-----------|
| T1.1 | 修复 perpendicular 参数说明 | P0 | 1h | 无 | ✅ 可并行 |
| T1.2 | 完善 intersection index 参数说明 | P0 | 1h | 无 | ✅ 可并行 |
| T1.3 | 创建 QUICKSTART.md | P0 | 2h | 无 | ✅ 可并行 |
| T1.4 | API 文档元素分类 | P0 | 3h | 无 | ✅ 可并行 |
| T2.1 | 创建示例主题索引 | P1 | 2h | T1.4 | ❌ 依赖 T1.4 |
| T2.2 | 标准化示例代码风格 | P1 | 4h | T1.1, T1.2 | ❌ 依赖 T1.1, T1.2 |
| T2.3 | 添加版本兼容性说明 | P1 | 1h | 无 | ✅ 可并行 |
| T2.4 | 精简高级元素 API 文档 | P1 | 8h | T1.4 | ❌ 依赖 T1.4 |
| T2.5 | 为 API 文档添加频率标签 | P1 | 2h | T1.4 | ❌ 依赖 T1.4 |
| T3.1 | 合并重复的 API 文档内容 | P2 | 6h | T2.4 | ❌ 依赖 T2.4 |
| T3.2 | 添加测试用例框架 | P2 | 4h | T2.2 | ❌ 依赖 T2.2 |
| T3.3 | 增强 SKILL.md 配置 | P2 | 2h | 无 | ✅ 可并行 |

### 2.3 并行执行建议

**阶段一（P0）可完全并行**：
- T1.1、T1.2、T1.3、T1.4 四个任务互不依赖，可由 4 人并行执行，总工期从 7h 缩短至 3h

**阶段二（P1）部分并行**：
- 第一波：T2.3（独立）、T2.1（依赖 T1.4 完成后）
- 第二波：T2.2、T2.4、T2.5（需 T1.4 完成）
- 建议人力分配：2 人执行 T2.4（工作量最大），1 人执行 T2.2，1 人执行 T2.1+T2.3+T2.5

**阶段三（P2）部分并行**：
- T3.3（独立）可随时执行
- T3.1 需 T2.4 完成后执行
- T3.2 需 T2.2 完成后执行

---

## 三、TODO List

### 阶段一：P0 核心修复（立即实施）

#### T1.1: 修复 perpendicular 函数参数说明

**目标**：统一 `perpendicular(line, point)` 的参数说明

**检查清单**：
- [ ] 检查 `grammar.md` 第 375 行的参数说明
- [ ] 检查 `instructions.md` 中所有 perpendicular 相关示例
- [ ] 检查用户示例 `01-circumcenter.md` 第 20 行
- [ ] 统一所有文档中的参数说明格式
- [ ] 验证示例代码的语义正确性

**验收标准**：
- [ ] 所有文档中 `perpendicular` 的参数顺序一致
- [ ] 示例代码能正确表达"过点作直线的垂线"的语义

---

#### T1.2: 完善 intersection index 参数说明

**目标**：补充 `intersection(line1, line2, index)` 的 `index` 参数说明

**检查清单**：
- [ ] 在 `grammar.md` 中补充 index 参数说明
- [ ] 在 `Intersection.md` 中明确两直线相交时的默认行为
- [ ] 说明何时需要指定 0 或 1
- [ ] 更新示例代码，展示不同场景的用法

**验收标准**：
- [ ] index 参数的默认值有明确说明
- [ ] 两直线/圆与直线/两圆三种场景的索引使用有清晰示例

---

#### T1.3: 创建 QUICKSTART.md 快速入门文档

**目标**：创建 5 分钟快速入门指南

**文档结构**：
```markdown
# 快速入门

## 1. Hello World（最简单的三角形）
## 2. 核心语法（3 个基本元素）
## 3. 常见问题 FAQ
## 4. 下一步学习路径
```

**检查清单**：
- [ ] 包含最简单的可运行示例
- [ ] 包含 3-5 个最常见问题的解答
- [ ] 提供清晰的学习路径指引

**验收标准**：
- [ ] 新手可在 5 分钟内完成第一个图形
- [ ] FAQ 覆盖了分析报告中的常见错误

---

#### T1.4: API 文档元素分类

**目标**：将 112 个 API 文档按使用频率分类

**分类标准**：

| 分类 | 数量 | 元素列表 |
|------|------|---------|
| **core** | 20 | Point, Line, Segment, Circle, Polygon, Text, Slider, Intersection, Midpoint, Perpendicular, Parallel, Angle, Arc, Sector, Functiongraph, Transform, Glider, Locus, Button, Checkbox |
| **common** | 30 | PerpendicularPoint, Projection, Circumcircle, Incircle, Semicircle, MajorArc, MinorArc, MajorSector, MinorSector, Ticks, StepFunction, FunctionPlot, Curve, Tangent, Normal, Bisector, Median, Altitude, Centroid, Orthocenter, Incenter, NinePointCircle, EulerLine, Vector, Complex, Matrix, PlotPanel, Animation, Image, Checkbox |
| **advanced** | 62 | 其余 3D 元素、特殊曲线、统计图表等 |

**检查清单**：
- [ ] 遍历 `api/` 目录，列出所有 112 个文件名
- [ ] 按照上述分类标准，为每个文件分配频率标签
- [ ] 生成分类清单文档 `api/CATEGORY_LIST.md`

**验收标准**：
- [ ] 112 个文件全部有明确的分类标签
- [ ] 分类清单可供后续任务引用

---

### 阶段二：P1 质量提升（1-2 周内）

#### T2.1: 创建示例主题索引

**目标**：创建示例代码的主题索引，提高检索效率

**索引结构**：
```markdown
# 示例代码索引

## 按主题分类
### 三角形相关
- 外心/内心/重心/垂心
- 中垂线/角平分线/中线/高

### 圆相关
- 基本圆/同心圆/相切圆
- 圆弧/扇形

## 按难度分类
### 入门（5 个）
### 进阶（20 个）
### 高级（13 个）
```

**检查清单**：
- [ ] 遍历 `examples/` 目录的 38 个示例
- [ ] 为每个示例添加主题标签
- [ ] 为每个示例添加难度标签
- [ ] 创建 `examples-index.md` 索引文件

**验收标准**：
- [ ] 每个示例都有主题和难度标签
- [ ] 索引文件支持按主题/难度快速检索

---

#### T2.2: 标准化示例代码风格

**目标**：统一所有示例代码的格式

**代码风格规范**：
```js
// 1. 赋值运算符两侧加空格
A = point(1, 2);

// 2. 函数调用括号内不加空格
point(1, 2)

// 3. 属性块 << >> 内格式统一
A = point(1, 2) <<
    strokeColor: 'red',
    fillColor: 'pink',
    size: 5
>>;

// 4. 注释前保留两个空格
A = point(1, 2);  // 创建点 A
```

**检查清单**：
- [ ] 遍历 38 个示例文件
- [ ] 按照风格规范格式化代码
- [ ] 修复已知的 `**` vs `^` 问题
- [ ] 验证 `.toFixed()` 等 JS 互操作的可用性

**验收标准**：
- [ ] 所有示例代码风格一致
- [ ] 无语法错误或未说明的 JS 互操作

---

#### T2.3: 添加版本兼容性说明

**目标**：创建版本兼容性文档

**文档内容**：
```markdown
# 版本兼容性

## JessieCode 版本
当前文档基于 JessieCode v1.x

## JSXGraph 兼容性
兼容 JSXGraph v1.6.0+

## 已知版本差异
- ** 幂运算符：v1.5+ 支持
- .toFixed()：JavaScript 互操作，所有版本支持
```

**检查清单**：
- [ ] 调研 JessieCode 当前版本
- [ ] 确认 JSXGraph 最低兼容版本
- [ ] 记录已知的版本差异问题
- [ ] 创建 `VERSION.md` 或更新 `README.md`

**验收标准**：
- [ ] 版本号有明确来源
- [ ] 版本差异问题有清晰说明

---

#### T2.4: 精简高级元素 API 文档

**目标**：将 62 个高级元素文档精简为关键语法 +1 个示例

**精简策略**：

| 保留内容 | 删除内容 |
|---------|---------|
| 基本语法 | 冗余示例（保留 1 个） |
| 参数说明 | 详细属性列表（指向 grammar.md） |
| 1 个核心示例 | 复杂场景示例 |

**精简模板**：
```markdown
# ElementName 元素名称

<!-- USAGE_FREQUENCY: advanced -->

## 基本语法

```js
element = api(param1, param2);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| param1 | Type | 说明 |

## 示例

```js
// 核心示例
element = api(1, 2);
```

## 更多信息

完整属性和方法请参考 [grammar.md](../grammar.md)。
```

**检查清单**：
- [ ] 根据 T1.4 的分类，筛选出 62 个 advanced 文档
- [ ] 按照精简模板逐个修改
- [ ] 记录精简前后的行数/token 数对比

**验收标准**：
- [ ] 62 个文档全部精简完成
- [ ] 精简后文档仍包含核心语法和 1 个示例
- [ ] token 消耗减少 50% 以上

---

#### T2.5: 为 API 文档添加频率标签

**目标**：在每个 API 文档顶部添加使用频率标签

**标签格式**：
```markdown
<!-- USAGE_FREQUENCY: core -->
<!-- USAGE_FREQUENCY: common -->
<!-- USAGE_FREQUENCY: advanced -->
```

**检查清单**：
- [ ] 根据 T1.4 的分类结果
- [ ] 为 112 个 API 文档添加对应标签
- [ ] 验证标签位置（文件顶部，标题之前）

**验收标准**：
- [ ] 112 个文档全部添加频率标签
- [ ] 标签位置统一、格式正确

---

### 阶段三：P2 长期优化（1 个月内）

#### T3.1: 合并重复的 API 文档内容

**目标**：将功能相似的元素合并到同一文档

**合并分组建议**：

| 分组 | 原文件 | 合并后 |
|------|--------|--------|
| 圆弧组 | Arc.md, MajorArc.md, MinorArc.md | Arc.md（包含所有变体） |
| 扇形组 | Sector.md, MajorSector.md, MinorSector.md | Sector.md |
| 三角形中心组 | Circumcircle.md, Incircle.md, Centroid.md, Orthocenter.md | TriangleCenters.md |

**检查清单**：
- [ ] 识别所有可合并的文档组
- [ ] 创建合并后的文档
- [ ] 更新相关引用链接
- [ ] 删除原文件（或保留为重定向）

**验收标准**：
- [ ] 合并后文档数量减少 30% 以上
- [ ] 所有内部引用链接有效

---

#### T3.2: 添加测试用例框架

**目标**：为技能生成能力添加验证机制

**测试框架内容**：
```markdown
# 测试用例框架

## 语法正确性测试
- [ ] 所有元素创建语法正确
- [ ] 所有属性名称拼写正确
- [ ] 所有函数调用格式正确

## 几何构造覆盖测试
- [ ] 三角形构造（外心/内心/重心/垂心）
- [ ] 圆构造（同心圆/相切圆/外接圆/内切圆）
- [ ] 函数图构造（一次函数/二次函数/三角函数）

## 边界情况测试
- [ ] 空输入处理
- [ ] 极端值处理
- [ ] 错误输入处理
```

**检查清单**：
- [ ] 设计测试用例模板
- [ ] 编写核心功能的测试用例
- [ ] 记录测试结果和修复情况

**验收标准**：
- [ ] 有明确的测试用例清单
- [ ] 核心功能测试覆盖率 > 80%

---

#### T3.3: 增强 SKILL.md 配置

**目标**：完善 SKILL.md 中的技能描述和边界说明

**建议更新内容**：
```yaml
description: >-
  Generate JessieCode code for creating interactive geometric constructions
  and mathematical function graphs using JSXGraph. Use when users need to:
  (1) create geometric figures (triangles, circles, polygons),
  (2) plot 2D/3D function graphs,
  (3) demonstrate mathematical concepts visually,
  (4) generate dynamic constructions with sliders or animations.

boundaries:
  - Do not generate complex 3D animation code
  - Do not handle graphics requiring external resources
  - For ambiguous requirements, ask clarifying questions

output_format:
  - Use ```jessiecode code blocks
  - Add brief explanation before code
  - Add key points explanation after code
```

**检查清单**：
- [ ] 补充技能边界说明
- [ ] 补充输出格式规范
- [ ] 补充模糊需求处理方式

**验收标准**：
- [ ] SKILL.md 包含完整的触发条件、边界说明、输出格式

---

## 四、质量评估标准

### 4.1 单项任务质量评估

每个任务完成后，使用以下检查表进行自评估：

| 评估维度 | 评分标准 | 得分 (1-5) |
|---------|---------|-----------|
| **完整性** | 任务检查清单 100% 完成 | /5 |
| **准确性** | 修改内容无错误、无遗漏 | /5 |
| **一致性** | 与现有文档风格保持一致 | /5 |
| **可维护性** | 修改后易于后续维护更新 | /5 |

**通过标准**：单项任务平均得分 ≥ 4 分

---

### 4.2 阶段质量评估

#### 阶段一（P0）完成评估

| 评估项 | 检查方法 | 通过标准 |
|-------|---------|---------|
| 文档一致性 | 抽样检查 10 处 perpendicular/intersection 用法 | 无不一致 |
| 快速入门 | 实际执行 QUICKSTART.md 的流程 | 5 分钟内完成 |
| 元素分类 | 检查 CATEGORY_LIST.md 是否覆盖 112 个文件 | 100% 覆盖 |

#### 阶段二（P1）完成评估

| 评估项 | 检查方法 | 通过标准 |
|-------|---------|---------|
| 示例索引 | 随机查找 3 个主题的示例 | 能快速定位 |
| 代码风格 | 抽样检查 10 个示例文件 | 风格统一 |
| API 精简 | 对比精简前后的 token 数 | 减少 ≥ 50% |
| 频率标签 | 检查 112 个文件的标签 | 100% 添加 |

#### 阶段三（P2）完成评估

| 评估项 | 检查方法 | 通过标准 |
|-------|---------|---------|
| 文档合并 | 统计合并后的文件数量 | 减少 ≥ 30% |
| 测试覆盖 | 检查测试用例覆盖的核心功能 | ≥ 80% |
| SKILL.md | 检查配置完整性 | 包含边界和格式说明 |

---

### 4.3 最终整体验收

改进项目完成后，进行整体验证：

| 验证项 | 验证方法 | 目标值 |
|-------|---------|--------|
| **Token 优化** | 对比改进前后的总 token 数 | 减少 50-70% |
| **文档一致性** | 全面扫描所有文档的关键函数用法 | 零不一致 |
| **示例质量** | 随机抽取 5 个示例进行代码审查 | 无语法错误 |
| **用户体验** | 邀请新手试用 QUICKSTART.md | 5 分钟内上手 |
| **检索效率** | 通过索引查找特定主题示例 | < 30 秒定位 |

---

## 五、执行建议

### 5.1 人力配置建议

| 阶段 | 建议人数 | 角色分工 |
|------|---------|---------|
| P0 | 2-4 人 | 1 人负责文档修复，1 人负责元素分类，可选 2 人加速 |
| P1 | 2-3 人 | 1 人负责示例相关，1 人负责 API 精简，1 人负责其他 |
| P2 | 1-2 人 | 1 人负责合并和测试，1 人负责 SKILL.md |

### 5.2 进度跟踪建议

- **每日站会**：同步任务进展和阻塞问题
- **周报**：汇总本周完成的任务和 token 优化效果
- **阶段复盘**：每个阶段完成后进行质量评估和流程优化

### 5.3 风险控制

| 风险 | 影响 | 应对措施 |
|------|------|---------|
| API 精简过度导致信息缺失 | 高 | 保留完整版本备份，建立反馈渠道 |
| 文档合并后链接失效 | 中 | 使用脚本批量更新引用链接 |
| 示例修改引入新错误 | 中 | 修改后执行语法验证 |

---

## 六、附录

### 附录 A：相关文件路径

| 文件 | 路径 |
|------|------|
| 分析报告 | `aichat/output/05-report/jessiecode-writer-analysis.md` |
| Skill 目录 | `.claude/skills/jessiecode-writer/` |
| 语法文档 | `.claude/skills/jessiecode-writer/references/grammar.md` |
| API 目录 | `.claude/skills/jessiecode-writer/references/api/` |
| 示例目录 | `.claude/skills/jessiecode-writer/references/examples/` |

### 附录 B：112 个 API 元素清单

（待 T1.4 任务完成后补充完整清单）

### 附录 C：变更日志

| 日期 | 版本 | 变更内容 |
|------|------|---------|
| 2026-02-27 | v1.0 | 初始版本 |

---

**文档制定者**：skill-creator 分析
**审核状态**：待审核
**执行状态**：待执行
