# Image 图像

<!-- USAGE_FREQUENCY: common -->

## 描述

图像元素用于在画布上显示外部图片。

## JessieCode 语法

```js
// 基本语法 - 创建图像
img = image(url, [x, y], [width, height]);

// 带属性创建
img = image('picture.jpg', [-3, -2], [3, 3]) <<
    rotate: 45,
    opacity: 0.8
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| url | String/Function | 图片的 URL 地址（字符串或返回字符串的函数） |
| coords | Array | 图像左下角的用户坐标 `[x, y]` |
| size | Array | 图像的宽度和高度（用户坐标）`[width, height]` |

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `opacity` | Number | 1.0 | 透明度（0-1） |
| `visible` | Boolean | true | 是否可见 |
| `fixed` | Boolean | false | 是否固定（不可拖动） |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 元素名称 |
| `id` | String | 自动生成 | 元素的唯一 ID |

### 图像特有属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `cssClass` | String | 'JXGimage' | 图像的 CSS 类名 |
| `highlightCssClass` | String | 'JXGimageHighlight' | 高亮时的 CSS 类名 |
| `rotate` | Number | 0 | 图像旋转角度（度） |
| `snapSizeX` | Number | 1 | 吸附网格的 X 方向间距 |
| `snapSizeY` | Number | 1 | 吸附网格的 Y 方向间距 |
| `attractors` | Array | [] | 吸引元素列表 |
| `attractorDistance` | Number | 0.5 | 吸附距离 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `move(dx, dy)` | dx, dy: Number | 移动图像 |
| `free()` | 无 | 释放图像 |

## 示例

### 1. 创建基本图像

```js
// 从 URL 加载图像
img = image('https://jsxgraph.org/jsxgraph/distrib/images/uccellino.jpg', [-3, -2], [3, 3]);
```

### 2. 设置图像位置和大小

```js
// 左下角坐标 (-3, -2)，宽度 3，高度 3
img1 = image('picture.jpg', [-3, -2], [3, 3]);

// 左下角坐标 (0, 0)，宽度 2，高度 1.5
img2 = image('photo.png', [0, 0], [2, 1.5]);
```

### 3. 旋转图像

```js
// 旋转 45 度
img = image('picture.jpg', [-2, -2], [4, 4]) <<
    rotate: 45
>>;

// 旋转 90 度
img2 = image('photo.png', [0, 0], [2, 2]) <<
    rotate: 90
>>;
```

### 4. 设置透明度

```js
// 半透明图像
img = image('picture.jpg', [-3, -3], [6, 6]) <<
    opacity: 0.5
>>;

// 更透明
img2 = image('photo.png', [0, 0], [3, 3]) <<
    opacity: 0.3
>>;
```

### 5. 固定图像（不可拖动）

```js
// 固定图像位置
img = image('background.jpg', [-5, -5], [10, 10]) <<
    fixed: true
>>;
```

### 6. 图像吸附到网格

```js
// 设置吸附网格
img = image('picture.jpg', [-3, -3], [6, 6]) <<
    snapSizeX: 1,
    snapSizeY: 1
>>;

// 使用更大的吸附间距
img2 = image('photo.png', [0, 0], [4, 4]) <<
    snapSizeX: 2,
    snapSizeY: 2
>>;
```

### 7. 动态图像位置

```js
// 使用函数创建动态位置
A = point(0, 0);
img = image('picture.jpg',
    function() { return A.X() - 1; },
    function() { return A.Y() - 1; },
    [2, 2]);

// 图像跟随点移动
P = point(1, 1);
img2 = image('logo.png',
    function() { return P.X(); },
    function() { return P.Y(); },
    [1, 1]);
```

### 8. 使用滑块控制图像

```js
// 创建滑块控制图像位置
s = slider([1, 4], [4, 4], [-5, 0, 5]) << name: 'x' >>;
img = image('picture.jpg',
    function() { return V(s); },
    0,
    [2, 2]);

// 滑块控制图像大小
sizeSlider = slider([1, 3], [4, 3], [0.5, 2, 5]);
img2 = image('photo.png', [-2, -2],
    function() { return [V(sizeSlider), V(sizeSlider) * 0.75]; });
```

### 9. 多个图像组合

```js
// 创建背景图像
bg = image('background.jpg', [-5, -5], [10, 10]) <<
    fixed: true
>>;

// 创建前景图像
fg = image('foreground.png', [-3, -3], [6, 6]) <<
    opacity: 0.8
>>;
```

### 10. 图像与几何元素交互

```js
// 创建图像
img = image('map.jpg', [-4, -4], [8, 8]);

// 在图像上创建点标记位置
marker = point(0, 0) <<
    strokeColor: 'red',
    fillColor: 'yellow',
    size: 5
>>;

// 标记点的标签
label = text(0.3, 0.3, "标记点") <<
    anchor: marker,
    fontSize: 14
>>;
```

### 11. 动态图像 URL

```js
// 使用函数动态改变图像
toggle = slider([1, 4], [4, 4], [0, 0, 1]) <<
    snapWidth: 1,
    name: 't'
>>;

img = image(function() {
    return V(toggle) > 0.5 ? 'image1.jpg' : 'image2.jpg';
}, [-3, -3], [6, 6]);
```

### 12. 图像作为按钮背景

```js
// 创建小图像作为按钮
btnImg = image('button.png', [1, 1], [1, 1]) <<
    fixed: true
>>;

// 在图像上创建文本
btnText = text(0.5, 0.5, "点击") <<
    anchorX: 'middle',
    anchorY: 'middle',
    anchor: btnImg
>>;
```

## 注意事项

1. **坐标解释**：坐标数组可以包含 2 个元素（2D 仿射坐标）或 3 个元素（齐次坐标）
2. **约束坐标**：坐标可以是数字（自由图像）或函数/字符串（约束图像）
3. **图片格式**：支持常见的图片格式（JPG、PNG、GIF、SVG 等）
4. **跨域问题**：使用外部 URL 时可能遇到跨域限制
5. **性能考虑**：大尺寸图片可能影响渲染性能，建议预先压缩
6. **CSS 类**：`cssClass` 和 `highlightCssClass` 可以覆盖默认的 JSXGraph 样式
7. **吸附功能**：`snapSizeX` 和 `snapSizeY` 设置为 0 或负数时，使用坐标轴的默认刻度网格

## 相关元素

- [Point](./Point.md) - 点
- [Text](./Text.md) - 文本
- [Button](./Button.md) - 按钮
