# 综合示例 (Comprehensive JessieCode Example)

## 图形描述

本示例是一个综合性的 JessieCode 演示，展示了多种高级功能：

- 创建多个点并进行动态属性绑定
- 使用函数动态计算点的坐标
- 通过 `$()` 语法获取元素并修改属性
- 创建中点和外接圆
- 使用条件表达式动态设置填充颜色
- 定义自定义函数（加法函数、抛物线函数、分段函数）
- 创建圆、函数图像（plot）
- 使用十六进制颜色代码和 strokeWidth 设置样式
- 演示对象字面量和数组的嵌套访问

## JessieCode 代码

```js
use jxgbox;
point(2, 3) << strokeColor : 'yellow', fillColor : 'green', id: 'wrzpfrmpf', name: 'A' >>;
B = point(1, 1);
C = point(-1, 1);
D = point(2, -2);
sqrt4 = 3.14159265358 ~= PI;
D.X = function () {
    return A.X() + 1 - X(B);
};
$('wrzpfrmpf').strokeColor = 'black';
M = point('(A.X()+B.X())/2', '(A.Y()+B.Y())/2');
M.free();
CC = circumcircle('wrzpfrmpf', B, C) << center: << visible: true, withLabel: true, name: 'The Midpoint' >>, strokeColor: 'red' >>;
l = line(A, B);
B.fillColor = function () {
    if (A.X() > 0) {
        return 'green';
    } else {
        return 'red';
    }
};
add = function(a, b) {
    if (b > 0) {
        return a + b;
    } else {
        return a - b;
    }
};
parab = function(x) {
    return A.X()*x^2;
};
circle('wrzpfrmpf', M);
p = plot(parab);
plot(function (x) {
    if (x > 0) {
        return B.Y()*cos(x*3+2);
    } else {
        return B.Y()*sin(x*3+2);
    }
});
p.strokeColor = '#CDEB8B';
p.strokeWidth = 4;
obj = << foo: 3, bar: 'baz', sub: << this: 99 >> >>;
val = obj.sub.this;
arr = [function () { return [3, 4]; }];
foobar = arr[0]()[1];
```

## 知识点

1. **模块导入**：`use jxgbox;` 导入 JSXGraph 基础模块
2. **点的创建与属性**：使用 `point(x, y)` 创建点，并通过 `<< >>` 设置属性（strokeColor、fillColor、id、name）
3. **变量赋值**：`B = point(1, 1)` 将创建的元素赋值给变量
4. **常量近似**：`~= PI` 将数值近似为圆周率常量
5. **动态坐标函数**：`D.X = function() { ... }` 设置点的 X 坐标为动态计算函数
6. **$() 选择器语法**：`$('id')` 通过 ID 获取已创建的元素
7. **中点构造**：使用字符串表达式 `'(A.X()+B.X())/2'` 创建中点坐标
8. **释放点的自由性**：`M.free()` 使点变为自由点
9. **外接圆**：`circumcircle(point1, point2, point3)` 创建三点确定的外接圆
10. **嵌套属性**：`center: << visible: true, ... >>` 为中心点设置嵌套属性
11. **直线**：`line(A, B)` 创建通过两点的直线
12. **条件填充色**：使用函数根据条件返回不同颜色
13. **自定义函数**：定义带参数和条件逻辑的函数
14. **抛物线函数**：使用点坐标动态构造抛物线
15. **圆**：`circle(center, point)` 创建以点为圆心、过另一点的圆
16. **函数图像**：`plot(function)` 绘制函数图像
17. **分段函数图像**：使用条件表达式定义分段函数
18. **样式属性**：strokeColor（十六进制）、strokeWidth
19. **对象字面量**：`<< key: value >>` 语法创建嵌套对象
20. **数组与函数调用链**：`arr[0]()[1]` 演示复杂的嵌套访问

## 涉及元素

- [Point](../../03-api/Point.md) - 点
- [Circle](../../03-api/Circle.md) - 圆
- [Circumcircle](../../03-api/Circumcircle.md) - 外接圆
- [Line](../../03-api/Line.md) - 直线
- [Plot](../../03-api/Plot.md) - 函数图像
