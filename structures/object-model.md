<h2 style="margin:0; line-height:1.1;">🎁 Object-Oriented Programming in Luz </h2>

*"OOPs, I did it again..."*

> **Background ↴**
>
> **Luz** supports **interoperability** with typical **Lua** - existing `setmetatable` and `getmetatable` logic is allowed
>
> Typical **Lua** supports **object-oriented programming** with **metatables & metamethods**. The typical method of invoking `setmetatable` with a table and associated metatable is **boilerplate-heavy**.

---

In Luz, we implement a `meta` keyword that defines a **metatable blueprint** which automatically **binds** itself as its own metatable. This creates a **self-referential metatable**, enabling objects to **derive behaviour from the table itself**. The result is **class-like** behavior through **prototypal delegation**, without needing explicit and boilerplate-heavy `setmetatable` calls. This is automatically assigned to a specified name.



**Syntax**: `meta (metatable-name) (table)`

---------------


**Luz** also supports `trait`- concepts which define a **set of methods** which can be **composed** using the `with` keyword with **prototypes/self-referential metatables** to extend functionality.

Definition is parallel to `meta` - requires **a name** and a **table with methods with no data fields**.

**Syntax**: `trait (trait-name) (method-table)`

---------------
<h4 style="margin:0; line-height:2.0;">📝 Sample Code with <code>meta</code></h4>

**Ex** 1 - Define a Vector self-ref metatable with additive functionality

```lua
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

---------------------
<h4 style="margin:0; line-height:2.0;">📝 Sample Code with <code>trait</code></h4>

**Ex** 2 - Define a trait with methods for social media users/admins

```lua
trait Social {
    post = (self, body: string) do
        ...
        print %"Posted {body} as {self.name}"
    end
}

```

---------------------
<h4 style="margin:0; line-height:2.0;">📝 Sample Code with <code>with</code></h4>

**Ex** 3 - Compose existing Social trait with a User metatable

```lua

trait Social {
    post = (self, body: string) do
        ...
        print %"Posted {body} as {self.name}"
    end
}

meta User {
    with Social, --syntactical sugar for composing mixins & prototypes together

    name: string,
    userId: int, 

    --reference of self immediately yields instantiation of a new object
    new = (name: string, id: int) do
        self.name     = name
        self.id       = id
        self-- Implicit return of `self` 
    end
}


newCustomer = User.new(name='John', id=42)
newCustomer:call("Hello, world")
--outputs: Posted Hello, world as John
```