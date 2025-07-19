# Extending the table in Luz

### Why keep the table?
Using a single, uniform data structure preserves minimalism in a language where simplicity is essential, while reducing cognitive load, enabling programmers to focus on the logic of a program rather then the syntax of the language.

❌ Say no to conflicting over *how* data is organised <br />
✅ Say yes to emphasising logic and abstraction 

### Inclusion of syntax sugar for data structures
Although under the hood, all data structures are implemented as tables, adding specialised constructors such as `array()`, `dict()`, `tuple()`, `list()` empower programmers to write clearer, more expressive code through syntactical sugar.

### Sample code
```lua
var fruit = array('orange', 'banana', 'pineapple', 'apple') --evaluates to: local fruit = {'orange', 'banana', 'pineapple', 'apple'}

print(fruit[0]) --evaluates to: print(fruit[1])
```

```lua
var data = tuple('John', 42, 'Cupertino') --evaluates to: local data = {'John', 42, 'Cupertino'}

var name, age, location = unpack(data)--evaluates to: local name, age, location = table.unpack(data)
```