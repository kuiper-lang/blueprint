<h2 style="margin:0; line-height:1.1;">Typing system</h2>

**Kuiper** implements a gradual, primarily structural typing system with a rich spread of features, including:

- Primitive, composite types
- Generic types, parameterisation
- Inference and annotation with types
- Type checking, error handling
- Nominal typing via `Unique<T>`
- ADT-like syntax

**Types** form the foundation of the **object model** through:

- Types as blueprints for tables (record-like)
- Metatyping (typing with associated metatables via `meta for...`)
- Associated methods via `function... for`
- Supporting polymorphism, encapsulation/access control
- Composition with intersections
- Enums, default values