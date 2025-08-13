<h2 style="margin:0; line-height:1.1;">Implementing methods, metatables to types</h2>

**Methods** are associated with `type`s via the `function ... for` syntax, which binds a function as a method to instances of that type. These methods function through the instance being passed implicitly as the receiver.

```lua
--New record-like `type`: User
type User = {
  userId:   int,
  userName: string
}

--Associate `function`: `logOut()` with `User` (short-hand function)
logOut() for (u: User) = print %"Logged out: {u.userName}"

--Instantiate: `User` with `userId` of 1, `userName` of "admin"
newUser = User(userId=1,
  userName = "admin")

--Outputs: Logged out: admin
newUser:logOut()
```

This type has no **metatable** implementation, which can be created like so:

```lua
--New record-like `type`: User
type User = {
  userId:   int,
  userName: string
}

--Associate `meta`: with `User`
meta for (u: User) = {
  --Implicit return: User(userId=..., userName=...)
  __tostring = () do
    %"User(userId={u.userId}, userName={u.userName})"
  end
}

--Associate `function`: `logOut()` with `User` (short-hand function)
logOut() for (u: User) = print %"Logged out: {u.userName}"

--Instantiate: `User` with `userId` of 1, `userName` of "admin"
newUser = User(userId=1,
  userName = "admin")

--Outputs: User(userId=1, userName="admin")
print tostring(newUser)
```

**Methods** cannot be defined on non-record-like types, but can be emulated through `meta for` structures.
