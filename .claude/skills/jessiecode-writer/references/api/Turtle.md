# Turtle 海龟画笔

<!-- USAGE_FREQUENCY: advanced -->

## 描述

海龟画笔（Turtle）是一种类似于 Logo 或 PostScript 编程语言的图形范式。通过控制一只"海龟"在画布上移动并绘制轨迹，可以创建各种几何图形和图案。

## JessieCode 语法

```js
// 基本语法 - 创建海龟画笔
t = turtle(x, y, angle);

// 在原点创建海龟
t = turtle(0, 0);

// 指定初始角度
t = turtle(0, 0, 90);  // 初始朝上

// 带属性创建
t = turtle(0, 0) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    visible: true
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number/Function | 海龟初始位置的 x 坐标 |
| y | Number/Function | 海龟初始位置的 y 坐标 |
| angle | Number/Function (可选) | 海龟初始方向的角度（度），默认为 0（向右） |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 画笔颜色 |
| `strokeWidth` | Number | 1 | 画笔宽度（像素） |
| `strokeOpacity` | Number | 1.0 | 画笔透明度 |
| `visible` | Boolean | true | 海龟是否可见 |
| `arrow` | Object | - | 海龟箭头的属性 |

### 箭头属性 (arrow)

```js
t = turtle(0, 0) <<
    arrow: <<
        strokeWidth: 2,
        strokeColor: 'red',
        size: 10
    >>
>>;
```

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeWidth` | Number | 2 | 箭头边框宽度 |
| `strokeColor` | String | 继承 strokeColor | 箭头颜色 |
| `size` | Number | 10 | 箭头大小 |

## 方法

### 移动方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `forward(len)` / `fd(len)` | len: Number | 向前移动 len 单位并绘制轨迹 |
| `back(len)` / `bk(len)` | len: Number | 向后移动 len 单位并绘制轨迹 |
| `moveTo(target)` | target: Point/Array | 移动到指定位置（不改变方向） |
| `setPos(x, y)` | x, y: Number | 设置位置（不绘制轨迹） |
| `home()` | 无 | 返回原点 (0, 0)，方向归零 |

### 旋转方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `left(angle)` / `lt(angle)` | angle: Number | 向左（逆时针）旋转 angle 度 |
| `right(angle)` / `rt(angle)` | angle: Number | 向右（顺时针）旋转 angle 度 |
| `lookTo(target)` | target: Number/Point/Array | 转向指定角度或位置 |

### 画笔控制

| 方法 | 参数 | 描述 |
|------|------|------|
| `penDown()` / `pd()` | 无 | 落下画笔（绘制轨迹） |
| `penUp()` / `pu()` | 无 | 抬起画笔（不绘制轨迹） |

### 状态管理

| 方法 | 参数 | 描述 |
|------|------|------|
| `clearScreen()` / `cs()` | 无 | 清除所有轨迹，重置到初始状态 |
| `clean()` | 无 | 清除所有轨迹，保持当前位置 |
| `hideTurtle()` / `ht()` | 无 | 隐藏海龟图标 |
| `showTurtle()` / `st()` | 无 | 显示海龟图标 |

### 堆栈操作

| 方法 | 参数 | 描述 |
|------|------|------|
| `pushTurtle()` / `push()` | 无 | 保存当前状态到堆栈 |
| `popTurtle()` / `pop()` | 无 | 从堆栈恢复状态 |

### 画笔属性设置

| 方法 | 参数 | 描述 |
|------|------|------|
| `setPenSize(size)` | size: Number | 设置画笔宽度 |
| `setPenColor(color)` | color: String | 设置画笔颜色 |
| `setHighlightPenColor(color)` | color: String | 设置高亮颜色 |
| `getPenSize()` | 无 | 获取当前画笔宽度 |
| `getPenColor()` | 无 | 获取当前画笔颜色 |
| `getHighlightPenColor()` | 无 | 获取当前高亮颜色 |
| `setAttribute(attrs)` | attrs: Object | 设置属性（对所有轨迹生效） |

## 示例

### 1. 创建基本海龟

```js
// 在原点创建海龟
t = turtle(0, 0);

// 移动海龟绘制正方形
t.forward(100);
t.right(90);
t.forward(100);
t.right(90);
t.forward(100);
t.right(90);
t.forward(100);
```

### 2. 设置海龟样式

```js
// 创建带样式的海龟
t = turtle(0, 0) <<
    strokeColor: 'blue',
    strokeWidth: 3,
    strokeOpacity: 0.8
>>;

// 自定义箭头样式
t2 = turtle(5, 5) <<
    arrow: <<
        strokeWidth: 2,
        strokeColor: 'red',
        size: 15
    >>
>>;
```

### 3. 使用简写方法

```js
t = turtle(0, 0);

// 使用简写方法
t.fd(50);   // forward 的简写
t.rt(60);   // right 的简写
t.fd(50);
t.rt(60);
t.fd(50);
t.rt(60);
t.fd(50);
t.rt(60);
t.fd(50);
```

### 4. 抬笔和落笔

```js
t = turtle(0, 0);

// 绘制虚线
for (i = 0; i < 10; i = i + 1) {
    t.pd();     // 落笔
    t.fd(10);   // 绘制 10 单位
    t.pu();     // 抬笔
    t.fd(10);   // 移动不绘制
}
```

