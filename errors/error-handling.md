<h2 style="margin:0; line-height:1.1;">⚠️ Error Handling Theory in Luz</h2>

*“I have not failed. I've just found 10,000 ways that won't work.” - Thomas Edison* 

**Luz's error handling** takes major inspiration from **TypeScript** `type` expression syntax, **Rust** `match` patterns, and **Elixir**'s pattern matching and tagged variants for errors and successful actions.

**Luz** uses a `match` statement for pattern matching on `Result<T>` types, allowing you to **destructure** and handle different `Error` or `Success<T>` cases directly in your code. Each `when` clause matches a specific type and binds its fields, making error handling **concise and expressive**.

The types `Success<T>`, `Result<T>`, and `Error` are automatically present in the **default namespace** as they are core types for error handling and can be extended via **`type` definitions**.

`Result<T>` is a **union** - indicative that it can only return a `Success<T>` or `Error` type, making for easy error handling.

```lua
type Success<T> {value: T} 
type Error {message: string}
type Result<T> Success<T> | Error 
```

Other `Error` types can be crafted through **intersections** with other tables with the `&` operator, and the root `Error` type. 

**Luz** does not come with any specialised `Error` types.

<h4 style="margin:0; line-height:2.0;">📝 Sample Code</h4>

**Ex** 1 - Crafting new error types, typecheck/destructuring of tables in match, and handling of errors.
```lua
--Define new nominal type 'DivideByZeroError'
type DivideByZeroError! Error

--Simple divide function with error handling and type annotation.
function divide(x: int, y: int) -> Result<int>
    if y == 0 then
        (DivideByZeroError) {message = "Divisors cannot be zero."}
    end
    (Success) {result = x/y}
end

-- Identification of type, successively then destructure associated sealed table for each type
match divide(100, 0)
    Success            {value}    then print %"Value: {value}"
    DivideByZeroError  {message}  then print %"Error: {message}"
    _                   {message}  then print %"Unknown error: {message}"
end 
```