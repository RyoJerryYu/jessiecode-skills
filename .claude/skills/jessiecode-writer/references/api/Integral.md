# Integral 积分

## 描述

积分元素用于可视化给定函数在指定区间内的积分面积，并计算该面积的值。它显示函数曲线与 x 轴之间在给定区间内所围成的区域。

*定义于：* [composition.js](./src/src_element_composition.js)
*继承自：* [JXG.Curve](./JXG.Curve)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement)**
    ↳ **[JXG.Curve](./JXG.Curve)**
         ↳ **Integral**

## JessieCode 语法

```js
// 基本语法 - 创建积分区域
i = integral([a, b], curve);

// 带属性创建
i = integral([a, b], curve) <<
    fillOpacity: 0.3,
    fillColor: 'yellow',
    strokeColor: 'blue'
>>;

// 获取积分值
value = Value(i);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| interval | Array | 积分区间 [a, b]，其中 a 为下限，b 为上限 |
| curve | Curve/FunctionGraph | 要积分的曲线 |

### 父数组组合说明

| 组合 | 描述 |
|------|------|
| `[interval, curve]` | 构造的元素覆盖曲线与 x 轴之间在区间 interval 内的面积 |

## 属性

### 积分点属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `baseLeft` | Point | 积分左端点在 x 轴上的基点属性 |
| `baseRight` | Point | 积分右端点在 x 轴上的基点属性 |
| `curveLeft` | Point | 积分左端点在曲线上的起点属性 |
| `curveRight` | Point | 积分右端点在曲线上的终点属性 |

### 标签属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `label` | Object | 见下方 | 积分标签属性 |

### 标签默认值

```js
{
    fontSize: 20,
    digits: 4,
    intl: {
        enabled: false,
        options: {}
    }
}
```

### 常用曲线属性（继承自 Curve）

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffff00' | 填充颜色 |
| `fillOpacity` | Number | 0.3 | 填充透明度 |
| `strokeWidth` | Number | 1 | 线宽 |
| `visible` | Boolean | true | 是否可见 |

## 字段

| 字段 | 类型 | 描述 |
|------|------|------|
| `baseLeft` | Point | 初始对应区间下限值在 x 轴上的点 |
| `baseRight` | Point | 初始对应区间上限值在 x 轴上的点 |
| `curveLeft` | Glider | 对应区间下限值在曲线上的滑点 |
| `curveRight` | Glider | 对应区间上限值在曲线上的滑点 |

## 方法

| 方法 | 参数 | 描述 | 返回值 |
|------|------|------|--------|
| `Value()` | 无 | 获取积分的当前值 | Number |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `Value(integral)` | 获取积分值 | `Value(i)` |

## 示例

### 1. 创建基本积分区域

```js
// 创建函数图像
c1 = functiongraph(function(t) { return cos(t) * t; });

// 创建积分区域，区间 [-2, 2]
i1 = integral([-2.0, 2.0], c1);
```

### 2. 设置积分区域样式

```js
// 创建函数
f = functiongraph(function(t) { return t * t; });

// 黄色半透明填充
i1 = integral([0, 3], f) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 蓝色边框
i2 = integral([0, 2], f) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 3. 获取积分值

```js
// 创建函数和积分
c = functiongraph(function(t) { return t * t; });
i = integral([0, 3], c);

// 获取积分值
area = Value(i);  // 9

// 在文本中显示
txt = text(1, 1, function() {
    return "面积：" + Value(i);
});
```

### 4. 动态积分区间

```js
// 创建滑块控制积分区间
a = slider(-3, 0, 0.1);
b = slider(0, 3, 0.1);

// 创建函数
c = functiongraph(function(t) { return t * t; });

// 积分区间随滑块变化
i = integral(function() { return [V(a), V(b)]; }, c);
```

### 5. 带标签的积分

```js
// 创建函数和积分，显示面积值
c = functiongraph(function(t) { return sin(t); });
i = integral([0, PI], c) <<
    label: <<
        fontSize: 16,
        digits: 4
    >>
>>;
```

### 6. 多个积分区域比较

```js
// 创建函数
f = functiongraph(function(t) { return t * t; });

// 不同区间的积分
i1 = integral([0, 1], f) << fillColor: 'red', fillOpacity: 0.3 >>;
i2 = integral([1, 2], f) << fillColor: 'green', fillOpacity: 0.3 >>;
i3 = integral([2, 3], f) << fillColor: 'blue', fillOpacity: 0.3 >>;

// 显示各区域面积
txt1 = text(0.5, 0.5, function() { return "A1: " + Value(i1); });
txt2 = text(1.5, 2, function() { return "A2: " + Value(i2); });
txt3 = text(2.5, 5, function() { return "A3: " + Value(i3); });
```

### 7. 负值区域积分

```js
// 创建有正负值的函数
c = functiongraph(function(t) { return sin(t); });

// 积分区间跨越 x 轴
i = integral([0, 2 * PI], c) <<
    fillColor: 'yellow',
    fillOpacity: 0.4
>>;

// 注意：Value(i) 返回代数面积（负区域减去）
```

### 8. 参数曲线积分

```js
// 创建参数曲线
c = curve(function(t) { return t; },
          function(t) { return t * t; },
          [0, 3]);

// 创建积分
i = integral([0, 3], c);
```

## 注意事项

1. **积分区间**：积分区间可以是固定数组 `[a, b]` 或返回数组的函数
2. **代数面积**：积分值计算的是代数面积，x 轴下方的区域为负值
3. **曲线类型**：可以用于 `functiongraph`、`curve` 等曲线类型
4. **基点和曲线点**：`baseLeft/Right` 是 x 轴上的点，`curveLeft/Right` 是曲线上的滑点
5. **标签格式化**：使用 `label.digits` 控制显示的小数位数
6. **国际化**：可通过 `label.intl.enabled: true` 启用国际化数字格式

## 相关元素

- [Curve](./Curve.md) - 曲线
- [Functiongraph](./Functiongraph.md) - 函数图像
- [Area](./Area.md) - 面积
- [Riemannsum](./Riemannsum.md) - 黎曼和
- [Text](./Text.md) - 文本
