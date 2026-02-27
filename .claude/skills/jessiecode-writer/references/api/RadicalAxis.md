# RadicalAxis 根轴

<!-- USAGE_FREQUENCY: advanced -->

## 描述

根轴是连接两个不同圆心圆的两个交点的直线。圆心关于另一个圆的极线的角平分线始终是根轴。当两圆相交时，根轴经过交点。当以两圆心连线的中点为圆心、经过两圆心的圆与已知两圆相交时，极线经过这些交点。

## JessieCode 语法

```js
// 通过两个圆创建根轴
ra = radicalaxis(c1, c2);

// 带属性创建
ra = radicalaxis(c1, c2) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    dash: 1,
    withLabel: true
>>;
```

## 参数

| 参数组合 | 类型 | 描述 |
|----------|------|------|
| circle1, circle2 | Circle, Circle | 两个不同圆心的圆 |

## 属性

根轴继承自直线（Line），因此具有直线的所有属性。

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线，3=点划线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 根轴名称 |

## 示例

### 1. 创建基本根轴

```js
// 创建两个圆的圆心和半径点
p1 = point(2, 3);
p2 = point(1, 4);
c1 = circle(p1, p2);

p3 = point(6, 5);
p4 = point(8, 6);
c2 = circle(p3, p4);

// 创建根轴
ra = radicalaxis(c1, c2);
```

### 2. 设置根轴样式

```js
// 创建两个圆
O1 = point(0, 0);
A1 = point(2, 0);
c1 = circle(O1, A1) << strokeColor: 'red' >>;

O2 = point(5, 0);
A2 = point(7, 0);
c2 = circle(O2, A2) << strokeColor: 'blue' >>;

// 创建带样式的根轴
ra = radicalaxis(c1, c2) <<
    strokeColor: 'green',
    strokeWidth: 2,
    dash: 1
>>;
```

### 3. 带标签的根轴

```js
// 创建两个相交的圆
O1 = point(0, 0);
O2 = point(3, 0);
c1 = circle(O1, 2.5);
c2 = circle(O2, 2.5);

// 创建带标签的根轴
ra = radicalaxis(c1, c2) <<
    withLabel: true,
    name: '根轴'
>>;
```

### 4. 相交圆的根轴

```js
// 创建两个相交的圆
O1 = point(0, 0);
O2 = point(4, 0);
c1 = circle(O1, 3);
c2 = circle(O2, 3);

// 根轴经过两个交点
ra = radicalaxis(c1, c2) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;

// 可以创建交点来验证
// 交点会在根轴上
```

### 5. 动态圆的根轴

```js
// 创建可移动的点
O1 = point(0, 0);
O2 = point(5, 0);

// 半径点可以拖动改变半径
R1 = point(2, 0);
R2 = point(3, 0);

// 创建动态圆
c1 = circle(O1, R1);
c2 = circle(O2, R2);

// 根轴会随着圆的变化而动态更新
ra = radicalaxis(c1, c2) <<
    strokeColor: 'blue',
    dash: 1
>>;
```

### 6. 根轴与极线的关系

```js
// 创建两个圆
O1 = point(0, 0);
O2 = point(6, 0);
c1 = circle(O1, 2);
c2 = circle(O2, 3);

// 创建根轴
ra = radicalaxis(c1, c2);

// 根轴是圆心关于另一个圆的极线的角平分线
// 这是一个几何性质，可以通过作图验证
```

### 7. 完整示例：两圆位置关系演示

```js
// 设置画板
// boundingbox: [-5, 5, 5, -5]

// 圆 1：圆心和半径
O1 = point(0, 0) <<
    strokeColor: 'red',
    fillColor: 'red',
    size: 4
>>;
R1 = point(2, 0);
c1 = circle(O1, R1) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 圆 2：圆心和半径
O2 = point(5, 0) <<
    strokeColor: 'blue',
    fillColor: 'blue',
    size: 4
>>;
R2 = point(3, 0);
c2 = circle(O2, R2) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 根轴
ra = radicalaxis(c1, c2) <<
    strokeColor: 'green',
    strokeWidth: 3,
    dash: 1,
    withLabel: true,
    name: '根轴'
>>;
```

## 注意事项

1. **圆心必须不同**：两个圆的圆心必须不同，否则无法创建根轴
2. **根轴的性质**：
   - 当两圆相交时，根轴经过两个交点
   - 当两圆相切时，根轴是过切点的公切线
   - 当两圆相离时，根轴在两圆之间
3. **等幂性**：根轴上的任意一点到两圆的幂相等
4. **垂直性**：根轴垂直于两圆心的连线
5. **继承属性**：根轴继承自直线，具有直线的所有属性和方法

## 相关元素

- [Circle](./Circle.md) - 圆
- [Line](./Line.md) - 直线
- [Polar](./Polar.md) - 极线
- [Tangent](./Tangent.md) - 切线