### 5. 绘制正多边形

```js
// 绘制正六边形
t = turtle(0, 0);
n = 6;  // 边数
len = 50;  // 边长

for (i = 0; i < n; i = i + 1) {
    t.fd(len);
    t.rt(360 / n);
}

// 绘制正五边形
t2 = turtle(100, 0);
for (i = 0; i < 5; i = i + 1) {
    t2.fd(60);
    t2.rt(72);  // 360/5 = 72
}
```

### 6. 使用堆栈保存状态

```js
t = turtle(0, 0);

// 保存初始状态
t.push();

// 绘制第一个正方形
for (i = 0; i < 4; i = i + 1) {
    t.fd(50);
    t.rt(90);
}

// 恢复到初始状态
t.pop();

// 改变方向
t.lt(45);

// 绘制第二个正方形（从初始位置旋转 45 度）
for (i = 0; i < 4; i = i + 1) {
    t.fd(50);
    t.rt(90);
}
```

### 7. 螺旋图案

```js
t = turtle(0, 0);

// 绘制螺旋
for (i = 0; i < 50; i = i + 1) {
    t.fd(i * 2);    // 每次前进距离增加
    t.rt(90);       // 右转 90 度
}
```

### 8. 星星图案

```js
t = turtle(0, 0) << strokeColor: 'gold', strokeWidth: 2 >>;

// 绘制五角星
for (i = 0; i < 5; i = i + 1) {
    t.fd(100);
    t.rt(144);  // 180 - 36 = 144 度（外角）
}
```

### 9. 动态海龟（使用函数）

```js
// 使用滑块控制边长
s = slider([1, 4], [4, 4], [10, 50, 100]);

// 创建海龟
t = turtle(0, 0);

// 使用滑块值绘制三角形
t.fd(function() { return V(s); });
t.rt(120);
t.fd(function() { return V(s); });
t.rt(120);
t.fd(function() { return V(s); });
```

### 10. 分形树

```js
t = turtle(0, -100) << strokeColor: 'brown' >>;

// 简单的递归树函数（需要 JessieCode 支持函数定义）
// 这里用迭代方式演示
t.pu();
t.setPos(0, -100);
t.pd();

// 主干
t.setPenSize(8);
t.fd(80);

// 保存位置，绘制左分支
t.push();
t.lt(30);
t.setPenSize(4);
t.fd(50);

// 恢复位置，绘制右分支
t.pop();
t.rt(30);
t.setPenSize(4);
t.fd(50);
```

### 11. 海龟位置操作

```js
t = turtle(0, 0);

// 移动到指定位置（不绘制）
t.setPos(50, 50);

// 落笔绘制
t.pd();
t.fd(30);

// 抬笔移动到新位置
t.pu();
t.moveTo([100, 100]);

// 继续绘制
t.pd();
t.fd(30);

// 返回原点
t.home();
```

### 12. 多色图案

```js
t = turtle(0, 0) << strokeWidth: 3 >>;

// 绘制彩色正方形
colors = ['red', 'green', 'blue', 'purple'];

for (i = 0; i < 4; i = i + 1) {
    t.setPenColor(colors[i]);
    t.fd(80);
    t.rt(90);
}
```

### 13. 圆形近似

```js
t = turtle(0, 0);

// 用多边形近似圆形
n = 36;  // 边数
len = 10;  // 每边长度

for (i = 0; i < n; i = i + 1) {
    t.fd(len);
    t.rt(360 / n);  // 每次转 10 度
}
```

### 14. 清除和重置

```js
t = turtle(0, 0);

// 绘制一些图形
t.fd(50);
t.rt(90);
t.fd(50);

// 清除轨迹但保持位置
t.clean();

// 继续绘制（从当前位置开始，无之前的轨迹）
t.fd(30);

// 完全重置（清除轨迹并返回初始状态）
t.cs();
```

### 15. 海龟可见性控制

```js
t = turtle(0, 0);

// 隐藏海龟图标（只显示轨迹）
t.ht();  // 或 t.hideTurtle()

// 绘制
t.fd(100);
t.rt(90);
t.fd(100);

// 显示海龟图标
t.st();  // 或 t.showTurtle()
```

## 注意事项

1. **角度单位**：旋转角度使用度数（degree），不是弧度
2. **方向**：初始方向向右（0 度），逆时针为正方向
3. **简写方法**：`fd`/`bk`/`lt`/`rt`/`pd`/`pu`/`ht`/`st`/`cs` 是相应完整方法名的简写
4. **堆栈深度**：堆栈操作支持多层嵌套，`push` 和 `pop` 成对使用
5. **轨迹属性**：使用 `setPenColor` 和 `setPenSize` 设置的属性只影响之后的轨迹
6. **全局属性**：使用 `setAttribute` 可以一次性设置所有轨迹的属性
7. **clean vs clearScreen**：`clean()` 清除轨迹但保持位置，`clearScreen()` 或 `cs()` 会重置所有状态

## 相关元素

- [Glider](./Glider.md) - 滑点（可在海龟轨迹上滑动）
- [Curve](./Curve.md) - 曲线（海龟轨迹本质是曲线）
- [Button](./Button.md) - 按钮（可用于控制海龟动作）
- [Transformation](./Transformation.md) - 变换（可对海龟进行变换）
