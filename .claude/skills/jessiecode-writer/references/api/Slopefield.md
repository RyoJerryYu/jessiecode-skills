# Slopefield 斜率场

## 描述

斜率场是一阶标量函数微分方程解的图形化表示。

给定一个返回数值的函数 f(x, y)，绘制其斜率场。

*定义于：* [vectorfield.js](./src/src_element_vectorfield.js.md)。
*继承自：* [Vectorfield](./Vectorfield.md)。

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
   → **[JXG.Curve](./JXG.Curve.md)**
      → **[Vectorfield](./Vectorfield.md)**
         → **Slopefield**

## JessieCode 语法

```js
// 基本语法 - 创建斜率场
field = slopefield(f, xData, yData);

// 带属性创建
field = slopefield(f, xData, yData) <<
    strokeColor: 'blue',
    strokeWidth: 1.5,
    scale: 0.5
>>;

// 动态斜率场（使用滑块控制）
field = slopefield(f,
    [-6, function() { return steps.Value(); }, 6],
    [-5, function() { return steps.Value(); }, 5]) <<
    scale: function() { return length.Value(); }
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| f | Function/String | 函数 f(x, y)，返回一个数值（斜率） |
| xData | Array | 长度为 3 的数组：[x 起始值，步数，x 结束值]。斜率场在 x 方向将包含 (步数) + 1 个向量 |
| yData | Array | 长度为 3 的数组：[y 起始值，步数，y 结束值]。斜率场在 y 方向将包含 (步数) + 1 个向量 |

### 参数说明

**函数 f(x, y)**
- 接收两个参数 x 和 y
- 返回一个数值，表示该点处的斜率 dy/dx

**xData 和 yData**
- 定义斜率场的网格范围和密度
- 格式：`[start, steps, end]`
  - `start`: 起始坐标值
  - `steps`: 步数（整数）
  - `end`: 结束坐标值
- 这三个值可以是数字或返回数字的函数（用于动态更新）

## 属性

斜率场继承自 Vectorfield，拥有其所有属性，并扩展了以下特有属性：

### 斜率场特有属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `scale` | Number/Function | 1 | 设置向量的长度（用户坐标单位） |
| `arrowhead` | Object | 见下文 | 自定义向量箭头的样式 |

### arrowhead 箭头属性

| 字段 | 类型 | 描述 |
|------|------|------|
| `enabled` | Boolean | 是否启用箭头（默认 false，启用会降低性能） |
| `size` | Number | 箭头腿的长度（像素），默认 5 |
| `angle` | Number | 箭头腿的角度（弧度），默认 Math.PI * 0.125 |

**默认值：** `{enabled: false, size: 5, angle: Math.PI * 0.125}`

### 继承属性（来自 Vectorfield/Curve）

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `highlightStrokeColor` | String | '#ffff00' | 高亮时的颜色 |
| `highlightStrokeWidth` | Number | 3 | 高亮时的线宽 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |

## 方法

### setF(func)

设置斜率场的定义函数。

**参数：**
- `func`: 函数 f(x, y)，返回一个数值

**返回值：**
- `{Object}` 斜率场对象的引用

**示例：**
```js
field.setF((x, y) => x * x + y * y);
board.update();
```

## 示例

### 1. 基本斜率场

```js
// 简单的斜率场：dy/dx = x² - x - 2
field = slopefield(
    (x, y) => x * x - x - 2,
    [-6, 25, 6],  // 水平网格：从 -6 到 6，25 步
    [-5, 20, 5]   // 垂直网格：从 -5 到 5，20 步
);
```

### 2. 带样式的斜率场

```js
// 自定义颜色和线宽
field = slopefield(
    (x, y) => x * x - y * y,
    [-6, 20, 6],
    [-5, 20, 5]
) <<
    strokeColor: 'blue',
    strokeWidth: 1.5,
    highlightStrokeWidth: 0.5
>>;
```

### 3. 动态斜率场（滑块控制）

```js
// 滑块控制向量长度
lengthSlider = slider([-3, 7], [3, 7], [0, 0.33, 1]) << name: 'length' >>;

