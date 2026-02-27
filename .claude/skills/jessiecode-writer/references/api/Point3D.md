# Point3D 3D 点

<!-- USAGE_FREQUENCY: advanced -->

## 描述

3D 点对象由三个坐标 [x, y, z] 定义，或者由一个返回包含三个数字的数组的函数定义。也可以将所有数字作为返回数字的函数提供。

## JessieCode 语法

```js
// 通过坐标创建 3D 点
P = point3d(x, y, z);

// 通过函数创建 3D 点
Q = point3d(function() { return [x, y, z]; });

// 使用函数创建每个坐标
R = point3d(function() { return A.X(); }, function() { return A.Y(); }, function() { return A.Z(); });

// 带属性创建
P = point3d(1, 2, 3) <<
    strokeColor: 'red',
    size: 5,
    withLabel: true,
    name: 'P'
>>;

// 在 3D 视图中创建点
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);
P = view.create('point3d', [1, 2, 2], << name: 'A', size: 5 >>);
```

## 参数

### 方式一：三个坐标

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number/Function | x 坐标（数字或返回数字的函数） |
| y | Number/Function | y 坐标（数字或返回数字的函数） |
| z | Number/Function | z 坐标（数字或返回数字的函数） |
| slide | GeometryElement3D | （可选）3D 滑动载体元素，点将在该元素上滑动 |

### 方式二：坐标数组

| 参数 | 类型 | 描述 |
|------|------|------|
| F | Array/Function | 长度为 3 的数组 [x, y, z] 或返回该数组的函数 |
| slide | GeometryElement3D | （可选）3D 滑动载体元素 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 点的名称 |
| `visible` | Boolean | true | 是否可见 |
| `fixed` | Boolean | false | 是否固定（不可拖动） |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `X()` | 无 | 获取 x 坐标 |
| `Y()` | 无 | 获取 y 坐标 |
| `Z()` | 无 | 获取 z 坐标 |
| `W()` | 无 | 获取齐次坐标的 w 分量 |
| `setPosition(coords)` | coords: Array | 设置点的位置，格式为 [x, y, z] 或 [w, x, y, z] |

## 示例

### 1. 创建基本 3D 点

```js
// 创建 3D 视图
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);

// 创建固定 3D 点
A = view.create('point3d', [1, 2, 2], << name: 'A', size: 5 >>);

// 创建另一个 3D 点
B = view.create('point3d', [3, 1, 4], << name: 'B' >>);
```

### 2. 使用函数创建动态 3D 点

```js
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);

// 创建一个基准点
P = view.create('point3d', [1, 2, 2], << name: 'P' >>);

// 创建一个点，其坐标依赖于点 P
Q = view.create('point3d', function() {
    return [P.X(), P.Y(), P.Z() - 3];
}, << name: 'Q', size: 3, fixed: true >>);

// 使用箭头函数创建点
R = view.create('point3d', [
    () => P.X() + 3,
    () => P.Y(),
    () => P.Z() - 2
], << name: 'R', size: 3, fixed: true >>);
```

### 3. 在球面上的滑点

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central',
    xPlaneRear: << fillOpacity: 0.2, gradient: null >>,
    yPlaneRear: << fillOpacity: 0.2, gradient: null >>,
    zPlaneRear: << fillOpacity: 0.2, gradient: null >>
>>);

// 球心
center = view.create('point3d', [0, 0, 0], << withLabel: false, size: 2 >>);

// 球面上一点（定义半径）
point = view.create('point3d', [2, 0, 0], << withLabel: false, size: 2 >>);

// 创建球面
sphere = view.create('sphere3d', [center, point], << fillOpacity: 0.8 >>);

// 在球面上滑动的点
glide = view.create('point3d', [2, 2, 0, sphere], <<
    withLabel: false,
    color: 'red',
    size: 4
>>);

// 连接滑点和球心的线
l1 = view.create('line3d', [glide, center], << strokeWidth: 2, dash: 2 >>);
```

### 4. 访问 3D 点的坐标

```js
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);

P = view.create('point3d', [1, 2, 3], << name: 'P' >>);

// 获取坐标
x = P.X();  // 1
y = P.Y();  // 2
z = P.Z();  // 3
w = P.W();  // 1（有限点的齐次坐标 w=1）
```

### 5. 设置点的位置

```js
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);

P = view.create('point3d', [0, 0, 0], << name: 'P' >>);

// 使用 setPosition 方法设置位置
P.setPosition([1, 3, 4]);

// 也可以使用齐次坐标
P.setPosition([1, 2, 3, 4]);  // [w, x, y, z]
```

### 6. 在 3D 直线上的滑点

```js
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);

// 创建 3D 直线
A = view.create('point3d', [0, 0, 0]);
B = view.create('point3d', [3, 3, 3]);
line = view.create('line3d', [A, B]);

// 创建在直线上滑动的点
P = view.create('point3d', [1, 1, 1, line], <<
    name: 'P',
    size: 5,
    color: 'red'
>>);
```

## 注意事项

1. **齐次坐标**：3D 点内部使用齐次坐标 [w, x, y, z] 表示，其中 w=1 表示有限点，w=0 表示无穷远点
2. **坐标可以是函数**：点的坐标可以是返回数字的函数，用于创建动态点
3. **滑点功能**：从版本 v1.11 开始，仅支持在 line3d 类型的元素上滑动
4. **3D 视图**：3D 点必须在 3D 视图（view3d）中创建和显示

## 相关元素

- [Line3D](./Line3D.md) - 3D 直线
- [Plane3D](./Plane3D.md) - 3D 平面
- [Sphere3D](./Sphere3D.md) - 3D 球面
- [View3D](./View3D.md) - 3D 视图
