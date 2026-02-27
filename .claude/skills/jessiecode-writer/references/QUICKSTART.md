# JessieCode 快速入门指南

> 5 分钟上手 JessieCode，创建你的第一个几何图形！

---

## 1. Hello World - 最简单的三角形

```jessiecode
---
boundingBox: [-5, 5, 5, -5]
grid: true
---
// 定义三个顶点
A = point(-2, -1) << name: 'A' >>;
B = point(2, -1) << name: 'B' >>;
C = point(0, 2) << name: 'C' >>;

// 连接成三角形
triangle = polygon(A, B, C) << fillColor: 'lightblue' >>;
```

**说明**：
- `--- ... ---` 是配置区域，设置画布范围和网格
- `point(x, y)` 创建点
- `polygon(A, B, C)` 创建多边形
- `<< >>` 内设置属性（颜色、大小等）

---

## 2. 核心语法 - 3 个基本元素

### 2.1 点 (Point)

```jessiecode
// 基本点
A = point(1, 2);

// 带样式的点
B = point(3, 4) <<
    strokeColor: 'red',
    fillColor: 'pink',
    size: 5,
    name: 'B'
>>;
```

### 2.2 线 (Line/Segment)

```jessiecode
// 直线（无限延伸）
l = line(A, B);

// 线段（有限长度）
s = segment(A, B);

// 射线（从 A 经过 B 延伸）
r = halfline(A, B);
```

### 2.3 圆 (Circle)

```jessiecode
// 圆心 O，经过点 A
c = circle(O, A);

// 带样式
c = circle(O, A) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

---

## 3. 常用几何构造

### 3.1 中点

```jessiecode
M = midpoint(A, B);
```

### 3.2 交点

```jessiecode
// 两直线交点
P = intersection(l1, l2, 0);

// 直线与圆交点（2 个交点）
P1 = intersection(l, c, 0);  // 第一个交点
P2 = intersection(l, c, 1);  // 第二个交点
```

### 3.3 垂线

```jessiecode
// 过点 P 作直线 l 的垂线
perp = perpendicular(l, P);
```

### 3.4 平行线

```jessiecode
// 过点 P 作直线 l 的平行线
para = parallel(l, P);
```

---

## 4. 常见问题 FAQ

### Q1: 为什么我的图形不显示？

**检查清单**：
- [ ] 坐标是否在 `boundingBox` 范围内？
- [ ] 元素是否正确引用（变量名拼写正确）？
- [ ] 是否忘记加分号 `;`？

### Q2: 对象属性应该用什么括号？

**答案**：使用 `<< >>`，不是 `{}`！

```jessiecode
// 错误！
A = point(1, 2) { strokeColor: 'red' };

// 正确！
A = point(1, 2) << strokeColor: 'red' >>;
```

### Q3: 如何为函数添加参数？

**答案**：JessieCode 的函数需要括号：

```jessiecode
// 错误！
A = point 1, 2;

// 正确！
A = point(1, 2);
```

### Q4: 交点有两个，如何选择？

**答案**：使用索引参数（0 或 1）：

```jessiecode
// 第一个交点
P1 = intersection(l, c, 0);

// 第二个交点
P2 = intersection(l, c, 1);
```

### Q5: 如何添加动态文本？

**答案**：使用 `function()`：

```jessiecode
text(0, 0, function() {
    return "距离 = " + dist(A, B).toFixed(2);
});
```

---

## 5. 学习路径

完成本快速入门后，建议按以下顺序学习：

### 第一步：浏览示例索引
- 查看 [examples-index.md](./examples-index.md) 找到感兴趣的示例

### 第二步：学习核心 API
- 阅读 [api/Point.md](./api/Point.md) - 点的用法
- 阅读 [api/Line.md](./api/Line.md) - 线的用法
- 阅读 [api/Circle.md](./api/Circle.md) - 圆的用法

### 第三步：掌握几何构造
- [api/Midpoint.md](./api/Midpoint.md) - 中点
- [api/Intersection.md](./api/Intersection.md) - 交点
- [api/Perpendicular.md](./api/Perpendicular.md) - 垂线
- [api/Parallel.md](./api/Parallel.md) - 平行线

### 第四步：进阶主题
- [grammar.md](./grammar.md) - 完整语法规则
- 滑块 (Slider) - 动态参数
- 函数图 (Functiongraph) - 函数图像

---

## 6. 参考资源

| 资源 | 描述 |
|------|------|
| [grammar.md](./grammar.md) | 完整语法参考 |
| [api/](./api/) | 112 个元素的 API 文档 |
| [examples/](./examples/) | 38 个示例代码 |
| [SKILL.md](../SKILL.md) | 技能使用说明 |

---

**下一步**：打开 [examples-index.md](./examples-index.md) 浏览示例库！
