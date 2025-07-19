# OOP-style programming in Luz
Lua has metatables in order to implement object-oriented style programming in your code. However, invoking setmetatable with a table and associated metatable increases boilerplate in your program.

### Changes to metatabling:
```lua
meta Vector2
    var x: int
    var y: int

    function _add(self, other)
        self.x += other.x
        self.y += other.y
    end

    function constructor(self, other) --equivalent to __call metamethod 
    end
end

var new_vec = Vector2(1, 2)
```

### Struct-esque type definitions with `type`:
```
type Address = {street: string, zipcode: string}
```