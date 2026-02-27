---
name: jessiecode-writer
description: >-
  Generate JessieCode code for creating interactive geometric constructions
  and mathematical function graphs using JSXGraph. Use when users need to:
  (1) create geometric figures (triangles, circles, polygons),
  (2) plot 2D/3D function graphs,
  (3) demonstrate mathematical concepts visually,
  (4) generate dynamic constructions with sliders or animations.
---

# JessieCode Writer

## Overview

This skill generates JessieCode script code for creating interactive geometric constructions and mathematical visualizations using the JSXGraph library.

## When to Use This Skill

Invoke this skill when users request:

- **Geometric constructions**: Points, lines, circles, polygons, angles, perpendiculars, parallels, etc.
- **Function graphs**: 2D or 3D plots of mathematical functions
- **Mathematical demonstrations**: Euler line, triangle centers (circumcenter, incenter, centroid, orthocenter), etc.
- **Dynamic visualizations**: Constructions with sliders, animations, or interactive elements
- **Code modification**: Edit or extend existing JessieCode code

## Code Generation Workflow

### Step 1: Understand the Request

Identify:
- **Graphic type**: Geometric figure, function graph, or 3D visualization
- **Key elements**: Points, lines, circles, polygons, functions, etc.
- **Constraints**: Relationships (perpendicular, parallel, tangent, etc.)
- **Style requirements**: Colors, line widths, labels, etc.

### Step 2: Plan the Code Structure

```jessiecode
// 1. Configuration (optional frontmatter)
---
boundingBox: [-5, 5, 5, -5]
axis: false
grid: true
---

// 2. Style definitions (optional)
redStyle = << strokeColor: 'red', strokeWidth: 2 >>;

// 3. Base elements (points, sliders)
A = point(-2, -1);
B = point(2, -1);

// 4. Derived elements (lines, circles, polygons)
segment(A, B);
circumcircle(A, B, C);

// 5. Labels and annotations
text(0, 0, "Triangle ABC");
```

### Step 3: Generate the Code

Follow these principles:

1. **Syntax correctness**: Use `<< >>` for objects (not `{}`), proper function calls
2. **Clear structure**: Group related elements, use comments
3. **Visual appeal**: Appropriate colors, line widths, transparency
4. **Dynamic features**: Use sliders for interactive elements when appropriate

### Step 4: Verify the Output

Check:
- [ ] Syntax is valid (especially `<< >>` for attributes)
- [ ] Element references are correct
- [ ] Attributes are properly set
- [ ] Code has necessary comments
- [ ] Geometry renders correctly

## Syntax Quick Reference

For detailed syntax rules, see [references/grammar.md](references/grammar.md).

### Data Types

```jessiecode
// Booleans (case-insensitive)
flag = true;

// Strings (single quotes)
label = 'Hello World';

// Numbers
x = 3.14159;

// Objects (use << >> not {})
style = << strokeColor: 'red', size: 5 >>;

// Functions
f = function(x) { return x * x; };
```

### Operators

```jessiecode
// Arithmetic: +, -, *, /, %, ^ (power)
// Comparison: ==, !=, <, >, <=, >=, ~= (approximately equal)
// Logic: &&, ||, !
// Ternary: condition ? expr1 : expr2
```

### Element Creation

```jessiecode
// Basic elements
A = point(1, 2);
l = line(A, B);
s = segment(A, B);
c = circle(O, A);  // center O, through A
p = polygon(A, B, C);

// With attributes
P = point(1, 2) << strokeColor: 'red', size: 5 >>;

// Geometric constructions
M = midpoint(A, B);
perp = perpendicular(l, P);
para = parallel(l, P);
I = intersection(l1, l2, 0);  // index 0 for first intersection
```

### Control Structures

```jessiecode
// If statement
if (x > 0) {
    // positive
} else {
    // negative
}

// For loop
for (i = 0; i < 10; i = i + 1) {
    // loop body
}

// While loop
while (condition) {
    // loop body
}
```

## API Reference

For detailed element documentation, see [references/api/](references/api/).

### Common Elements

| Element | Function | Example |
|---------|----------|---------|
| Point | `point(x, y)` | `A = point(1, 2)` |
| Line | `line(A, B)` | `l = line(A, B)` |
| Segment | `segment(A, B)` | `s = segment(A, B)` |
| Circle | `circle(center, point)` | `c = circle(O, A)` |
| Polygon | `polygon(A, B, C, ...)` | `tri = polygon(A, B, C)` |
| Text | `text(x, y, content)` | `text(0, 0, 'Hello')` |
| Slider | `slider(min, max, step)` | `a = slider(0, 10, 0.1)` |
| Midpoint | `midpoint(A, B)` | `M = midpoint(A, B)` |
| Intersection | `intersection(l1, l2, index)` | `I = intersection(l1, l2, 0)` |

### Common Attributes

```jessiecode
<<
    strokeColor: 'red',      // Line/border color
    fillColor: 'blue',       // Fill color
    strokeWidth: 2,          // Line width
    size: 5,                 // Point size
    name: 'A',               // Label name
    withLabel: true,         // Show label
    opacity: 0.5,            // Transparency (0-1)
    visible: true            // Visibility
>>
```

## Example Gallery

For more examples, see [references/examples/](references/examples/).

### Example 1: Triangle Circumcenter

```jessiecode
---
boundingBox: [-5, 5, 5, -5]
grid: true
---
// Define triangle vertices
A = point(-2, -1) << name: 'A' >>;
B = point(2, -1) << name: 'B' >>;
C = point(0, 2) << name: 'C' >>;
triangle = polygon(A, B, C);

// Construct perpendicular bisectors
pAB = perpendicular(triangle.borders[0], midpoint(A, B));
pBC = perpendicular(triangle.borders[1], midpoint(B, C));

// Circumcenter is the intersection
O = intersection(pAB, pBC) << name: 'O' >>;

// Circumcircle
circ = circle(O, A) << strokeColor: 'blue' >>;
```

### Example 2: Function Graph with Slider

```jessiecode
---
boundingBox: [-5, 5, 5, -5]
axis: true
---
// Slider for parameter
a = slider(-3, 3, 0.1) << name: 'a' >>;

// Function with parameter
f = function(x) { return a * x^2; };

// Graph
graph = functiongraph(f, -5, 5) << strokeColor: 'red' >>;

// Dynamic text
text(-4, 4, "f(x) = " + a + " * x^2");
```

## Common Mistakes to Avoid

### Wrong Object Syntax

```jessiecode
// Wrong: Using {} for objects
A = point(1, 2) { strokeColor: 'red' };

// Correct: Use << >>
A = point(1, 2) << strokeColor: 'red' >>;
```

### Missing Function Parentheses

```jessiecode
// Wrong
A = point 1, 2;

// Correct
A = point(1, 2);
```

### Wrong Property Access

```jessiecode
// Wrong: Using bracket notation
A['strokeColor'] = 'red';

// Correct: Use dot notation
A.strokeColor = 'red';
```

## Resources

- **Grammar**: [references/grammar.md](references/grammar.md) - Complete syntax reference
- **API**: [references/api/](references/api/) - Element documentation (112 elements)
- **Examples**:
  - [references/examples/from-official/](references/examples/from-official/) - 24 official examples
  - [references/examples/from-user/](references/examples/from-user/) - 14 user examples

## Version

v1.0 - Initial release with complete grammar, API docs (112 elements), and 38 examples