// 滑块控制步数
stepSlider = slider([-3, 6], [3, 6], [1, 20, 100]) <<
    name: 'steps',
    snapWidth: 1
>>;

// 动态斜率场
field = slopefield(
    (x, y) => x * x - y * y,
    [-6, function() { return V(stepSlider); }, 6],
    [-5, function() { return V(stepSlider); }, 5]
) <<
    strokeWidth: 1.5,
    highlightStrokeColor: '#0000ff',
    scale: function() { return V(lengthSlider); },
    arrowhead: <<
        enabled: false,
        size: 8,
        angle: PI / 16
    >>
>>;
```

### 4. 带箭头的斜率场

```js
// 注意：启用箭头会降低性能
field = slopefield(
    (x, y) => 2 * x,
    [-5, 15, 5],
    [-5, 15, 5]
) <<
    strokeColor: 'green',
    strokeWidth: 1,
    scale: 0.5,
    arrowhead: <<
        enabled: true,
        size: 6,
        angle: PI / 12
    >>
>>;
```

### 5. 常见微分方程的斜率场

```js
// dy/dx = y（指数增长）
expField = slopefield(
    (x, y) => y,
    [-5, 20, 5],
    [-3, 15, 3]
) << strokeColor: 'red' >>;

// dy/dx = -x/y（圆）
circleField = slopefield(
    (x, y) => -x / y,
    [-4, 16, 4],
    [-4, 16, 4]
) << strokeColor: 'blue' >>;

// dy/dx = sin(x) * cos(y)
waveField = slopefield(
    (x, y) => sin(x) * cos(y),
    [-2*PI, 25, 2*PI],
    [-2*PI, 25, 2*PI]
) << strokeColor: 'purple' >>;
```

### 6. 动态函数斜率场

```js
// 滑块控制参数
a = slider([-3, -2.5], [3, -2.5], [-3, 1, 3]) << name: 'a' >>;

// 斜率场函数随滑块变化：dy/dx = a*x
field = slopefield(
    function(x, y) { return V(a) * x; },
    [-5, 20, 5],
    [-5, 20, 5]
) << strokeColor: 'blue' >>;
```

### 7. 使用 setF 方法更新函数

```js
// 初始斜率场
field = slopefield(
    (x, y) => x,
    [-4, 16, 4],
    [-4, 16, 4]
);

// 之后更新函数
field.setF((x, y) => x * x - y);
board.update();
```

### 8. 斜率场与解曲线结合

```js
// 创建斜率场
field = slopefield(
    (x, y) => 2 * x,
    [-3, 18, 3],
    [-2, 12, 2]
) << strokeColor: 'gray', strokeWidth: 0.5 >>;

// 创建一个特解曲线（通过某点的积分曲线）
// dy/dx = 2x 的通解是 y = x² + C
solution1 = functiongraph((x) => x * x - 1, -3, 3) << strokeColor: 'red', strokeWidth: 2 >>;
solution2 = functiongraph((x) => x * x + 1, -3, 3) << strokeColor: 'blue', strokeWidth: 2 >>;
solution3 = functiongraph((x) => x * x, -3, 3) << strokeColor: 'green', strokeWidth: 2 >>;
```

## 注意事项

1. **性能考虑**：启用箭头（`arrowhead.enabled: true`）会显著降低渲染性能，建议在大网格中禁用
2. **步数选择**：步数越多，斜率场越密集，但渲染越慢。通常 15-25 步即可
3. **scale 属性**：与 Vectorfield 不同，Slopefield 的 scale 属性设置的是向量的绝对长度（用户坐标单位），而不是缩放因子
4. **函数定义域**：确保函数 f(x, y) 在整个网格范围内有定义，避免出现除零等错误
5. **动态更新**：xData 和 yData 中的值可以是函数，用于创建动态更新的斜率场

## 相关元素

- [Vectorfield](./Vectorfield.md) - 向量场（父类）
- [Functiongraph](./Functiongraph.md) - 函数图像（绘制解曲线）
- [Slider](./Slider.md) - 滑块（控制参数）
- [Curve](./Curve.md) - 曲线（祖父类）
