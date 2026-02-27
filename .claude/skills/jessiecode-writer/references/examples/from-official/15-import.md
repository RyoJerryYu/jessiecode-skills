# 导入模块示例 (Import Module Example)

## 图形描述

本示例演示了 JessieCode 中的模块导入功能和贝塞尔曲线构造：

- 导入几何模块（Math/Geometry）
- 导入数值计算模块（Math/Numerics）
- 创建四个控制点
- 使用数值模块计算贝塞尔曲线
- 使用曲线函数创建贝塞尔曲线

## JessieCode 代码

```js
geo = import('Math/Geometry');
num = import('Math/Numerics');
A = point(3, 1);
B = point(1, 1);
C = point(1, 3);
D = point(-1, 2);
arr = num.bezier([A, B, C, D]);
path = curve(arr[0], arr[1], arr[2]);
```

## 知识点

1. **模块导入**：`import('Math/Geometry')` 导入几何模块
2. **数值模块**：`import('Math/Numerics')` 导入数值计算模块
3. **模块方法调用**：`num.bezier()` 调用数值模块的贝塞尔曲线方法
4. **点的创建**：`point(x, y)` 创建二维点
5. **数组参数**：`[A, B, C, D]` 将点作为数组传递给函数
6. **贝塞尔曲线**：使用四个控制点定义三次贝塞尔曲线
7. **曲线创建**：`curve(dataX, dataY, dataZ)` 创建参数曲线
8. **数组访问**：`arr[0]`、`arr[1]`、`arr[2]` 访问数组元素

## 涉及元素

- [Point](../../03-api/Point.md) - 点
- [Curve](../../03-api/Curve.md) - 曲线
- [Import](../../03-api/Import.md) - 导入模块
