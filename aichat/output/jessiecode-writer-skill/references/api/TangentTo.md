# TangentTo 切线

## 描述

通过外部点作圆锥曲线或圆的切线。切线是直线的一种特殊形式。

## JessieCode 语法

```js
// 基本语法 - 创建圆锥曲线的切线
t = tangentto(conic, point, number);

// 创建圆的切线
t = tangentto(circle, point, 0);

// 带属性创建
t = tangentto(conic, point, 0) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    dash: 1
>>;

// 创建两条切线
t0 = tangentto(c, p, 0);
t1 = tangentto(c, p, 1);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| conic | Conic/Circle | 圆锥曲线或圆对象 |
| point | Point | 外部点（切线经过的点） |
| number | Number | 切线编号：0 或 1（过圆外一点有两条切线） |

## 属性

### 切线特有属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `polar` | Object | 极线属性配置（切点弦所在直线） |
| `point` | Object | 切点属性配置（切线与圆锥曲线的交点） |

### 继承自直线的常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线，3=点划线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 直线名称 |

### polar 属性（极线）

```js
t = tangentto(c, p, 0) <<
    polar: <<
        visible: true,
        strokeColor: 'gray',
        dash: 2
    >>
>>;
```

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `visible` | Boolean | false | 是否显示极线 |
| `strokeColor` | String | '#000000' | 极线颜色 |
| `dash` | Number | 0 | 极线虚线样式 |

### point 属性（切点）

```js
t = tangentto(c, p, 0) <<
    point: <<
        visible: true,
        size: 4,
        fillColor: 'red'
    >>
>>;
```

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `visible` | Boolean | false | 是否显示切点 |
| `size` | Number | 3 | 切点大小 |
| `fillColor` | String | '#ffffff' | 切点填充颜色 |

## 示例

### 1. 创建圆的切线

```js
// 创建圆（圆心 [3, 0]，半径 4）
c = circle([3, 0], [3, 4]);

// 创建外部点
p = point(0, 6);

// 创建第一条切线
t0 = tangentto(c, p, 0);

// 创建第二条切线
t1 = tangentto(c, p, 1);
```

### 2. 设置切线样式

```js
c = circle([3, 0], [3, 4]);
p = point(0, 6);

// 蓝色实线切线
t0 = tangentto(c, p, 0) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 红色虚线切线
t1 = tangentto(c, p, 1) <<
    strokeColor: 'red',
    dash: 1
>>;
```

### 3. 显示极线和切点

```js
c = circle([3, 0], [3, 4]);
p = point(0, 6);

// 显示极线和切点的切线
t0 = tangentto(c, p, 0) <<
    polar: <<
        visible: true,
        strokeColor: 'gray',
        dash: 2
    >>,
    point: <<
        visible: true,
        size: 4,
        fillColor: 'red'
    >>
>>;

// 第二条切线（简洁显示）
t1 = tangentto(c, p, 1) <<
    strokeColor: 'black'
>>;
```

### 4. 椭圆的切线

```js
// 创建外部点
p = point(0, 6);

// 创建椭圆（由三个点定义）
ell = ellipse([-5, 1], [-2, -1], [-3, 2]);

// 创建两条切线
t0 = tangentto(ell, p, 0);
t1 = tangentto(ell, p, 1);
```

### 5. 完整示例：圆的切线及辅助线

```js
// 设置画板
c = circle([3, 0], [3, 4]);

// 圆外一点
p = point(0, 6) <<
    size: 5,
    fillColor: 'black'
>>;

// 第一条切线（带极线和切点）
t0 = tangentto(c, p, 0) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    polar: <<
        visible: true,
        strokeColor: 'gray',
        dash: 2
    >>,
    point: <<
        visible: true,
        size: 4,
        fillColor: 'red'
    >>,
    withLabel: true,
    name: 't1'
>>;

// 第二条切线
t1 = tangentto(c, p, 1) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    withLabel: true,
    name: 't2'
>>;
```

### 6. 动态切线

```js
// 创建可移动的外部点
p = point(0, 6);

// 创建圆
c = circle([3, 0], [3, 4]);

// 创建切线，当点 p 移动时切线会自动更新
t0 = tangentto(c, p, 0) <<
    strokeColor: 'blue'
>>;
t1 = tangentto(c, p, 1) <<
    strokeColor: 'red'
>>;
```

## 注意事项

1. **两条切线**：过圆外一点有两条切线，使用 `number` 参数（0 或 1）来区分
2. **点的位置**：点必须在圆锥曲线外部才能作切线，否则会抛出异常
3. **极线**：极线是两个切点连线所在的直线，可通过 `polar.visible: true` 显示
4. **切点**：可通过 `point.visible: true` 显示切点位置
5. **适用于多种圆锥曲线**：切线不仅适用于圆，也适用于椭圆、双曲线和抛物线

## 相关元素

- [Circle](./Circle.md) - 圆
- [Conic](./Conic.md) - 圆锥曲线
- [Line](./Line.md) - 直线
- [Point](./Point.md) - 点
- [Polar](./Polar.md) - 极线
