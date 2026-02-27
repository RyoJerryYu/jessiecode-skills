# Polyhedron3D 3D 多面体

<!-- USAGE_FREQUENCY: advanced -->

## 描述

3D 多面体由多个面组成，每个面由顶点定义。多面体需要指定顶点列表和每个面的顶点索引。

## JessieCode 语法

```js
// 通过顶点列表和面列表创建多面体
polyhedron = polyhedron3d(vertices, faces);

// 带属性创建
polyhedron = polyhedron3d(vertices, faces) <<
    fillColorArray: ['blue', 'red', 'yellow'],
    fillOpacity: 0.5,
    strokeWidth: 2
>>;

// 在 3D 视图中创建
view = view3d([-5, -3], [8, 8], [[-4, 4], [-4, 4], [-4, 4]]);
polyhedron = view.create('polyhedron3d', [vertices, faces]);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| vertices | Array | 顶点列表，可以是坐标数组 [x, y, z]、Point3D 元素或函数 |
| faces | Array | 面列表，每个面由顶点索引数组定义，也可以包含面属性 |

### 顶点格式

顶点可以用以下方式定义：
- 坐标数组：`[x, y, z]`
- Point3D 元素引用
- 返回坐标的函数：`() => [x, y, z]`
- 命名对象：`{ a: [x, y, z], b: [x, y, z], ... }`

### 面格式

面可以用以下方式定义：
- 顶点索引数组：`[0, 1, 2, 3]`
- 带属性的数组：`[[0, 1, 2, 3], { fillColor: 'red', fillOpacity: 0.5 }]`
- 使用顶点名称：`['a', 'b', 'c', 'd']`（当顶点使用命名对象时）

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fillColor` | String | 'white' | 默认填充颜色 |
| `fillOpacity` | Number | 0.8 | 填充透明度 |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 1 | 描边宽度 |
| `visible` | Boolean | true | 是否可见 |
| `fillColorArray` | Array | ['white', 'black'] | 循环应用于各面的填充颜色数组 |

### 着色器属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `shader.enabled` | Boolean | false | 是否启用着色器 |
| `shader.type` | String | 'angle' | 着色器类型 |
| `shader.hue` | Number | 60 | 色调 (0-360) |
| `shader.saturation` | Number | 90 | 饱和度 (0-100) |
| `shader.minlightness` | Number | 60 | 最小亮度 (0-100) |
| `shader.maxLightness` | Number | 80 | 最大亮度 (0-100) |

## 字段

| 字段 | 类型 | 描述 |
|------|------|------|
| `faces` | Array | Face3D 对象列表 |
| `def` | Object | 多面体的定义数据，包含顶点定义和每个面的顶点列表 |
| `numberFaces` | Number | 面的数量 |

## 示例

### 1. 创建立方体

```js
box = [-4, 4];
view = view3d([-5, -3], [8, 8], [box, box, box], <<
    projection: 'parallel',
    trackball: << enabled: false >>,
    depthOrder: << enabled: true >>,
    xPlaneRear: << visible: false >>,
    yPlaneRear: << visible: false >>,
    zPlaneRear: << fillOpacity: 0.2 >>
>>);

// 立方体顶点
vertices = [
    [-3, -3, -3],  // 0: 后下左
    [3, -3, -3],   // 1: 后下右
    [3, 3, -3],    // 2: 后上右
    [-3, 3, -3],   // 3: 后上左
    [-3, -3, 3],   // 4: 前下左
    [3, -3, 3],    // 5: 前下右
    [3, 3, 3],     // 6: 前上右
    [-3, 3, 3]     // 7: 前上左
];

// 面（每个面由 4 个顶点索引定义）
faces = [
    [0, 1, 2, 3],  // 后面
    [0, 1, 5, 4],  // 底面
    [[1, 2, 6, 5], << fillColor: 'black', fillOpacity: 0.5, strokeWidth: 5 >>],  // 右面（自定义样式）
    [2, 3, 7, 6],  // 上面
    [3, 0, 4, 7],  // 左面
    [4, 5, 6, 7]   // 前面
];

cube = view.create('polyhedron3d', [vertices, faces], <<
    fillColorArray: ['blue', 'red', 'yellow']
>>);
```

### 2. 使用命名顶点创建立方体

