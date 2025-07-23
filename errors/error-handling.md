### Sample code
Pretty easy & type-driven error handling, similar to Rust/Elixir error handling with a Lua syntax derivation.

```lua
--[[
Native types, accessible in standard namespace.

type Success<T> {value: T} 
type Error {message: string}
type Result<T> Success<T> | Error

Custom error types can be defined:
]]
type DivideByZeroError Error
-- Not an alias, implicit _tag field carries the type name and inserted at transpilation
-- Nominal typing vs structured typing allows for type-aware matching with easy custom error handling

function divide(x: int, y: int): Result<int>
    if y == 0 then
        (DivideByZeroError) {message = "Divisors cannot be zero."} -- Implicit return
        -- Linear precedence on casting only works when the value is atomic
        -- Must be explicitly structured for casting tables
    end
    (Success) x/y -- Implicit return
    -- Linear precedence can be used here, x/y yields a int - an atomic/scalar value
end

match (Result<int>) divide(100, 0)
    when Success           {value}    then print("Value: ", value)
    when DivideByZeroError {message}  then print("Error: ", message)
    when _                 {message}  then print("Unknown error: ", message)
end 
```