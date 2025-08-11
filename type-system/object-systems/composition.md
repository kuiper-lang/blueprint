<h2 style="margin:0; line-height:1.1;">Composing multiple types</h2>

Types can be composed in multiple ways:

- via **nesting**
```lua
--New struct-like `type`: Review
type Review = {
  author:  string,
  body:    string,
  rating:  int
}
--New struct-like `type`: Restaurant, with an embedded type
type Restaurant = {
  cuisine:       string,
  name:          string,
  address:       string,
  criticReview:  Review
}

--Constructor: ensures `rating` lies between 1-5.
function Review(author: string, body: string, rating: int) for (r: Review)
  assert(rating == 1..=5, "rating needs to be between 1-5 stars!")

  r.author = author
  r.body = body
  r.rating = rating

  --`function.. for` returns a new instance implicitly
end

--Instantiate `Restaurant` with ...
newBusiness = Restaurant(
  cuisine       = "italian", 
  name          = "Pizza Planet",
  address       = "42 Oort Cloud",
  criticReview  = Review("Ms Kuiper", "Excellent!", 5)
)

print newBusiness.criticReview.body --Outputs: Excellent!
```
----
- via **intersections** through the `&` operator.

```lua
--New interface-like `type`: Animal
type Animal = {
  species:  string, 
  eat:      () -> void,
  sleep:    () -> void
}
--Associate `function`s: `eat` and `sleep` for `Animal` via short-hand function syntax
eat() for (a: Animal) = print %"{a.species} is eating"
sleep() for (a: Animal) = print %"{a.species} is sleeping"

--Compose: Animal `type` with inline interface type expression
type Amphibian = Animal & {
  swim: (distance: int) -> void 
}

--Associate `function`: `swim` for `Amphibian` via short-hand function syntax
swim(distance: int) for (a: Amphibian) = print %"{a.species} is swimming for {distance} meters"

--Instantiate: `Amphibian` with `species` of R. temporaria
frog = Amphibian (species="R. temporaria")

frog:swim(100) --Outputs: R. temporaria is swimming for 100 meters
frog:sleep() --Outputs: R. temporaria is sleeping

print frog.species --Outputs: R. temporaria
```