```js
box = [-4, 4];
view = view3d([-5, -3], [8, 8], [box, box, box], <<
    projection: 'parallel',
    trackball: << enabled: false >>,
    depthOrder: << enabled: true >>,
    xPlaneRear: << visible: false >>,
    yPlaneRear: << visible: false >>,
    zPlaneRear: << fillOpacity: 0.2 >>
>>);

// 创建 Point3D 元素作为顶点
aa = view.create('point3d', [-3, -3, -3], << name: 'A', layer: 12 >>);
bb = view.create('point3d', [() => aa.X(), () => aa.Y(), 3], << name: 'B', fixed: true, layer: 12 >>);

// 使用命名对象定义顶点
cube = view.create('polyhedron3d', [
    <<
        a: 'A',
        b: [3, -3, -3],
        c: [3, 3, -3],
        d: [-3, 3, -3],
        e: bb,
        f: [3, -3, 3],
        g: [3, 3, 3],
        h: [-3, 3, 3]
    >>,
    [
        ['a', 'b', 'c', 'd'],  // 后面
        ['a', 'b', 'f', 'e'],  // 底面
        ['b', 'c', 'g', 'f'],  // 右面
        ['c', 'd', 'h', 'g'],  // 上面
        ['d', 'a', 'e', 'h'],  // 左面
        ['e', 'f', 'g', 'h'],  // 前面
        ['a', 'g'],            // 边
        ['f']                  // 顶点
    ]
], <<
    fillColorArray: ['blue', 'red', 'yellow'],
    fillOpacity: 0.4,
    layer: 12
>>);

// 设置特定面的属性
cube.faces[6].setAttribute(<< strokeWidth: 5 >>);
cube.faces[7].setAttribute(<< strokeWidth: 10 >>);
```

### 3. 动态立方体（使用滑块）

```js
box = [-4, 4];
view = view3d([-5, -3], [8, 8], [box, box, box], <<
    projection: 'parallel',
    trackball: << enabled: false >>,
    depthOrder: << enabled: true >>,
    xPlaneRear: << visible: false >>,
    yPlaneRear: << visible: false >>,
    zPlaneRear: << fillOpacity: 0.2 >>
>>);

// 创建滑块控制立方体大小
s = slider([[-4, -6], [4, -6], [0, 2, 4]], << name: 's' >>);

// 使用函数定义动态顶点
cube = view.create('polyhedron3d', [
    [
        () => { let f = V(s); return [-f, -f, -f]; },
        () => { let f = V(s); return [f, -f, -f]; },
        () => { let f = V(s); return [f, f, -f]; },
        () => { let f = V(s); return [-f, f, -f]; },
        () => { let f = V(s); return [-f, -f, f]; },
        () => { let f = V(s); return [f, -f, f]; },
        () => { let f = V(s); return [f, f, f]; },
        [() => -V(s), () => V(s), () => V(s)]
    ],
    [
        [0, 1, 2, 3],
        [0, 1, 5, 4],
        [1, 2, 6, 5],
        [2, 3, 7, 6],
        [3, 0, 4, 7],
        [4, 5, 6, 7]
    ]
], <<
    strokeWidth: 3,
    fillOpacity: 0.6,
    fillColorArray: ['blue', 'red', 'yellow'],
    shader: << enabled: false >>
>>);
```

### 4. 创建正二十面体

```js
box = [-4, 4];
view = view3d([-5, -3], [8, 8], [box, box, box], <<
    projection: 'parallel',
    trackball: << enabled: false >>,
    depthOrder: << enabled: true >>,
    xPlaneRear: << visible: false >>,
    yPlaneRear: << visible: false >>,
    zPlaneRear: << fillOpacity: 0.2 >>
>>);

// 黄金比例
rho = 1.6180339887;

// 12 个顶点
vertexList = [
    [0, -1, -rho], [0, +1, -rho], [0, -1, rho], [0, +1, rho],
    [1, rho, 0], [-1, rho, 0], [1, -rho, 0], [-1, -rho, 0],
    [-rho, 0, 1], [-rho, 0, -1], [rho, 0, 1], [rho, 0, -1]
];

// 20 个三角形面
faceArray = [
    [4, 1, 11], [11, 1, 0], [6, 11, 0], [0, 1, 9],
    [11, 10, 4], [9, 1, 5], [8, 9, 5], [5, 3, 8],
    [6, 10, 11], [2, 3, 10], [2, 10, 6], [8, 3, 2],
    [3, 4, 10], [7, 8, 2], [9, 8, 7], [0, 9, 7],
    [4, 3, 5], [5, 1, 4], [0, 7, 6], [7, 2, 6]
];

// 创建正二十面体
ico = view.create('polyhedron3d', [vertexList, faceArray], <<
    fillColorArray: [],
    fillOpacity: 1,
    strokeWidth: 0.1,
    layer: 12,
    shader: <<
        enabled: true,
        type: 'angle',
        hue: 60,
        saturation: 90,
        minlightness: 60,
        maxLightness: 80
    >>
>>);
```

