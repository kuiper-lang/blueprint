<h2 style="margin:0; line-height:1.1;">Encapsulating data in Kuiper </h2>

*"OOPs, I did it again..."*

```lua
--trait 
type Ops   = { 
    translate(dx: int, dy: int) -> Self,
    scale(factor: int) -> Self 
}

type Point = { 
    x: int, 
    y: int 
} & Ops

-- assoc wrapper as metatable for types
meta for (p: Point) = {__tostring() = %"Point({p.x}, {p.y})"}

-- assoc methods
-- if not stated, associative methods return Self implicitly
function translate(dx: int, dy: int) for (p: Point)
    p.x += dx
    p.y += dy
end

function scale(factor: int) for (p: Point)
    p.x *= factor
    p.y *= factor
end

-- instantiate table with type `Point`
loc = Point {x = 1, y = 2}

loc
    |> .translate(2, 1)
    |> .scale(2)
    |> print 

```