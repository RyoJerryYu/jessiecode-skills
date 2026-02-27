# Ellipse 椭圆

## 描述

椭圆是一种特殊的圆锥曲线，由两个焦点和椭圆上的第三个点定义，或由两个焦点和长轴长度定义。

## JessieCode 语法

```js
// 通过三个点创建椭圆
ellipse = ellipse(focus1, focus2, pointOnEllipse);

// 通过两个焦点和长轴长度创建
ellipse = ellipse(focus1, focus2, majorAxisLength);

// 带属性创建
ellipse = ellipse(F1, F2, P) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 椭圆弧（指定参数范围）
ellipseArc = ellipse(F1, F2, P, startAngle, endAngle);
```

## 参数

### 方式一：三个点

| 参数 | 类型 | 描述 |
|------|------|------|
| focus1 | Point/Array | 第一个焦点 |
| focus2 | Point/Array | 第二个焦点 |
| pointOnEllipse | Point/Array | 椭圆上的点 |

### 方式二：两个焦点加长轴

| 参数 | 类型 | 描述 |
|------|------|------|
| focus1 | Point/Array | 第一个焦点 |
| focus2 | Point/Array | 第二个焦点 |
| majorAxisLength | Number/Function | 长轴长度 |

### 方式三：椭圆弧

| 参数 | 类型 | 描述 |
|------|------|------|
| focus1 | Point/Array | 第一个焦点 |
| focus2 | Point/Array | 第二个焦点 |
| pointOnEllipse | Point/Array | 椭圆上的点 |
| start | Number (可选) | 起始角度，默认 0 |
| end | Number (可选) | 结束角度，默认 2π |

## 属性

椭圆继承自 Conic，因此拥有 Conic 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |

## 示例

### 1. 创建基本椭圆

```js
// 三个点定义椭圆
F1 = point(-1, 4);  // 焦点 1
F2 = point(-1, -4); // 焦点 2
P = point(1, 1);    // 椭圆上的点

ellipse1 = ellipse(F1, F2, P);
```

### 2. 使用长轴长度

```js
// 两个焦点
F1 = point(-2, 0);
F2 = point(2, 0);

// 长轴长度 = 6
ellipse2 = ellipse(F1, F2, 6);
```

### 3. 椭圆弧

```js
// 完整椭圆
p1 = point(-1, 2);
p2 = point(1, 2);
p3 = point(0, 3);

// 椭圆弧（从 0 到 π）
ellipseArc = ellipse(p1, p2, p3, 0, PI) <<
    lastArrow: << type: 7 >>
>>;
```

### 4. 动态椭圆

```js
// 可移动的焦点
F1 = point(-2, 0);
F2 = point(2, 0);

// 可移动的点
P = point(0, 3);

// 动态椭圆
ellipse = ellipse(F1, F2, P) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 显示焦距
distText = text(0, 4, function() {
    return "F1F2 = " + dist(F1, F2).toFixed(2);
});
```

### 5. 椭圆定义演示

```js
// 焦点
F1 = point(-2, 0);
F2 = point(2, 0);

// 椭圆上的动点
P = point(3, 0);

// 创建椭圆
ellipse = ellipse(F1, F2, P);

// 显示 PF1 + PF2 = 常数
sumDist = text(0, 4, function() {
    return "PF1 + PF2 = " + (dist(P, F1) + dist(P, F2)).toFixed(2);
});

// 绘制线段
r1 = segment(P, F1) << strokeColor: 'red' >>;
r2 = segment(P, F2) << strokeColor: 'blue' >>;
```

### 6. 椭圆参数

```js
// 创建椭圆
F1 = point(-3, 0);
F2 = point(3, 0);
P = point(5, 0);
el = ellipse(F1, F2, P);

// 获取椭圆属性（需要通过元素方法）
// 长轴、短轴、离心率等需要通过计算获得
```

### 7. 同心椭圆

```js
// 共同焦点
F1 = point(-1, 0);
F2 = point(1, 0);

// 不同大小的椭圆
e1 = ellipse(F1, F2, point(3, 0)) << strokeColor: 'red' >>;
e2 = ellipse(F1, F2, point(4, 0)) << strokeColor: 'blue' >>;
e3 = ellipse(F1, F2, point(5, 0)) << strokeColor: 'green' >>;
```

### 8. 椭圆的切线

```js
// 椭圆
F1 = point(-2, 0);
F2 = point(2, 0);
P = point(0, 3);
el = ellipse(F1, F2, P);

// 椭圆上的点
M = glider(el);

// 切线（如果支持）
// tangent = tangent(M);
```

### 9. 椭圆与圆的关系

```js
// 当两个焦点重合时，椭圆变为圆
F1 = point(0, 0);
F2 = point(0, 0);  // 与 F1 重合
P = point(3, 0);

// 这是一个半径为 3 的圆
circleLikeEllipse = ellipse(F1, F2, P);

// 或者使用动态焦点
F1Dyn = point(-1, 0);
F2Dyn = point(1, 0);
// 当 F1Dyn 和 F2Dyn 重合时，椭圆变成圆
```

### 10. 椭圆轨道演示

```js
// 太阳（焦点）
Sun = point(0, 0) <<
    strokeColor: 'yellow',
    fillColor: 'yellow',
    size: 8,
    face: 'circle'
>>;

// 第二个焦点（空）
F2 = point(2, 0) << visible: false >>;

// 行星轨道
orbit = ellipse(Sun, F2, point(4, 0)) <<
    strokeColor: 'white',
    strokeWidth: 2
>>;

// 行星
planet = glider(orbit) <<
    strokeColor: 'blue',
    fillColor: 'blue',
    size: 4
>>;
```

## 注意事项

1. **几何定义**：椭圆上任意点到两焦点的距离之和为常数（等于长轴长度）
2. **离心率**：e = c/a，其中 c 是焦距的一半，a 是长轴的一半
3. **椭圆弧**：通过指定 start 和 end 参数可以创建椭圆弧
4. **退化情况**：当两焦点重合时，椭圆退化为圆

## 相关元素

- [Conic](./Conic.md) - 圆锥曲线（父类）
- [Hyperbola](./Hyperbola.md) - 双曲线
- [Parabola](./Parabola.md) - 抛物线
- [Circle](./Circle.md) - 圆（特殊情况）
