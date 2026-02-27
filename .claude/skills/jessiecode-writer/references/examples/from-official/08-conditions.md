# 属性合并示例 (Property Merge Example)

## 图形描述

本示例演示了 JessieCode 中属性对象（对象字面量）的定义和合并使用：

- 定义空对象 `<<>>`
- 定义命名的颜色属性对象（cerise 樱桃色、grass 草绿色）
- 定义可见性属性对象
- 定义线宽属性对象（thick 粗线、thin 细线）
- 在创建点时合并多个属性对象
- 演示属性的覆盖（thin 后被 thick 覆盖）

注意：原文件名为 `merge_props.html`，但实际内容是属性合并示例。

## JessieCode 代码

```js
empty = <<>>;
cerise = <<
    strokeColor: '#901B77',
    fillColor: '#CA147A'
>>;
grass = <<
    strokeColor: '#009256',
    fillColor: '#65B72E'
>>;
visible = <<
    visible: true,
    withLabel: true
>>;
thick = << strokeWidth: 4 >>;
thin = << strokeWidth: 1>>;
P = point(1, 1) cerise, thick, visible, << size: 10 >>;
Q = point(3, 2) grass, thick, visible;
R = point(-2, 3) cerise, thin, thick;
```

## 知识点

1. **空对象**：`<<>>` 创建空属性对象
2. **属性对象定义**：使用 `<< key: value >>` 语法定义可复用的属性对象
3. **十六进制颜色**：`#901B77` 等十六进制颜色代码
4. **属性合并**：在元素后使用逗号分隔多个属性对象进行合并
5. **属性覆盖**：后面定义的属性会覆盖前面的同名属性（如 R 的 thin 被 thick 覆盖）
6. **内联属性**：`<< size: 10 >>` 直接在元素创建时定义属性
7. **点的样式**：strokeColor（描边颜色）、fillColor（填充颜色）、size（大小）

## 涉及元素

- [Point](../../03-api/Point.md) - 点
