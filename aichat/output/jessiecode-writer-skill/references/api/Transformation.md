# Transformation 变换

## 描述

变换定义了二维投影变换，如平移、旋转、反射、缩放等。变换可以应用于点、线、圆、多边形等几何元素。

## JessieCode 语法

```js
// 创建变换
t = transform(parameters) << type: 'transformType' >>;

// 应用变换到元素
P2 = point(P1, t);  // 创建变换后的点
```

## 变换类型

### 1. 平移 (translate)

```js
// 平移向量 (dx, dy)
t = transform(dx, dy) << type: 'translate' >>;
```

| 参数 | 类型 | 描述 |
|------|------|------|
| dx | Number/Function | x 方向平移量 |
| dy | Number/Function | y 方向平移量 |

**变换矩阵**：
```
(1  0  0)
(0  1  0)  * (x, y, z) = (x+dx, y+dy, z)
(dx dy 1)
```

### 2. 缩放 (scale)

```js
// 缩放因子 (sx, sy)
t = transform(sx, sy) << type: 'scale' >>;
```

| 参数 | 类型 | 描述 |
|------|------|------|
| sx | Number/Function | x 方向缩放因子 |
| sy | Number/Function | y 方向缩放因子 |

**变换矩阵**：
```
(1  0  0)
(0  sx 0)  * (x, y, z) = (sx*x, sy*y, z)
(0  0  sy)
```

### 3. 旋转 (rotate)

```js
// 绕原点旋转
t = transform(alpha) << type: 'rotate' >>;

// 绕指定点旋转
t = transform(alpha, point) << type: 'rotate' >>;
t = transform(alpha, x, y) << type: 'rotate' >>;
```

| 参数 | 类型 | 描述 |
|------|------|------|
| alpha | Number/Function | 旋转角度（弧度） |
| point | Point | 旋转中心（可选） |
| x, y | Number | 旋转中心坐标（可选） |

**变换矩阵**（绕原点）：
```
(1   0       0   )
(0  cos(α) -sin(α))  * (x, y, z)
(0  sin(α)  cos(α))
```

### 4. 反射 (reflect)

```js
// 关于直线反射
t = transform(line) << type: 'reflect' >>;

// 关于两点定义的直线反射
t = transform(p1, p2) << type: 'reflect' >>;
```

| 参数 | 类型 | 描述 |
|------|------|------|
| line | Line | 反射轴（直线） |
| p1, p2 | Point | 定义反射轴的两个点 |

### 5. 剪切 (shear)

```js
// 剪切变换
t = transform(sx, sy) << type: 'shear' >>;
```

| 参数 | 类型 | 描述 |
|------|------|------|
| sx | Number/Function | x 方向剪切因子 |
| sy | Number/Function | y 方向剪切因子 |

**变换矩阵**：
```
(1  0  0)
(0  1  sx)  * (x, y, z) = (x+sx*z, y+sy*z, z)
(0  sy 1)
```

### 6. 通用/矩阵变换 (generic/matrix)

```js
// 通用 3x3 矩阵
t = transform(a, b, c, d, e, f, g, h, i) << type: 'generic' >>;

// 或直接提供矩阵
t = transform([[a,b,c], [d,e,f], [g,h,i]]) << type: 'matrix' >>;
```

## 示例

### 1. 平移变换

```js
// 创建点
A = point(1, 1);

// 平移变换：向右 2 单位，向上 3 单位
t = transform(2, 3) << type: 'translate' >>;

// 应用变换
B = point(A, t);  // B = (3, 4)

// 或使用动态值
s = slider([1, 4], [4, 4], [0, 1, 5]);
t2 = transform(function() { return V(s); }, 0) << type: 'translate' >>;
C = point(A, t2);  // C 随滑块移动
```

### 2. 缩放变换

```js
// 原始点
A = point(1, 1);

// 缩放：x 方向 2 倍，y 方向 0.5 倍
t = transform(2, 0.5) << type: 'scale' >>;

// 应用变换
B = point(A, t);  // B = (2, 0.5)

// 均匀缩放
t2 = transform(2, 2) << type: 'scale' >>;
C = point(A, t2);  // C = (2, 2)
```

### 3. 旋转变换

```js
// 原始点
A = point(1, 0);

// 绕原点旋转 90 度（PI/2 弧度）
t = transform(PI/2) << type: 'rotate' >>;
B = point(A, t);  // B = (0, 1)

// 绕指定点旋转
C = point(2, 0);  // 旋转中心
t2 = transform(PI/2, C) << type: 'rotate' >>;
D = point(A, t2);  // D 绕 C 旋转 90 度

// 动态旋转
angle = slider([1, 4], [4, 4], [0, 0, 2*PI]);
t3 = transform(function() { return V(angle); }, C) << type: 'rotate' >>;
E = point(A, t3);  // E 随角度旋转
```

### 4. 反射变换

```js
// 创建反射轴
l = line(point(0, 0), point(1, 1));  // y = x

// 原始点
A = point(2, 0);

// 反射变换
t = transform(l) << type: 'reflect' >>;

// 应用变换
B = point(A, t);  // B = (0, 2)

// 或使用两点定义反射轴
p1 = point(-1, 0);
p2 = point(1, 0);
t2 = transform(p1, p2) << type: 'reflect' >>;  // 关于 x 轴反射
C = point(point(0, 2), t2);  // C = (0, -2)
```

