# 生成项示例 (Generate Term Example)

## 图形描述

本示例演示了 JessieCode 中函数图像（plot）的 `generateTerm` 方法使用：

- 创建正弦函数图像
- 调用 `generateTerm` 方法生成新的项
- 更新画布显示

## JessieCode 代码

```js
p = plot(sin);
p.generateTerm('x', 'x', tan);
$board.update();
```

## 知识点

1. **函数图像**：`plot(sin)` 创建正弦函数图像
2. **内置函数**：`sin`、`tan` 是内置三角函数
3. **generateTerm 方法**：为函数图像生成新的代数项
   - 第一个参数 `'x'`：变量名
   - 第二个参数 `'x'`：项名
   - 第三个参数 `tan`：要添加的函数
4. **画布更新**：`$board.update()` 强制刷新画布重绘

## 涉及元素

- [Plot](../../03-api/Plot.md) - 函数图像
- [Board](../../03-api/Board.md) - 画板
