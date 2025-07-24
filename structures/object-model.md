# OOP-style programming in Luz
Lua supports object-oriented programming with metatables & metamethods. The typical method of invoking setmetatable with a table and associated metatable is boilerplate-heavy.

### Changes to metatabling:
Luz implements a `meta` keyword that defines a metatable blueprint which automatically binds itself as its own metatable. This creates a self-referential metatable, enabling objects to derive behaviour from the table itself. The result is class-like behavior through prototypal delegation, without needing explicit and boilerplate-heavy `setmetatable` calls.

Luz supports interoperability with existing Lua code, therefore existing `setmetatable` and `getmetatable` logic is supported, enabling Luz's scalable and expressive nature.
```lua
-- meta variableName prototype (self-referential metatable)
meta Vector2 {
    x: int,
    y: int,

    __add = (self, other) do
        self.x += other.x
        self.y += other.y
        self
    end,
    
    new = (x, y) do
        self.x = x
        self.y = y
        self --Implicit return of `self` 
    end,
}

positionA = Vector2.new(1, 2)
positionB = Vector2.new(3, 4)

positionResult = positionA + positionB
print(positionResult.x, positionResult.y) --Outputs: 4 6
```

### `type` provides struct-like containers:
For plain data containers with no method definitions, Luz enables the programmer to create struct-like containers through a `type` syntax:

```lua
type Address {
    houseNumber: int,
    street: string, 
    zipcode: string
}
```

### `mixin` provides composable method signatures
```lua
mixin ContactMethods {
    call = (self) do
        print %"Calling {self.contact.phone}."
    end
}
```

### Composition vs inheritance
Luz, like Lua, emphasises composition over inheritance for flexibility.
Type-level composition can be achieved with intersections of types:

```lua
type Address {
    houseNumber:  int,
    street:       string, 
    zipcode:      string
}

type ContactInfo {
    email:  string,
    phone:  string
}

-- Create new type definition User and intersect types Address, ContactInfo with a new tabled type which
-- expects name as a string, age as an integer.
type User Address & ContactInfo & {
    name:  string,
    age:   int
}
```

Metatable/mixin composition can be achieved through the `compose` keyword
```lua
--Type definitions for tables passed to User
type Address {
    houseNumber:  int,
    street:       string, 
    zipcode:      string
}

type ContactInfo {
    email:  string,
    phone:  string
}

mixin ContactMethods {
    call = (self) do
        print %"Calling {self.contact.phone}."
    end
}

-- Metatable creation, assign to User variable, composes ContactMethods with new metatable.
meta User {
    with ContactMethods, --Syntactical sugar for composing mixins & metatables together

    name: string,
    age: int,
    address: Address,
    contact: ContactInfo,
    -- Constructor function - special function that returns a new instance of the table/metatable User.
    new = (name: string, age: int, addr: Address, contact: ContactInfo) do
        self.name     = name
        self.age      = age
        self.address  = addr -- Structured composition
        self.contact  = contact
        self-- Implicit return of `self` 
    end
}

--Initialise structs
address: Address = {houseNumber=42, street='A Road', zipcode='ABC1792'}
contactInfo: ContactInfo = {email='john.luz@example.com', phone='288-1782'}

newCustomer = User.new(name='John', age=42, addr=address, contact=contactInfo)
newCustomer:call() -- outputs: Calling 288-1782.
```