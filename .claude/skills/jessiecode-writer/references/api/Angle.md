# Angle 角度

<!-- USAGE_FREQUENCY: core -->

## 描述

角度由三个点或两条直线定义。角度始终按逆时针方向从第一个点（或第一条线）到第三个点（或第二条线）围绕第二个点（或交点）绘制。

## JessieCode 语法

```js
// 通过三个点创建角度
ang = angle(p1, p2, p3);

// 带属性创建
ang = angle(A, B, C) <<
    radius: 1,
    type: 'sector',
    withLabel: true
>>;
```

## 参数

### 方式一：三个点

| 参数 | 类型 | 描述 |
|------|------|------|
| p1 | Point | 起始点 |
| p2 | Point | 顶点（角度中心） |
| p3 | Point | 终止点 |

**注意**：角度始终逆时针从 p1 到 p3 围绕 p2 绘制。

### 方式二：两条直线

| 参数 | 类型 | 描述 |
|------|------|------|
| line1 | Line | 第一条直线 |
| line2 | Line | 第二条直线 |
| coord1 | Array | 第一条线上的点坐标 |
| coord2 | Array | 第二条线上的点坐标 |
| radius | Number | 角度半径 |

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

### 1. 创建基本角度

```js
// 三个点定义角度
A = point(5, 3);
B = point(1, 0.5);  // 顶点
C = point(1.5, 5);
ang = angle(A, B, C);

// 显示角度值
text(4, 4, "Angle: " + ang.Value('degrees') + "°");
```

### 2. 设置角度样式

```js
// 自定义半径和颜色
ang1 = angle(A, B, C) <<
    radius: 1.5,
    strokeColor: 'red',
    fillColor: 'pink',
    fillOpacity: 0.5
>>;

// 无填充，仅弧线
ang2 = angle(D, E, F) <<
    type: 'none',
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 3. 直角标记

```js
// 创建直角三角形
A = point(0, 0);
B = point(3, 0);
C = point(0, 4);

// 直角在 A 点
rightAngle = angle(B, A, C) <<
    type: 'square',
    fillColor: 'none',
    strokeColor: 'black'
>>;
```

### 4. 显示角度值作为标签

```js
// 标签显示角度值
ang = angle(A, B, C) <<
    radius: 1,
    name: function() {
        return JXG.toFixed(ang.Value('degrees'), 1) + "°";
    }
>>;

// 或使用弧度
ang2 = angle(D, E, F) <<
    name: function() {
        return JXG.toFixed(ang2.Value('radians'), 2);
    }
>>;
```

### 5. 使用全局函数计算角度

```js
A = point(1, 0);
B = point(0, 0);
C = point(0, 1);

// 使用 deg 函数
angleDeg = deg(A, B, C);  // 90

// 使用 rad 函数
angleRad = rad(A, B, C);  // PI/2

text(2, 2, "Angle: " + angleDeg + " degrees");
```

### 6. 动态角度

```js
// 可拖动的点
A = point(3, 0);
B = point(0, 0);
C = point(0, 3);

// 动态角度
ang = angle(A, B, C) << radius: 0.8 >>;

// 实时更新角度值
text(1, 1, "Angle: " + function() {
    return JXG.toFixed(ang.Value('degrees'), 2) + "°";
});
```

### 7. 设置固定角度值

```js
// 创建基础角度
A = point(5, 0);
B = point(0, 0);
C = point(0, 5);
ang = angle(A, B, C);

// 设置为固定角度（60 度 = PI/3 弧度）
ang.setAngle(PI / 3);

// 或使用函数设置动态角度
slider1 = slider([1, 4], [4, 4], [0, PI/2, PI]);
ang.setAngle(function() { return V(slider1); });
```

### 8. 两条直线形成的角度

```js
// 创建两条直线
p1 = point(-1, 4);
p2 = point(4, 1);
q1 = point(-2, -3);
q2 = point(4, 3);

l1 = line(p1, p2);
l2 = line(q1, q2);

// 创建角度（通过直线和方向）
ang1 = angle(l1, l2, [5.5, 0], [4, 3]) << radius: 1 >>;
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

// 圆心角
centerAngle = angle(A, O, B) <<
    radius: 0.8,
    fillColor: 'lightblue'
>>;

// 圆周角
inscribedAngle = angle(A, C, B) <<
    radius: 0.6,
    fillColor: 'lightgreen'
>>;

// 显示关系
text(-2, 2.5, "Center: " + centerAngle.Value('degrees') + "°");
text(-2, 2, "Inscribed: " + inscribedAngle.Value('degrees') + "°");
```

### 10. 多边形内角和

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
pol = polygon(A, B, C);

// 三个内角
angA = angle(B, A, C) << radius: 0.5, fillColor: 'red' >>;
angB = angle(C, B, A) << radius: 0.5, fillColor: 'green' >>;
angC = angle(A, C, B) << radius: 0.5, fillColor: 'blue' >>;

// 内角和
sumText = text(0, -2, "Sum: " + function() {
    return (angA.Value('degrees') + angB.Value('degrees') + angC.Value('degrees')).toFixed(1) + "°";
});
```

## 注意事项

1. **角度方向**：角度始终按逆时针方向测量
2. **自动标签**：如果不指定名称，会自动使用希腊字母（α, β, γ 等）
3. **半径**：可以使用 `radius: 'auto'` 让系统自动选择合适大小
4. **角度单位**：`Value()` 默认返回弧度，使用 `Value('degrees')` 返回角度
5. **直角检测**：当角度接近 90 度时，根据 `orthoType` 可能显示正方形标记

## 相关元素

- [Sector](./Sector.md) - 扇形
- [Arc](./Arc.md) - 圆弧
- [Polygon](./Polygon.md) - 多边形（内角）
