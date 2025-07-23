# 🛠️ Extending the table in Luz

### Why keep the table?
Using a single, uniform data structure preserves minimalism in a language where simplicity is essential, while reducing cognitive load. This enables programmers to focus on the *logic* of a program rather then the syntax of the language or multiple data structures.

### Inclusion of syntax sugar for data structures
Although all data structures will be implemented as tables, adding specialised constructors such as `array()`, `dict()`, and `tuple()` empower programmers to write clearer and more expressive code. These constructors will enforce the semantics and rules for their respective structures while providing useful helper methods (i.e. .keys(), .filter(), .map()).

### Sample code
```lua
fruit = array('orange', 'banana', 'pineapple', 'apple') --evaluates to: tagged table w/ zero-based indexing, array-like semantics

print(fruit[0]) --zero-based indexing, in arrays only
```

```lua
data = tuple('John', 42, 'Cupertino') --evaluates to: local data = {'John', 42, 'Cupertino'}

(name, age, location) = data--evaluates to: local name, age, location= table.unpack(data)
```