# CircumcircleArc 外接圆弧

<!-- USAGE_FREQUENCY: advanced -->

## 描述

外接圆弧是通过三个点的圆弧。它是由这三个点确定的外接圆的一部分，从第一个点逆时针经过第二个点绘制到第三个点。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建外接圆弧
arc = circumcirclearc(A, B, C);

// 带属性创建
arc = circumcirclearc(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 显示圆心
arc = circumcirclearc(A, B, C) <<
    center: <<
        visible: true,
        strokeColor: 'red',
        size: 5
    >>
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| A | Point | 第一个点（圆弧起点） |
| B | Point | 第二个点（圆弧经过的点） |
| C | Point | 第三个点（圆弧终点） |

**注意**：圆弧从点 A 开始，逆时针经过点 B，到点 C 结束。

## 属性

外接圆弧继承自 Arc，因此具有所有圆弧的属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线 |
| `opacity` | Number | 1.0 | 透明度 |
| `visible` | Boolean | true | 是否可见 |
| `selection` | String | 'auto' | 弧的类型：'minor', 'major', 'auto' |
| `center` | Object | - | 圆心属性 |

### 弧的类型 (selection)

| 值 | 描述 |
|----|------|
| `'minor'` | 劣弧（小于半圆） |
| `'major'` | 优弧（大于半圆） |
| `'auto'` | 自动选择（默认） |

## 方法

外接圆弧继承自 Arc，因此具有所有圆弧的方法：

| 方法 | 参数 | 描述 |
|------|------|------|
| `Value()` | unit: String | 获取弧长或角度 |
| `Value('length')` | 无 | 获取弧长 |
| `Value('radians')` | 无 | 获取角度（弧度） |
| `Value('degrees')` | 无 | 获取角度（度） |
| `Radius()` | 无 | 获取半径 |

## 示例

### 1. 创建基本外接圆弧

```js
// 三个点定义外接圆弧
A = point(2, 2);
B = point(1, 0.5);
C = point(3.5, 1);

// 创建外接圆弧（从 A 经过 B 到 C）
arc = circumcirclearc(A, B, C);

// 带样式的外接圆弧
arc = circumcirclearc(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;
```

### 2. 显示圆心和半径

```js
// 三个点
A = point(1.5, 5);
B = point(1, 0.5);
C = point(5, 3);

// 外接圆弧，显示圆心
arc = circumcirclearc(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    center: <<
        visible: true,
        strokeColor: 'red',
        fillColor: 'black',
        size: 5,
        withLabel: true,
        name: 'O'
    >>
>>;

// 显示半径
text(1, 6, function() {
    return "Radius: " + arc.Radius().toFixed(3);
});
```

### 3. 动态外接圆弧

```js
// 可移动的点
A = point(2, 2);
B = point(1, 0.5);
C = point(3.5, 1);  // 可以拖动

// 外接圆弧随点移动而更新
arc = circumcirclearc(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 显示弧长
text(1, 3, function() {
    return "Arc length: " + arc.Value('length').toFixed(3);
});

// 显示角度
text(1, 2.5, function() {
    return "Angle: " + arc.Value('degrees').toFixed(1) + "°";
});
```

### 4. 外接圆弧与外接圆

```js
// 三角形顶点
A = point(1, 1);
B = point(5, 1);
C = point(3, 4);

// 完整的外接圆
circumcircle = circumcircle(A, B, C) <<
    strokeColor: 'gray',
    dash: 1,
    fillOpacity: 0.1
>>;

// 外接圆弧（从 A 经过 B 到 C）
arc = circumcirclearc(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 显示圆心
O = circumcenter(A, B, C) <<
    visible: true,
    strokeColor: 'red',
    size: 5
>>;
```

### 5. 劣弧与优弧

```js
// 基础点
A = point(2, 0);
B = point(1, 1);
C = point(0, 2);

// 劣弧（默认）
minorArc = circumcirclearc(A, B, C) <<
    selection: 'minor',
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 优弧
majorArc = circumcirclearc(A, B, C) <<
    selection: 'major',
    strokeColor: 'red',
    strokeWidth: 3
>>;
```

### 6. 外接圆弧与圆弧对比

```js
// 先创建外接圆弧的三个点
A = point(2, 2);
B = point(1, 0.5);
C = point(3.5, 1);

// 外接圆弧（自动确定圆心和半径）
arc1 = circumcirclearc(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 使用普通圆弧需要先确定圆心
O = circumcenter(A, B, C);
arc2 = arc(O, A, C) <<
    strokeColor: 'red',
    strokeWidth: 1,
    dash: 1
>>;
```

### 7. 获取外接圆弧属性

```js
// 三个点
A = point(1, 0);
B = point(0, 1);
C = point(-1, 0);

// 外接圆弧
arc = circumcirclearc(A, B, C);

// 获取半径
r = arc.Radius();

// 获取弧长（默认）
len1 = arc.Value();

// 获取弧长（显式）
len2 = arc.Value('length');

// 获取角度（弧度）
angleRad = arc.Value('radians');

// 获取角度（度）
angleDeg = arc.Value('degrees');

// 显示值
text(-2, 2, "Radius: " + r.toFixed(3));
text(-2, 1.5, "Length: " + len2.toFixed(3));
text(-2, 1, "Angle: " + angleDeg.toFixed(1) + "°");
```

### 8. 多个外接圆弧组合

```js
// 圆上的点
A = point(2, 0);
B = point(0, 2);
C = point(-2, 0);
D = point(0, -2);

// 不同的外接圆弧
arc1 = circumcirclearc(A, B, C) << strokeColor: 'blue' >>;
arc2 = circumcirclearc(B, C, D) << strokeColor: 'red' >>;
arc3 = circumcirclearc(C, D, A) << strokeColor: 'green' >>;
arc4 = circumcirclearc(D, A, B) << strokeColor: 'orange' >>;
```

### 9. 外接圆弧变换

```js
// 原始外接圆弧
A = point(1, 1);
B = point(0, 0);
C = point(2, 0);

arc1 = circumcirclearc(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 创建平移变换
translate = transform(3, 1) << type: 'translate' >>;

// 变换后的圆弧
arc2 = curve(arc1, translate) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

### 10. 圆周角演示

```js
// 圆上三点
A = point(2, 0);
B = point(0, 2);
C = point(-2, 0);

// 外接圆弧
arc = circumcirclearc(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 完整的外接圆
O = circumcenter(A, B, C);
c = circle(O, A) <<
    strokeColor: 'gray',
    dash: 1
>>;

// 圆上任意点（圆周角顶点）
P = glider(c);

// 圆心角
centerAngle = angle(A, O, C) <<
    radius: 0.5,
    fillColor: 'lightblue'
>>;

// 圆周角
inscribedAngle = angle(A, P, C) <<
    radius: 0.5,
    fillColor: 'lightgreen'
>>;

// 显示关系
text(-2, 2.5, "Center: " + centerAngle.Value('degrees') + "°");
text(-2, 2, "Inscribed: " + inscribedAngle.Value('degrees') + "°");
```

## 注意事项

1. **方向**：外接圆弧始终从第一个点逆时针经过第二个点绘制到第三个点
2. **三点确定**：三个点唯一确定一个外接圆弧
3. **与 Arc 的区别**：`circumcirclearc` 自动通过三点确定圆心和半径，而 `arc` 需要显式指定圆心
4. **选择类型**：使用 `selection` 属性可以强制绘制劣弧或优弧
5. **圆心属性**：通过 `center` 属性可以控制圆心的显示和样式

## 相关元素

- [Circumcenter](./Circumcenter.md) - 外心
- [Circumcircle](./Circumcircle.md) - 外接圆
- [CircumcircleSector](./CircumcircleSector.md) - 外接圆扇形
- [Arc](./Arc.md) - 圆弧
- [Circle](./Circle.md) - 圆
- [Sector](./Sector.md) - 扇形
