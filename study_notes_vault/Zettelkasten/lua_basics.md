---
aliases:
tags:
references:
  - "[[Lua]]"
date: 10-30-2025
time: 03:01
---

[great Lua tutorial](https://www.youtube.com/watch?v=CuWfgiwI73Q)
## for loops
```lua
local favorite_accounts = {"teej_dv", "ThePrimeagen", "terminaldotshop"}

---# is an "octothorpe" or length of operator NOT zero based indexing
for index = 1, #favorite_accounts do
	print(index, favorite_accounts[index])
end
```
> [!warning]- the octothorpe # only works on contiguous data types
> ie all strings, all integers etc. It will not work on a mapping
## ipairs() function
```lua
-- NOTE the same data type so lua sees this as a list type
local favorite_accounts = {"teej_dv", "ThePrimeagen", "terminaldotshop"}

-- ipairs are "index pairs" which returns index and value at that index
for index, value in ipairs(favorite_accounts) do
	print(index,value)
end

```
## pairs() function
```lua
local reading_scores = {teej_dv = 9.5, ThePrimeagen = "N/A" }
-- The above data types are not contiguous so we use pairs NOT ipairs ie "integer pairs"
for key, value in pairs (reading_scores) do
	print(key, value)
end
```
## if statements
```lua
local function action(loves_coffee)
	if loves_coffee then
		print("check out `ssh terminal.shop` - it's cool!")
	else
		print("Check out `ssh terminal.shop` it's cool!")
	end
end

-- "falsey": nil, false
action() -- same as: action(nil)
action(false)

-- Everything else is "truthy"
action(true)
action(0) -- <--- tricky
action({})-- <--- tricky
```
## Modules
```lua
-- nothing special in Lua to denote modules just "files" of functions
-- might see something like
-- foo.lua
local M = {} -- <-- nothing special about capital M its just convention to stand for 'module'
M.cool_function = function() end
-- Don't have to return a table, but it's best practice to future proof to be able to add more and more functions as one big "object" to return as a "module"
return M 


-- Assume this is bar.lua
local foo = require('foo')
foo.cool_function()
```
## Multiple Return Values from Functions
```lua
local returns_four_values = function()
	return 1, 2, 3, 4
end

first, second, last = returns_four_values()

print("first: ", first)
print("second: ", second)
print("last: ", last)
-- the `4` is discarded 
```
## Variable Amount of Arguments
```lua
-- You see it in functions
local variable_arguments = function( ... )
	-- As well as in defining maps
	local arguments = { ... }
	for i, v in ipairs({ ... }) do print(i,v ) end -- print all values
	return unpack(arguments) -- This will just unpack/return all those values
end

print("===========================")
print("1:", variable_arguments("Hello", "world", "!"))
print("===========================")
print("2:", variable_arguments("Hello", "world", "!"), "<lost>") -- this will only allow you to unpack Hello back into the second place, world and ! will be discarded then <lost> will take up that last slot in the print statement
```
## Table Shorthand
```lua
-- This style only works for "literal strings" and "literal tables"
local single_string = function(s)
	return s .. " - WOW!"
end

local x = single_string("HI")
local y = single_string "HI" -- <-- this works with no parenthesis for string literal
print(x, y)

------------------------------------------------------------------------
local setup = function(opts)
	if opts.default == nil then
		opts.default = 17
	end
	
	print(opts.default, opts.other)
end

-- calling it like this simulates "default args" since Lua doesn't support that, but the function will only reference the piece of the table that it needs even though the table contains more "arguments"
setup { default = 12, other = false } -- <-- this works with no paren for table literal
setup { other = true }
```
## Colon Function
```lua
local MyTable = {}

-- Both of these are equivalent
-- : is the only Lua syntax sugar for calling a method and passing self
function MyTable.something(self, ...) end
function Mytable:something( ... ) end
```
# Metatables
## "Meta Methods"
### __add
> [!NOTE]- Metatables
> similar to dunder methods in Python
> describe or change the behavior of tables
```lua
local vector_mt = {} -- table

--[[
Basically the _add below says "vector_mt" table should have the capability to use the + to add and when + is used vector_mt should call some function

setmetatable takes two args:
	- first being a new table(array) that is a combination of left, and right inputs,
	- the second is the table(object) you want the values in
]]
vector_mt._add = function(left, right) -- add functionality to the table "object"
	return setmetatable({              -- 
		left[1] + right[1],
		left[2] + right[2],
		left[3] + right[3],
	}, vector_mt)
end

local v1 = setmetatable({3, 1, 5,}, vector_mt)
local v2 = setmetatable({-3, 2, 2}, vector_mt)
local v3 = v1 + v2 -- this only works because v1, and v2 "inerhit" __add from vector_mt
print(v3[1], v3[2], v3[3])
print(v3 + v3) -- this only works becuase v3 has now "inherited" from vector_mt

```
### __index
Called when you try to get a value from a table and that value doesn't exist

###
```lua
local fib
```