# ReflexAngle 优角

<!-- USAGE_FREQUENCY: common -->

## 描述

优角是角度大于 180° 的角。它由圆心、半径点和角度点三个点定义。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建优角
reflexAng = reflexangle(center, radiusPoint, anglePoint);

// 带属性创建
reflexAng = reflexangle(A, B, C) <<
    radius: 2,
    fillColor: 'lightgreen',
    strokeColor: 'green'
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| center | Point | 角的顶点（角度中心） |
| radiusPoint | Point | 半径点（定义起始边） |
| anglePoint | Point | 角度点（定义终止边） |

**注意**：优角从 radiusPoint 开始，逆时针绘制到 anglePoint 结束，角度始终大于 180°。

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `radius` | Number/String | 'auto' | 角度扇形半径 |
| `type` | String | 'sector' | 显示类型 |
| `withLabel` | Boolean | true | 是否显示标签 |
| `name` | String | 自动生成 | 角度名称（默认为希腊字母） |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#aaaaaa' | 填充颜色 |
| `fillOpacity` | Number | 0.3 | 填充透明度 |
| `visible` | Boolean | true | 是否可见 |

### 角度类型 (type)

| 值 | 描述 |
|----|------|
| `'sector'` | 扇形 |
| `'sectordot'` | 带点的扇形 |
| `'square'` | 正方形（用于直角） |
| `'none'` | 不显示填充 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `Value()` | unit: String | 获取角度值 |
| `Value('degrees')` | 无 | 获取角度值（度） |
| `Value('radians')` | 无 | 获取角度值（弧度） |
| `setAngle(val)` | val: Number | 设置角度值（弧度） |
| `free()` | 无 | 释放角度约束 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `deg(A, B, C)` | 计算角度（度） | `deg(A, B, C)` |
| `rad(A, B, C)` | 计算角度（弧度） | `rad(A, B, C)` |

## 示例

### 1. 创建基本优角

```js
// 三个自由点创建优角
p1 = point(5.0, 3.0);   // 顶点
p2 = point(1.0, 0.5);   // 起始点
p3 = point(1.5, 5.0);   // 终止点

// 创建优角
a = reflexangle(p1, p2, p3, << radius: 2 >>);

// 显示角度值
t = text(4, 4, function() { return JXG.toFixed(a.Value(), 2); });
```

### 2. 设置优角样式

```js
A = point(5.0, 3.0);
B = point(1.0, 0.5);
C = point(1.5, 5.0);

// 自定义半径和颜色
ang = reflexangle(A, B, C) <<
    radius: 2,
    fillColor: 'lightgreen',
    fillOpacity: 0.5,
    strokeColor: 'green'
>>;
```

### 3. 优角与非优角对比

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(0, 2);  // 90 度位置

// 非优角（<= 180°）- 显示较小的角
nonReflex = nonreflexangle(O, A, B) <<
    fillColor: 'lightblue',
    radius: 1,
    name: 'α'
>>;

// 优角（> 180°）- 显示较大的角（270°）
reflex = reflexangle(O, A, B) <<
    fillColor: 'lightgreen',
    radius: 1.5,
    name: 'β'
>>;

// 显示角度值
text(1, 3, "Non-reflex: " + nonReflex.Value('degrees').toFixed(1) + "°");
text(1, 2.5, "Reflex: " + reflex.Value('degrees').toFixed(1) + "°");
```

### 4. 动态优角

```js
// 可拖动的点
A = point(5, 3);
B = point(1, 0.5);
C = point(1.5, 5);

// 动态优角
ang = reflexangle(A, B, C) << radius: 2 >>;

// 实时更新角度值
text(4, 4, "Angle: " + function() {
    return JXG.toFixed(ang.Value('degrees'), 2) + "°";
});
```

### 5. 显示角度值作为标签

```js
A = point(5, 3);
B = point(1, 0.5);
C = point(1.5, 5);

// 标签显示角度值
ang = reflexangle(A, B, C) <<
    radius: 2,
    name: function() {
        return JXG.toFixed(ang.Value('degrees'), 1) + "°";
    }
>>;

// 或使用弧度
ang2 = reflexangle(D, E, F) <<
    name: function() {
        return JXG.toFixed(ang2.Value('radians'), 2);
    }
