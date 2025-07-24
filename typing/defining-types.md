<h2 style="margin:0; line-height:1.1;">📦 Crafting Types in Luz</h2>

*"Definitely my type!"*

Similar to **TypeScript** and **Luau**, Luz provides a simple syntax for custom type definitions. Luz enables a **nominal & gradual** typing system to enable better tooling, opt-in type safety, and enable rich error handling. 

Luz also provides primitive subtype distinctions derived from `string`: `char` and `number`: `float` & `int` for semantic clarity.



| 💡 Luz syntax                         | 🛠️ Semantics                                                                 |
|:--------------------------------------|:------------------------------------------------------------------------------|
|`type (typeName) (description)`        | Base syntax for a **custom type**                                             |
|`type Vector2 {x: int, y: int}`        | Defines a nominal **struct** type, **faux instantiation** through annotations |
|`type Error {message: string, id: int}`| Identical to above, varying data types in **struct** types permitted.         |
|`type Char string`                     | Nominal **type** for a 1-byte Unicode character scalar. Distinct from `string`    |
|`type List<T> { T }`                   | **Generic** parameterised type for a list of values of type `T`               |
|`type Success<T> { value: T }`         | **Generic** parameterised type, variant of `Result<T>` in namespace.          |
|`type Error { message: string }`       | **Basic** error type                                                          |
|`type Result Success<T> \| Error`      | **Union** of types `Success<T>` and `Error` - value can be of either type     |
|`type UserData Address & ContactInfo`  | **Intersection** of types `Address` and `ContactInfo`.                        |
|`type Data Address & { name: string }` | **Intersection** of type `Address` and a new **record literal**               |
|`type
-------------------------------------------------------------------------------------------------------------------------

➤ `type` vs `type alias` 