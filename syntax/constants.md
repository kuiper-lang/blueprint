<h2 style="margin:0; line-height:1.1;">❌ Immutability in Luz</h2>

*'Change is inevitable...'*

**Luz** is influenced heavily by modern functional languages, i.e. Elixir, which emphasise **zero data mutation** and **variable immutability** by default. This concept was not reflected into Luz's syntax due to emphasis of **speed**, **flexibility** and **ease of use for beginner programmers** over paradigm fidelity.

Immutability of variables can be enforced via the new `const` keyword to empower programmers to adopt functional patterns in code and encourage proper programming etiquette. To differentiate between variables and constants in large production environments, ensure you write constants in **BLOCK CAPITALS** with **SNAKE_CASE** with **:type** annotations.

See: *Luz's official style guide - Best practices*.
<h4 style="margin:0; line-height:2.0;">📝 Sample Code</h4>

**Ex** 1 - Finds area of a circle and outputs to the user
```lua
-- define new constant `PI`
const PI: float = 3.14

--fyi - print appends \n in Luz regardless
io.write "Input the radius: " 
radius: int = io.scan()

print (pi * (radius ^ 2)) 
-- brackets not needed here for final expression, but are used for readability
```

**Ex** 2 - Recursive function that prints retry attempts up to a constant limit

```lua
-- define new constant `MAX_ENTRIES`
const MAX_RETRIES = 5

-- recursive function that prints retry attempts up to MAX_RETRIES
function retry(attempt: int)
    if attempt > MAX_RETRIES then
        print "Giving up."
        return
    end

    print %"Attempt {attempt}: retrying..."
    retry(attempt + 1)
end

-- start retry process
retry(1)
```

**✅ This document provides all knowledge of the concepts of immutability and constancy in Luz.**