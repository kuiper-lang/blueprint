<h2 style="margin:0; line-height:1.1;">Assigning default values to types</h2>

**Default values** in Kuiper for `type`s are set through **overriding** the **default constructor** for the `type` to provide default arguments.

```lua
--New record-like `type`: Person.
type Person = {
    age:  int,
    name: string
}

-- Constructors w/ matching names will instantiate the `Type`.
--`function`s associated with a `type` through `for (t: Type)`
-- will return the instance implicitly unless specified otherwise.
function Person(age: int = 0, 
  name: string = "Unknown") for (p: Person)
    p.age  = age
    p.name = name
end

--Instantiate: `Person` with `age` of 42.
newUser = Person(age=42)

--Output: values of properties - no parentheses needed
print newUser.age --Outputs: 42
print newUser.name --Outputs: Unknown
```

**Default methods** are created through composition with a trait-type with prior implementations through `function .. for`.