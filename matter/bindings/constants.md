<h2 style="margin:0; line-height:1.1;">Defining constants</h2>

**Constants** are defined via the `const` keyword.
```lua
const (variable-name): (type-expression?) = (value)
```

```lua
--Define new `const`: PI
const PI: int = 3.14

--Outputs: Input the radius:
--Define new variable: radius, takes user input
--`print` in Lua appends \n, we use io.write
io.write "Input the radius: " 
radius: int = io.scan()

--For this final expression, brackets not required but used for readability
print (pi * (radius ^ 2)) 
```