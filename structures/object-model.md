# OOP-style programming in Lua
Lua support object-oriented programming with metatables & metamethods. The typical method of invoking setmetatable with a table and associated metatable is boilerplate-heavy.

### Changes to metatabling:
Luz implements a declarative `meta` block to enable metamethods in tables, enabling tables to be analogous with classes . 

Luz supports interoperability with existing Lua code - so existing `setmetatable` functionality is retained, enabling scalability.
```lua
meta Vector2 {
    var x: int,
    var y: int,

    _add(self, other) do
        self.x += other.x
        self.y += other.y
    end,

    new(self, x, y) do
        self.x = x
        self.y = y
        self --implicit returns
    end,
}

new_vec = Vector2(1, 2)
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
    call(self) do
        telephone:call(self.phone)
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
    call(self) do
        print %"Calling {self.contact.phone}."
    end
}

-- Metatable creation, assign to User variable, composes ContactMethods with new metatable.
meta User 
    with ContactMethods {
    
    name: string,
    age: int,
    address: Address,
    contact: ContactInfo,
    -- Constructor function - special function that returns a new instance of the table/metatable User.
    new(name: string, age: int, addr: Address, contact: ContactInfo) do
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