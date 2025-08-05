<h2 style="margin:0; line-height:1.1;">Arrays</h2>

Arrays in Kuiper are constructed using a general constructor which establishs general rules for arrays in other languages.
```lua
Array<T>(tbl : {T}): Array<T>
```
> Returns a `Array<T>` table, where `T` is the element type. Elements are ordered and indexed consecutively starting from zero.

-----
<h4 style="margin:0; line-height:2.0;">Examples</h4>

```lua
nums = Array<int> {1, 2, 3, 4} 
--This is a `function` call to the constructor for `Array<T>`
```

