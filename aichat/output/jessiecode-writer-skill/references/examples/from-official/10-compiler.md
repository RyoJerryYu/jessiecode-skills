# 函数作用域示例 (Function Scope Example)

## 图形描述

本示例演示了 JessieCode 中的函数定义、条件表达式和作用域相关特性：

- 全局变量定义
- 使用三元运算符的函数
- 函数内变量赋值
- 在函数内创建几何元素（点、数组）
- 数组元素修改
- 元素属性修改

## JessieCode 代码

```js
z = 1;
f = function(x) {
    return x < 0 ? 'neg' : 'pos';
};
h = function (x) {
    y = 2;
    return x + y;
};
g = function () {
    A = point(1, 1);
    a = [1, 2, 3, 4];
    a[1] = 5;
};
B = point(-1, 1);
B.strokeColor = 'pink';
```

## 知识点

1. **全局变量**：`z = 1` 在全局作用域定义变量
2. **三元运算符函数**：`x < 0 ? 'neg' : 'pos'` 根据条件返回不同字符串
3. **函数内赋值**：在函数内部给变量 y 赋值
4. **隐式全局变量**：函数内直接赋值 `y = 2` 创建隐式全局变量
5. **点的创建**：`point(1, 1)` 创建几何点
6. **数组字面量**：`[1, 2, 3, 4]` 创建数组
7. **数组元素修改**：`a[1] = 5` 修改数组第二个元素
8. **元素属性修改**：`B.strokeColor = 'pink'` 动态修改元素的描边颜色

## 涉及元素

- [Point](../../03-api/Point.md) - 点
- [Function](../../03-api/Function.md) - 函数
- [Array](../../03-api/Array.md) - 数组
