# Conic 圆锥曲线

<!-- USAGE_FREQUENCY: advanced -->

## 描述

圆锥曲线是通过五个点或圆锥曲线一般方程的系数创建的通用圆锥截面。

如果圆锥曲线由以下方程的系数定义：

*Ax² + Bxy + Cy² + Dx + Ey + F = 0*

则可以通过指定这 6 个系数来创建圆锥曲线。

## JessieCode 语法

```js
// 通过五个点创建圆锥曲线
c = conic(A, B, C, D, E);

// 通过方程系数创建圆锥曲线
// 参数顺序：A, C, F, B/2, D/2, E/2
c = conic(A, C, F, B_2, D_2, E_2);

// 带属性创建
c = conic(A, B, C, D, E) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    visible: true
>>;
```

## 参数

### 方式一：五个点

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point/Array/Function | 第一个点 |
| point2 | Point/Array/Function | 第二个点 |
| point3 | Point/Array/Function | 第三个点 |
| point4 | Point/Array/Function | 第四个点 |
| point5 | Point/Array/Function | 第五个点 |

**注意**：五个点必须不共线且任意四点不共圆，否则无法唯一确定圆锥曲线。

### 方式二：六个系数（圆锥曲线方程）

| 参数 | 类型 | 描述 |
|------|------|------|
| a00 (A) | Number/Function | x² 的系数 |
| a11 (C) | Number/Function | y² 的系数 |
| a22 (F) | Number/Function | 常数项 |
| a01 (B/2) | Number/Function | xy 系数的一半 |
| a02 (D/2) | Number/Function | x 系数的一半 |
| a12 (E/2) | Number/Function | y 系数的一半 |

**注意**：参数顺序为 `A, C, F, B/2, D/2, E/2`，对应方程 `Ax² + Bxy + Cy² + Dx + Ey + F = 0`

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 圆锥曲线名称 |

### 专用属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `center` | Point | 圆锥曲线的中心点属性（椭圆/双曲线） |
| `foci` | Point | 焦点属性 |
| `point` | Point | 定义圆锥曲线的五个点的属性 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `getType()` | 无 | 获取圆锥曲线类型（'ellipse', 'hyperbola', 'parabola'） |
| `getX()` | 无 | 获取中心点 x 坐标（如果存在） |
| `getY()` | 无 | 获取中心点 y 坐标（如果存在） |

## 示例

### 1. 通过五个点创建圆锥曲线

```js
// 创建五个点
A = point(1, 5);
B = point(1, 2);
C = point(2, 0);
D = point(0, 0);
E = point(-1, 5);

// 通过五个点创建圆锥曲线
conic = conic(A, B, C, D, E);
```

### 2. 通过系数创建椭圆

```js
// 创建椭圆：x² + 2y² - 4 = 0
// 参数：A=1, C=2, F=-4, B/2=0, D/2=0, E/2=0
ellipse = conic(1, 2, -4, 0, 0, 0);
```

### 3. 通过系数创建圆

```js
// 创建单位圆：x² + y² - 1 = 0
// 参数：A=1, C=1, F=-1, B/2=0, D/2=0, E/2=0
circle = conic(1, 1, -1, 0, 0, 0);
```

### 4. 通过系数创建双曲线

```js
// 创建双曲线：x² - y² - 1 = 0
// 参数：A=1, C=-1, F=-1, B/2=0, D/2=0, E/2=0
hyperbola = conic(1, -1, -1, 0, 0, 0);
```

### 5. 通过系数创建抛物线

```js
// 创建抛物线：y - x² = 0，即 x² - y = 0
// 这个需要特殊处理，因为标准形式不同
// 实际上抛物线的一般形式需要更复杂的系数
```

### 6. 设置圆锥曲线的样式

```js
// 创建五个点
A = point(2, 3);
B = point(4, 1);
C = point(5, 4);
D = point(3, 6);
E = point(1, 5);

// 创建带样式的圆锥曲线
conic = conic(A, B, C, D, E) <<
    strokeColor: 'blue',
    strokeWidth: 3,
    dash: 1,
    opacity: 0.8
>>;
```

### 7. 动态圆锥曲线

```js
// 创建滑块控制点的位置
t = slider(0, 2*PI, 0.01);

// 创建动态点
A = point(function() { return 3 * cos(V(t)); },
          function() { return 3 * sin(V(t)); });
B = point(2, 0);
C = point(0, 2);
D = point(-2, 0);
E = point(0, -2);

// 圆锥曲线随点 A 移动而变化
conic = conic(A, B, C, D, E);
```

### 8. 访问圆锥曲线的属性

```js
// 创建椭圆
A = point(3, 0);
B = point(0, 2);
C = point(-3, 0);
D = point(0, -2);
E = point(2, 1.5);

ellipse = conic(A, B, C, D, E);

// 获取类型
type = ellipse.getType();  // 'ellipse'

// 获取中心坐标
cx = ellipse.getX();
cy = ellipse.getY();
```

## 圆锥曲线类型判断

根据方程 `Ax² + Bxy + Cy² + Dx + Ey + F = 0` 的系数，可以判断圆锥曲线的类型：

| 判别式 | 类型 |
|--------|------|
| B² - 4AC < 0 | 椭圆（包括圆） |
| B² - 4AC = 0 | 抛物线 |
| B² - 4AC > 0 | 双曲线 |

## 注意事项

1. **五个点的约束**：通过五个点创建时，必须确保任意三点不共线，且任意四点不共圆
2. **系数顺序**：使用系数方式创建时，参数顺序为 `A, C, F, B/2, D/2, E/2`
3. **退化情况**：某些系数组合可能导致退化的圆锥曲线（如两条直线）
4. **中心点**：只有椭圆和双曲线有中心点，抛物线没有中心点
5. **动态更新**：当使用函数或依赖其他元素时，圆锥曲线会动态更新

## 相关元素

- [Point](./Point.md) - 点
- [Circle](./Circle.md) - 圆
- [Ellipse](./Ellipse.md) - 椭圆
- [Arc](./Arc.md) - 圆弧