### 5. 创建四面体

```js
view = view3d([-5, -3], [8, 8], [[-4, 4], [-4, 4], [-4, 4]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

// 四面体的 4 个顶点
vertices = [
    [0, 0, 2],     // 顶点
    [-1.5, -1, -1], // 底面 1
    [1.5, -1, -1],  // 底面 2
    [0, 2, -1]      // 底面 3
];

// 4 个三角形面
faces = [
    [0, 1, 2],  // 前面
    [0, 2, 3],  // 右面
    [0, 3, 1],  // 左面
    [1, 3, 2]   // 底面
];

tetrahedron = view.create('polyhedron3d', [vertices, faces], <<
    fillColorArray: ['red', 'green', 'blue', 'yellow'],
    fillOpacity: 0.7,
    strokeWidth: 2
>>);
```

### 6. 创建八面体

```js
view = view3d([-5, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

// 八面体的 6 个顶点
vertices = [
    [0, 0, 2],   // 上顶点
    [0, 0, -2],  // 下顶点
    [2, 0, 0],   // 右
    [-2, 0, 0],  // 左
    [0, 2, 0],   // 前
    [0, -2, 0]   // 后
];

// 8 个三角形面
faces = [
    [0, 2, 4], [0, 4, 3], [0, 3, 5], [0, 5, 2],  // 上面 4 个
    [1, 4, 2], [1, 3, 4], [1, 5, 3], [1, 2, 5]   // 下面 4 个
];

octahedron = view.create('polyhedron3d', [vertices, faces], <<
    fillColorArray: ['cyan', 'magenta', 'yellow', 'lime'],
    fillOpacity: 0.6,
    strokeWidth: 2
>>);
```

### 7. 使用着色器效果

```js
view = view3d([-5, -3], [8, 8], [[-4, 4], [-4, 4], [-4, 4]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

// 立方体顶点
vertices = [
    [-2, -2, -2], [2, -2, -2], [2, 2, -2], [-2, 2, -2],
    [-2, -2, 2], [2, -2, 2], [2, 2, 2], [-2, 2, 2]
];

faces = [
    [0, 1, 2, 3], [0, 1, 5, 4], [1, 2, 6, 5],
    [2, 3, 7, 6], [3, 0, 4, 7], [4, 5, 6, 7]
];

// 使用角度着色器
cube = view.create('polyhedron3d', [vertices, faces], <<
    fillOpacity: 0.8,
    strokeWidth: 1,
    shader: <<
        enabled: true,
        type: 'angle',
        hue: 120,
        saturation: 80,
        minlightness: 50,
        maxLightness: 70
    >>
>>);
```

## 注意事项

1. **顶点顺序**：面的顶点应按逆时针顺序排列（从外部观察）以确保正确的法线方向
2. **封闭性**：多面体应该是封闭的，所有边应该恰好被两个面共享
3. **颜色循环**：`fillColorArray` 会循环应用于各个面
4. **单个面属性**：可以在面定义中单独设置每个面的属性
5. **3D 视图**：多面体必须在 3D 视图（view3d）中创建和显示
6. **深度排序**：建议启用 `depthOrder: { enabled: true }` 以获得正确的渲染效果
7. **着色器**：着色器可以根据面的角度自动计算颜色，产生更真实的 3D 效果

## 相关元素

- [Point3D](./Point3D.md) - 3D 点
- [Polygon3D](./Polygon3D.md) - 3D 多边形
- [Plane3D](./Plane3D.md) - 3D 平面
- [View3D](./View3D.md) - 3D 视图
- [Sphere3D](./Sphere3D.md) - 3D 球面
