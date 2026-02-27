# 创建者属性值 (Creator Attribute Values)

## 图形描述

本示例演示了如何在 JessieCode 中组合使用多个属性对象来创建具有复杂样式的元素。通过定义可复用的属性对象，可以简洁地为元素设置多种视觉效果。

## JessieCode 代码

```js
// Prepare some visual properties
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
thin = << strokeWidth: 1 >>;

P = point(1, 1) cerise, thick, visible, << size: 10 >>;
Q = point(3, 2) grass, thick, visible;
R = point(-2, 3) cerise, thin;
plot(function (x) {
    return sin(x)*cos(x);
});

a = function (x) {
    point(1, 1) cerise, thick;
    return sin(x)cos(x);
};
```

## 知识点

1. **属性对象定义**：使用 `<< ... >>` 语法定义可复用的属性对象
2. **属性对象组合**：在创建元素时，可以依次列出多个属性对象，用逗号分隔
3. **内联属性**：除了使用预定义的属性对象，还可以直接内联定义 `<< size: 10 >>`
4. **函数定义**：使用 `function(x) { return ... }` 定义数学函数
5. **函数绘图**：使用 `plot(function)` 绘制函数图像
6. **属性继承**：后定义的属性会覆盖先定义的属性（如果有冲突）

## 涉及元素

- [Point](../../03-api/Point.md) - 点
- [Functiongraph](../../03-api/Functiongraph.md) - 函数图像
- JessieCode 语法：属性对象、函数定义
