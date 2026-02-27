# Group 组

## 描述

组是一个容器元素，用于同时控制一组点、图像或文本元素的移动。组的元素及其依赖元素可以通过拖动其中一个组元素来进行平移、旋转和缩放。

*定义于：* [group.js](./src/src_base_group.js.md)
*继承自：* [JXG.Group](./JXG.Group.md)

## 继承关系

**[JXG.Group](./JXG.Group.md)**
      ↳ **Group**

## JessieCode 语法

```js
// 创建组 - 使用 board.create 方法
// 语法：board.create('group', [点数组], {属性})

// 基本用法 - 创建包含多个点的组
var p = [];
p.push(board.create('point', [-2, -1], {size: 5, strokeColor: 'blue', fillColor: 'blue'}));
p.push(board.create('point', [2, -1], {size: 5, strokeColor: 'blue', fillColor: 'blue'}));
p.push(board.create('point', [2, 1], {size: 5, strokeColor: 'blue', fillColor: 'blue'}));
p.push(board.create('point', [-2, 1], {size: 5, strokeColor: 'blue', fillColor: 'blue'}));
g = board.create('group', p);

// 带旋转功能的组
g = board.create('group', p)
    .setRotationCenter('centroid')
    .setRotationPoints([p[1], p[2]]);

// 带缩放功能的组
g = board.create('group', p)
    .setScaleCenter(p[0])
    .setScalePoints(p[1]);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| board | JXG.Board | 包含这些点的画板 |
| parents | Array | 要分组的点数组 |
| attributes | Object | 视觉属性（未使用） |

## 方法

### 旋转相关方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `setRotationCenter(center)` | center: Point/Array/String/Function | 设置旋转中心 |
| `setRotationPoints(points)` | points: Array | 设置触发旋转的点 |

### 缩放相关方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `setScaleCenter(center)` | center: Point/Array | 设置缩放中心 |
| `setScalePoints(points)` | points: Array | 设置触发缩放的点 |

### 平移相关方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `removeTranslationPoint(point)` | point: Point | 移除触发平移的点 |

### 旋转中心参数说明

| 输入值 | 描述 |
|--------|------|
| Point | 任意点作为旋转中心 |
| Array | 坐标数组，如 `[x, y]` |
| Function | 返回坐标数组的函数 |
| `'centroid'` | 使用预定义字符串 'centroid' 表示质心 |

## 示例

### 1. 创建基本组

```js
// 创建一些自由点
var p, col, g;
col = 'blue';
p = [];
p.push(board.create('point', [-2, -1], {size: 5, strokeColor: col, fillColor: col}));
p.push(board.create('point', [2, -1], {size: 5, strokeColor: col, fillColor: col}));
p.push(board.create('point', [2, 1], {size: 5, strokeColor: col, fillColor: col}));
p.push(board.create('point', [-2, 1], {size: 5, strokeColor: col, fillColor: col}));

// 创建组
g = board.create('group', p);
```

### 2. 组与多边形结合

```js
// 如果点定义了多边形且多边形属性 hasInnerPoints: true
// 多边形可以被拖动
var p, col, pol, g;
col = 'blue';
p = [];
p.push(board.create('point', [-2, -1], {size: 5, strokeColor: col, fillColor: col}));
p.push(board.create('point', [2, -1], {size: 5, strokeColor: col, fillColor: col}));
p.push(board.create('point', [2, 1], {size: 5, strokeColor: col, fillColor: col}));
p.push(board.create('point', [-2, 1], {size: 5, strokeColor: col, fillColor: col}));

pol = board.create('polygon', p, {hasInnerPoints: true});
g = board.create('group', p);
```

### 3. 允许旋转的组

```js
// 定义旋转中心并将组的点声明为"旋转点"
var p, col, pol, g;
col = 'blue';
p = [];
p.push(board.create('point', [-2, -1], {size: 5, strokeColor: col, fillColor: col}));
p.push(board.create('point', [2, -1], {size: 5, strokeColor: 'red', fillColor: 'red'}));
p.push(board.create('point', [2, 1], {size: 5, strokeColor: 'red', fillColor: 'red'}));
p.push(board.create('point', [-2, 1], {size: 5, strokeColor: col, fillColor: col}));

pol = board.create('polygon', p, {hasInnerPoints: true});
g = board.create('group', p);
g.setRotationCenter(p[0]);
g.setRotationPoints([p[1], p[2]]);
```

### 4. 使用质心作为旋转中心

```js
// 旋转中心可以是任意点、坐标数组、返回坐标数组的函数
// 或使用预定义字符串 'centroid'
// 设置旋转点的方法可以链式调用

