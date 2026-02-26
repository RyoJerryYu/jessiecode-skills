# NonReflexAngle 非优角

## 描述

非优角是角度不超过 180° 的角。它由圆心、半径点和角度点三个点定义。

## JessieCode 语法

```js
// 基本语法 - 通过三个点创建非优角
nonReflexAng = nonreflexangle(center, radiusPoint, anglePoint);

// 带属性创建
nonReflexAng = nonreflexangle(A, B, C) <<
    radius: 1,
    fillColor: 'lightblue',
    strokeColor: 'blue'
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| center | Point | 角的顶点（角度中心） |
| radiusPoint | Point | 半径点（定义起始边） |
| anglePoint | Point | 角度点（定义终止边） |

**注意**：非优角从 radiusPoint 开始，逆时针绘制到 anglePoint 结束，角度始终小于或等于 180°。

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

### 直角属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `orthoType` | String | 'square' | 直角显示类型 |
| `orthoSensitivity` | Number | 1.0 | 直角检测灵敏度（度） |

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

### 1. 创建基本非优角

```js
// 三个点定义非优角
p1 = point(5.0, 3.0);   // 顶点
p2 = point(1.0, 0.5);   // 起始点
p3 = point(1.5, 5.0);   // 终止点

// 创建非优角
a = nonreflexangle(p1, p2, p3);

// 显示角度值
t = text(4, 4, function() { return JXG.toFixed(a.Value(), 2); });
```

### 2. 设置非优角样式

```js
A = point(5.0, 3.0);
B = point(1.0, 0.5);
C = point(1.5, 5.0);

// 自定义半径和颜色
ang = nonreflexangle(A, B, C) <<
    radius: 2,
    fillColor: 'lightblue',
    fillOpacity: 0.5,
    strokeColor: 'blue'
>>;
```

### 3. 直角标记

```js
// 创建直角三角形
A = point(0, 0);
B = point(3, 0);
C = point(0, 4);

// 在 A 点创建非优角（直角）
rightAngle = nonreflexangle(B, A, C) <<
    type: 'square',
    fillColor: 'none',
    strokeColor: 'black'
>>;
```

### 4. 显示角度值作为标签

```js
A = point(5, 3);
B = point(1, 0.5);
C = point(1.5, 5);

// 标签显示角度值
ang = nonreflexangle(A, B, C) <<
    radius: 1,
    name: function() {
        return JXG.toFixed(ang.Value('degrees'), 1) + "°";
    }
>>;

// 或使用弧度
ang2 = nonreflexangle(D, E, F) <<
    name: function() {
        return JXG.toFixed(ang2.Value('radians'), 2);
    }
>>;
```

### 5. 动态非优角

```js
// 可拖动的点
A = point(5, 3);
B = point(1, 0.5);
C = point(1.5, 5);

// 动态非优角
ang = nonreflexangle(A, B, C) << radius: 1 >>;

// 实时更新角度值
text(4, 4, "Angle: " + function() {
    return JXG.toFixed(ang.Value('degrees'), 2) + "°";
});
```

### 6. 设置固定角度值

```js
// 创建基础非优角
A = point(5, 0);
B = point(0, 0);
C = point(0, 5);
ang = nonreflexangle(A, B, C);

// 设置为固定角度（60 度 = PI/3 弧度）
ang.setAngle(PI / 3);

// 或使用函数设置动态角度
slider1 = slider([1, 4], [4, 4], [0, PI/2, PI]);
ang.setAngle(function() { return V(slider1); });
```

### 7. 非优角与优角对比

```js
// 基础点
O = point(0, 0);
A = point(2, 0);
B = point(0, 2);  // 90 度位置

// 非优角（<= 180°）
nonReflex = nonreflexangle(O, A, B) <<
    fillColor: 'lightblue',
    radius: 1
>>;

// 优角（> 180°）- 使用 reflexangle
reflex = reflexangle(O, A, B) <<
    fillColor: 'lightgreen',
    radius: 1
>>;
```

### 8. 三角形内角和

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
pol = polygon(A, B, C);

// 三个内角（都是非优角）
angA = nonreflexangle(B, A, C) << radius: 0.5, fillColor: 'red' >>;
angB = nonreflexangle(C, B, A) << radius: 0.5, fillColor: 'green' >>;
angC = nonreflexangle(A, C, B) << radius: 0.5, fillColor: 'blue' >>;

// 内角和
sumText = text(0, -2, "Sum: " + function() {
    return (angA.Value('degrees') + angB.Value('degrees') + angC.Value('degrees')).toFixed(1) + "°";
});
```

### 9. 圆周角定理演示

```js
// 圆
O = point(0, 0);
A = point(2, 0);
c = circle(O, A);

// 圆上的点
B = glider(c);
C = glider(c);

// 圆心角（非优角）
centerAngle = nonreflexangle(A, O, B) <<
    radius: 0.8,
    fillColor: 'lightblue'
>>;

// 圆周角（非优角）
inscribedAngle = nonreflexangle(A, C, B) <<
    radius: 0.6,
    fillColor: 'lightgreen'
>>;

// 显示关系
text(-2, 2.5, "Center: " + centerAngle.Value('degrees') + "°");
text(-2, 2, "Inscribed: " + inscribedAngle.Value('degrees') + "°");
```

### 10. 使用全局函数计算角度

```js
A = point(1, 0);
B = point(0, 0);
C = point(0, 1);

// 使用 deg 函数
angleDeg = deg(A, B, C);  // 90

// 使用 rad 函数
angleRad = rad(A, B, C);  // PI/2

text(2, 2, "Angle: " + angleDeg + " degrees");

// 创建非优角可视化
ang = nonreflexangle(A, B, C) <<
    radius: 0.5,
    fillColor: 'yellow'
>>;
```

## 注意事项

1. **角度限制**：非优角的角度始终小于或等于 180°
2. **角度方向**：角度始终按逆时针方向测量
3. **自动标签**：如果不指定名称，会自动使用希腊字母（α, β, γ 等）
4. **半径**：可以使用 `radius: 'auto'` 让系统自动选择合适大小
5. **角度单位**：`Value()` 默认返回弧度，使用 `Value('degrees')` 返回角度
6. **直角检测**：当角度接近 90 度时，根据 `orthoType` 可能显示正方形标记
7. **与 ReflexAngle 区别**：`nonreflexangle` 强制创建角度 ≤ 180°的角，而 `reflexangle` 创建角度 > 180°的角

## 相关元素

- [Angle](./Angle.md) - 角度
- [ReflexAngle](./ReflexAngle.md) - 优角
- [Sector](./Sector.md) - 扇形
- [Arc](./Arc.md) - 圆弧
- [Polygon](./Polygon.md) - 多边形（内角）
