```lua
type State<T> { value: T }

--Linear precedence principle that wraps the atomic value `initial` into the first identified field
--of the `State` table's type, and returns the casted/initialised State table.
function useState(initial: int): State<int>
    (State) initial --implicit return
end

print useState(42) -- { value = 42 }
```