### 5. 变换串联

```js
// 原始点
A = point(1, 1);

// 定义多个变换
t1 = transform(-2, -1) << type: 'translate' >>;  // 平移
t2 = transform(PI/4) << type: 'rotate' >>;       // 旋转 45 度
t3 = transform(2, 1) << type: 'translate' >>;    // 平移

// 串联应用
B = point(A, [t1, t2, t3]);  // 依次应用 t1, t2, t3
```

### 6. 变换多边形

```js
// 原始三角形
A = point(-1, -1);
B = point(1, -1);
C = point(0, 1.5);
pol1 = polygon(A, B, C) << fillColor: 'blue' >>;

// 旋转变换
rot = transform(PI/3, point(0, 0)) << type: 'rotate' >>;

// 变换后的顶点
A2 = point(A, rot);
B2 = point(B, rot);
C2 = point(C, rot);

// 变换后的三角形
pol2 = polygon(A2, B2, C2) << fillColor: 'red', fillOpacity: 0.5 >>;
```

### 7. 正方形旋转演示

```js
// 创建正方形（通过变换）
sq = [];
right = transform(2, 0) << type: 'translate' >>;
up = transform(0, 2) << type: 'translate' >>;

// 第一个点可拖动
sq[0] = point(0, 0);
sq[1] = point(sq[0], right);
sq[2] = point(sq[0], [right, up]);
sq[3] = point(sq[0], up);

// 正方形
pol = polygon(sq[0], sq[1], sq[2], sq[3]) <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>;

// 旋转变换
angleSlider = point(0, 3);  // 拖动此点控制角度
rot = transform(function() {
    return atan2(angleSlider.Y(), angleSlider.X());
}, sq[0]) << type: 'rotate' >>;

// 绑定旋转到其他顶点
rot.bindTo(sq[1]);
rot.bindTo(sq[2]);
rot.bindTo(sq[3]);
```

### 8. 变换文本

```js
// 创建文本
txt = text(0.5, 0, "Hello World") << display: 'html' >>;

// 平移变换
p0 = point(0, 0);
tOff = transform(function() { return p0.X(); }, function() { return p0.Y(); }) << type: 'translate' >>;

// 绑定变换到文本
tOff.bindTo(txt);

// 当 p0 移动时，文本也会移动
```

### 9. 通用矩阵变换

```js
// 3x3 变换矩阵
// 错切变换示例
t = transform(
    [[1, 0, 0],
     [0.5, 1, 0],
     [0, 0, 1]]
) << type: 'matrix' >>;

// 应用变换
A = point(1, 0);
B = point(A, t);  // B = (1, 0.5)
```

### 10. 滑块控制变换

```js
// 滑块控制缩放
scaleX = slider([1, 4], [4, 4], [0.5, 1, 3]) << name: 'sx' >>;
scaleY = slider([1, 3.5], [3.5, 3.5], [0.5, 1, 3]) << name: 'sy' >>;

// 缩放变换
t = transform(function() { return V(scaleX); }, function() { return V(scaleY); }) << type: 'scale' >>;

// 原始图形
pol1 = polygon(point(-1, -1), point(1, -1), point(0, 1.5)) << fillColor: 'blue' >>;

// 变换后的图形
A2 = point(pol1.vertices[0], t);
B2 = point(pol1.vertices[1], t);
C2 = point(pol1.vertices[2], t);
pol2 = polygon(A2, B2, C2) << fillColor: 'red', fillOpacity: 0.5 >>;
```

### 11. 点关于直线的对称点

```js
// 反射轴
l = line(point(0, 0), point(4, 2));

// 原始点
A = point(2, 3);

// 反射变换
t = transform(l) << type: 'reflect' >>;

// 对称点
A2 = point(A, t);

// 验证：AA2 的中点在 l 上
M = midpoint(A, A2);
// M 应该在直线 l 上
```

### 12. 复合变换：平移 + 旋转 + 缩放

```js
// 定义变换
translate = transform(2, 1) << type: 'translate' >>;
rotate = transform(PI/4) << type: 'rotate' >>;
scale = transform(1.5, 1.5) << type: 'scale' >>;

// 原始点
A = point(1, 0);

// 依次应用变换
B = point(A, translate);      // 平移
C = point(B, rotate);         // 旋转
D = point(C, scale);          // 缩放

// 或一次性应用
E = point(A, [translate, rotate, scale]);
```

## 注意事项

1. **变换顺序**：变换串联时，顺序很重要，先应用的变换写在前面
2. **齐次坐标**：变换使用 3x3 矩阵，点在齐次坐标中表示为 (x, y, 1)
3. **旋转角度**：旋转角度使用弧度制，正值表示逆时针
4. **动态变换**：参数可以是函数，用于创建动态变换
5. **bindTo 方法**：可以使用 `bindTo()` 将变换绑定到元素，元素会随变换参数动态更新

## 相关元素

- [Point](./Point.md) - 点
- [Line](./Line.md) - 直线
- [Polygon](./Polygon.md) - 多边形
- [Slider](./Slider.md) - 滑块（控制变换参数）