>>;
```

### 6. 完整圆周角演示

```js
// 圆心
O = point(0, 0);
A = point(2, 0);

// 几乎重合的点（创建接近 360°的优角）
B = point(1.99, 0.1);

// 优角
reflex = reflexangle(O, A, B) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    radius: 1.5
>>;

// 显示角度
text(1, 3, "Reflex Angle: " + reflex.Value('degrees').toFixed(1) + "°");
```

### 7. 优角与多边形外角

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
pol = polygon(A, B, C);

// 在顶点 B 处创建外角（优角）
// 需要延长一边
extendPoint = point(4, -1);  // AB 延长线上的点
extAngle = reflexangle(A, B, extendPoint) <<
    radius: 0.8,
    fillColor: 'orange',
    fillOpacity: 0.5
>>;

// 内角（非优角）
intAngle = nonreflexangle(A, B, C) <<
    radius: 0.5,
    fillColor: 'lightblue'
>>;

// 显示关系
text(0, -2, "Exterior: " + extAngle.Value('degrees').toFixed(1) + "°");
text(0, -2.5, "Interior: " + intAngle.Value('degrees').toFixed(1) + "°");
```

### 8. 时钟角度演示

```js
// 时钟中心
O = point(0, 0);

// 12 点位置
twelve = point(0, 2);

// 创建滑块模拟时间
hourSlider = slider([3, 3], [5, 3], [0, 12, 1]);

// 时针位置（简化计算）
hourAngle = function() {
    return (V(hourSlider) / 12) * 2 * PI;
};

hourPoint = point(function() { return 1.5 * sin(hourAngle()); },
                  function() { return 1.5 * cos(hourAngle()); });

// 从 12 点到时针的优角（表示经过的时间）
timeAngle = reflexangle(twelve, O, hourPoint) <<
    fillColor: 'lightyellow',
    fillOpacity: 0.6,
    radius: 1
>>;

// 显示时间
text(3, 3, "Hour: " + V(hourSlider));
text(3, 2.5, "Angle: " + timeAngle.Value('degrees').toFixed(1) + "°");
```

### 9. 设置固定角度值

```js
// 创建基础优角
A = point(5, 0);
B = point(0, 0);
C = point(0, 5);
ang = reflexangle(A, B, C);

// 设置为固定角度（240 度 = 4*PI/3 弧度）
ang.setAngle(4 * PI / 3);

// 或使用函数设置动态角度
slider1 = slider([1, 4], [4, 4], [PI, 2*PI, 0.1]);
ang.setAngle(function() { return V(slider1); });
```

### 10. 优角与圆弧的关系

```js
// 圆
O = point(0, 0);
A = point(2, 0);
c = circle(O, A);

// 圆上的点
B = glider(c);

// 优角对应的优弧
reflex = reflexangle(O, A, B) <<
    fillColor: 'lightgreen',
    fillOpacity: 0.3,
    radius: 0.5
>>;

// 对应的优弧
majorArc = arc(O, A, B) <<
    selection: 'major',
    strokeColor: 'green',
    strokeWidth: 3
>>;

// 显示关系
text(1, 3, "Reflex Angle: " + reflex.Value('degrees').toFixed(1) + "°");
```

## 注意事项

1. **角度限制**：优角的角度始终大于 180° 且小于 360°
2. **角度方向**：角度始终按逆时针方向测量
3. **自动标签**：如果不指定名称，会自动使用希腊字母（α, β, γ 等）
4. **半径**：可以使用 `radius: 'auto'` 让系统自动选择合适大小
5. **角度单位**：`Value()` 默认返回弧度，使用 `Value('degrees')` 返回角度
6. **与 NonReflexAngle 区别**：`reflexangle` 强制创建角度 > 180° 的角，而 `nonreflexangle` 创建角度 ≤ 180° 的角
7. **完整圆**：当角度接近 360° 时，优角几乎填满整个圆

## 相关元素

- [Angle](./Angle.md) - 角度
- [NonReflexAngle](./NonReflexAngle.md) - 非优角
- [Sector](./Sector.md) - 扇形
- [Arc](./Arc.md) - 圆弧
- [MajorSector](./MajorSector.md) - 优扇形
