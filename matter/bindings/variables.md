<h2 style="margin:0; line-height:1.1;">Defining variables</h2>

Variables do not require `local` in Kuiper and therefore are implicitly local. Global variables can be set through the `_G` environment, but [are not recommended for most purposes](https://wiki.c2.com/?GlobalVariablesConsideredHarmful). Variables are **lexically scoped**, variables declared within a `do .. end` block or identical structure will only be accessible within that block. 

```lua
do
  x = 42 --Implicit `local`
end

print x --Outputs `nil`: variable is out of scope and released
```
When transpiling with existing Lua code, Kuiper will assume all top-level assignments are **local by default**. There may be interoperability issues with legacy code using global variables.

**Variables** may include **optional type annotations** with named types or inline expressions, with `:` introducing the type.

```lua
age: int = 27
total: float = 12.34
phone_numbers: {string} = {"555-6789", "123-4567"}
``` 