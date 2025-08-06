<h2 style="margin:0; line-height:1.1;">Composing multiple types</h2>

Multiple types can be composed via intersections through the `&` operator. This is analogous to composing traits and structs in other languages.

```lua
--New interface-like `type`: Animal
type Animal = {
    species: string,
    eat:     () -> void,
    sleep:   () -> void
}
--Associate `function`s: `eat` and `sleep` for `Animal` via short-hand function syntax
eat() for (a: Animal) = print %"{a.species} is eating"
sleep() for (a: Animal) = print %"{a.species} is sleeping"

--Compose: Animal `type` with inline interface type expression
type Amphibian = Animal & { swim: (distance: int) -> void }

--Associate `function`: `swim` for `Amphibian` via short-hand function syntax
swim(distance: int) for (a: Amphibian) = print %"{a.species} is swimming for {distance} meters"

--Instantiate: `Amphibian` with `species` of R. temporaria
frog = Amphibian (species="R. temporaria")

frog.swim(100) --Outputs: R. temporaria is swimming for 100 meters
frog.sleep() --Outputs: R. temporaria is sleeping

print frog.species --Outputs: R. temporaria
```