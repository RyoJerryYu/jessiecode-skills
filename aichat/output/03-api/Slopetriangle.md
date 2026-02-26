# Slopetriangle 斜率三角形

## 描述

斜率三角形用于可视化曲线、圆或直线的切线斜率。

## JessieCode 语法

```js
// 基于切线创建斜率三角形
st = slopetriangle(t);

// 基于直线和直线上的点创建斜率三角形
st = slopetriangle(li, P);

// 带属性创建
st = slopetriangle(t) <<
    baseline: <<
        strokeColor: 'blue',
        dash: 1
    >>,
    label: <<
        withLabel: true,
        name: 'm'
    >>
>>;
```

## 参数

### 方式一：基于切线

| 参数 | 类型 | 描述 |
|------|------|------|
| tangent | Line | 基于曲线上滑点的切线 |

### 方式二：基于直线和点

| 参数 | 类型 | 描述 |
|------|------|------|
| line | Line | 直线 |
| point | Point | 直线上的点（用户需确保点在直线上） |

## 属性

### 子元素属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `baseline` | Line | 基线属性 |
| `basepoint` | Point | 基点属性 |
| `glider` | Point | 滑动辅助点属性 |
| `label` | Label | 斜率三角形标签属性 |
| `tangent` | Line | 切线属性 |
| `toppoint` | Point | 顶点属性 |

### 属性示例

```js
// 自定义基线样式
st = slopetriangle(t) <<
    baseline: <<
        strokeColor: 'blue',
        strokeWidth: 2,
        dash: 1
    >>
>>;

// 自定义基点样式
st = slopetriangle(t) <<
    basepoint: <<
        strokeColor: 'red',
        size: 4
    >>
>>;

// 自定义标签
st = slopetriangle(t) <<
    label: <<
        withLabel: true,
        name: 'm = 2',
        position: 'top'
    >>
>>;
```

## 方法

### 实例方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `Direction()` | 无 | 返回斜率三角形的方向，即切线的方向 |
| `Value()` | 无 | 返回斜率三角形的值，即切线的斜率 |

### 方法示例

```js
// 创建斜率三角形
st = slopetriangle(t);

// 获取斜率值
slope = st.Value();

// 获取方向
dir = st.Direction();
```

## 示例

### 1. 基于曲线切线的斜率三角形

```js
// 创建函数图像
f = plot('sin(x)');

// 创建曲线上的滑点
g = glider(1, 2, f);

// 创建切线
t = tangent(g);

// 创建斜率三角形
st = slopetriangle(t);
```

### 2. 基于直线和点的斜率三角形

```js
// 创建两个点
p1 = point(-2, 3);
p2 = point(2, -3);

// 创建直线
li = line(p1, p2);

// 创建直线上的滑点
p = glider(0, 0, li);

// 创建斜率三角形
st = slopetriangle(li, p);
```

### 3. 自定义样式的斜率三角形

```js
// 创建函数和切线
f = plot('x^2');
g = glider(1, 1, f);
t = tangent(g);

// 创建带样式的斜率三角形
st = slopetriangle(t) <<
    baseline: <<
        strokeColor: '#0066ff',
        strokeWidth: 2,
        dash: 0
    >>,
    basepoint: <<
        strokeColor: '#ff0000',
        fillColor: '#ffffff',
        size: 5
    >>,
    toppoint: <<
        strokeColor: '#00ff00',
        fillColor: '#ffffff',
        size: 5
    >>,
    glider: <<
        visible: false
    >>,
    label: <<
        withLabel: true,
        name: 'm',
        strokeColor: '#000000'
    >>
>>;
```

### 4. 动态斜率三角形

```js
// 创建滑块控制参数
a = slider(-3, 3, 0.1);

// 创建抛物线
f = plot('a*x^2');

// 创建滑点和切线
g = glider(a, V(a)*V(a), f);
t = tangent(g);

// 斜率三角形随滑点移动而更新
st = slopetriangle(t) <<
    label: <<
        withLabel: true,
        name: function() { return 'm = ' + st.Value().toFixed(2); }
    >>
>>;
```

### 5. 获取斜率值

```js
// 创建斜率三角形
f = plot('cos(x)');
g = glider(1, 1, f);
t = tangent(g);
st = slopetriangle(t);

// 获取当前斜率值
slope = st.Value();

// 获取方向
direction = st.Direction();

// 在文本中显示斜率
txt = text(2, 2, function() {
    return '当前斜率：' + st.Value().toFixed(3);
});
```

### 6. 圆上的斜率三角形

```js
// 创建圆
c = circle(point(0, 0), 3);

// 创建圆上的滑点
g = glider(3, 0, c);

// 创建切线
t = tangent(g);

// 创建斜率三角形
st = slopetriangle(t);
```

## 注意事项

1. **切线依赖**：斜率三角形需要一个切线对象，该切线通常基于曲线、圆或直线上的滑点
2. **点在直线上**：当使用直线和点方式创建时，用户需确保点确实在直线上
3. **继承自 Line**：斜率三角形继承自 Line 元素，因此可以使用 Line 的部分属性和方法
4. **动态更新**：当滑点在曲线上移动时，斜率三角形会自动更新以反映新的斜率
5. **标签显示**：可以通过 label 属性配置斜率值的显示

## 相关元素

- [Tangent](./Tangent.md) - 切线
- [Glider](./Glider.md) - 滑点
- [Line](./Line.md) - 直线
- [Point](./Point.md) - 点
- [Plot](./Plot.md) - 函数图像
- [Circle](./Circle.md) - 圆
