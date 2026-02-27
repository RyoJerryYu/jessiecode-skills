# 性能基准测试示例 / Performance Benchmark Example

## 图形描述

此示例展示了一个动态函数绘图，用于性能基准测试。代码绘制了一个正弦函数图像，其振幅由点 `A` 的位置决定（`sin(x) * A.X() * A.X()`）。当点 A 被拖动时，函数图像的振幅会实时更新。这个简单的示例可用于测试 JSXGraph/JessieCode 在动态更新场景下的渲染性能。

## JessieCode 代码

```javascript
plot(function (x) {
    return sin(x)*A.X()*A.X();
});
```

## 知识点

1. **函数绘图**：`plot()` 函数用于绘制函数图像
2. **内联函数**：直接在 `plot()` 内部定义匿名函数
3. **三角函数**：`sin(x)` 计算正弦值
4. **元素坐标**：`A.X()` 获取点 A 的 X 坐标
5. **动态依赖**：函数图像依赖于点 A 的位置，实现动态更新
6. **链式调用**：多个操作可以组合在单个表达式中

## 涉及元素

| 元素 | 描述 | API 文档链接 |
|------|------|-------------|
| `plot` | 绘制函数图像的 JessieCode 内置函数 | [JessieCode - plot](https://jsxgraph.org/docs/symbols/JessieCode.html) |
| `sin` | 正弦三角函数 | [MDN - Math.sin](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/sin) |
| `point.X()` | 获取点的 X 坐标 | [JSXGraph - Point#X](https://jsxgraph.org/docs/symbols/Point.html#X) |

---

*来源：JessieCode 官方示例 - jcbench.html*