var p, col, pol, g;
col = 'blue';
p = [];
p.push(board.create('point', [-2, -1], {size: 5, strokeColor: col, fillColor: col}));
p.push(board.create('point', [2, -1], {size: 5, strokeColor: 'red', fillColor: 'red'}));
p.push(board.create('point', [2, 1], {size: 5, strokeColor: 'red', fillColor: 'red'}));
p.push(board.create('point', [-2, 1], {size: 5, strokeColor: col, fillColor: col}));

pol = board.create('polygon', p, {hasInnerPoints: true});
g = board.create('group', p)
    .setRotationCenter('centroid')
    .setRotationPoints([p[1], p[2]]);
```

### 5. 允许缩放的组

```js
// 与旋转类似，可以声明组的点来触发缩放操作
// 需要定义 scaleCenter，类似于旋转

// 在此示例中，黄色点启用缩放，红色点启用旋转
var p, col, pol, g;
col = 'blue';
p = [];
p.push(board.create('point', [-2, -1], {size: 5, strokeColor: col, fillColor: col}));
p.push(board.create('point', [2, -1], {size: 5, strokeColor: 'yellow', fillColor: 'yellow'}));
p.push(board.create('point', [2, 1], {size: 5, strokeColor: 'red', fillColor: 'red'}));
p.push(board.create('point', [-2, 1], {size: 5, strokeColor: col, fillColor: col}));

pol = board.create('polygon', p, {hasInnerPoints: true});
g = board.create('group', p)
    .setRotationCenter('centroid')
    .setRotationPoints([p[2]]);
g.setScaleCenter(p[0])
 .setScalePoints(p[1]);
```

### 6. 控制平移功能

```js
// 默认情况下，组的每个点都会触发平移
// 但有些情况下可能不需要这样

// 在此示例中，点 E 不触发任何操作，但它本身是旋转中心
// 当其他点移动时，它会被平移
var p, q, col, pol, g;
col = 'blue';
p = [];
p.push(board.create('point', [-2, -1], {size: 5, strokeColor: col, fillColor: col}));
p.push(board.create('point', [2, -1], {size: 5, strokeColor: 'yellow', fillColor: 'yellow'}));
p.push(board.create('point', [2, 1], {size: 5, strokeColor: 'red', fillColor: 'red'}));
p.push(board.create('point', [-2, 1], {size: 5, strokeColor: col, fillColor: col}));
q = board.create('point', [0, 0], {size: 5, strokeColor: col, fillColor: col});

pol = board.create('polygon', p, {hasInnerPoints: true});
g = board.create('group', p.concat(q))
    .setRotationCenter('centroid')
    .setRotationPoints([p[2]]);
g.setScaleCenter(p[0])
 .setScalePoints(p[1]);
g.removeTranslationPoint(q);
```

### 7. 组与图像结合

```js
// 添加图像并使用组工具进行操作
var urlImg = "https://jsxgraph.org/distrib/images/uccellino.jpg";
var lowleft = [-2, -1];

var col = 'blue';
var p = [];
p.push(board.create('point', lowleft, {size: 5, strokeColor: col, fillColor: col}));
p.push(board.create('point', [2, -1], {size: 5, strokeColor: 'yellow', fillColor: 'yellow', name: 'scale'}));
p.push(board.create('point', [2, 1], {size: 5, strokeColor: 'red', fillColor: 'red', name: 'rotate'}));
p.push(board.create('point', [-2, 1], {size: 5, strokeColor: col, fillColor: col, name: 'translate'}));

var im = board.create('image', [urlImg, lowleft, [2, 2]]);
var pol = board.create('polygon', p, {hasInnerPoints: true});

var g = board.create('group', p.concat(im));
// g.addPoint(im)   // 添加图像，但作为点处理

g.setRotationCenter(lowleft)
 .setRotationPoints([p[2]]);

g.setScaleCenter(p[0])
 .setScalePoints(p[1]);
```

## 注意事项

1. **组容器**：组本身没有构造函数，必须通过 `board.create('group', ...)` 创建
2. **支持的元素类型**：组可以包含点、图像和文本元素
3. **变换操作**：组支持三种变换操作：平移、旋转、缩放
4. **旋转中心**：可以是点、坐标数组、函数或特殊字符串 'centroid'（质心）
5. **属性设置**：组元素的视觉属性通过其包含的各个元素分别设置
6. **方法链式调用**：`setRotationCenter`、`setRotationPoints`、`setScaleCenter`、`setScalePoints` 等方法支持链式调用
7. **平移控制**：使用 `removeTranslationPoint` 可以移除某个点的平移触发功能

## 相关元素

- [Point](./Point.md) - 点
- [Image](./Image.md) - 图像
- [Text](./Text.md) - 文本
- [Polygon](./Polygon.md) - 多边形
- [Transform](./Transform.md) - 变换
