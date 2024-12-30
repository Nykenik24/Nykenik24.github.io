---
title: "Love2d Tools"
subtitle: "Love2d tools documentation"
date: 2024-12-30T14:06:42+01:00
draft: true
toc: true
tags:
    - "docs"
---

## Installation
### Download the library

{{< tabs >}}

{{< tab "Clone" >}}
Clone the repository.
```bash
git clone https://github.com/Nykenik24/love2d-tools.git path/to/library
```
{{< /tab >}}

{{< tab "Submodule" >}}
Add as a submodule.
```bash
git submodule add https://github.com/Nykenik24/love2d-tools.git path/to/library
```
{{< /tab >}}

{{< tab "Release" >}}
Download the latest release.
<p class="imgp">
  <img
    style="max-height: 50vh;border: solid rgb(100, 100, 255) 2px;border-radius: 12px;"
    src="/img/releases_love2d-tools.png"
  />
</p>
{{< /tab >}}

{{< /tabs >}}

### Require the library
To use the library, you need to require it either in `main.lua` or the file where you load libraries.
```lua
local love2d-tools = require("love2d-tools.lib")
-- or to require a single module
local mathx = require("love2d-tools.modules.math")
```

## Module list
#### Modules with documentation
- OOP

#### Modules with W.I.P documentation
- Timer
- Input
- Message Bus
- State Machine
- Vector2
- Mathx
- Tablex
- Logger
- Debug

#### Modules without documentation
- Easing
- Database

## OOP
### Overview
The **OOP** module implements **Object Oriented Programming** [^1], including objects, subclasses, etc. This makes for a very useful module when it comes to entities:\
Lets imagine we have an enemy called *goblin*, an enemy called *skeleton* and an enemy called *slime*. Classes would allow us to implement them easily with a superclass [^2], making a 
subclass[^3] for every type of enemy:
```lua {hl_lines=["3-8", "10-15", "19-21"]}
local class = require("love2d-tools.modules.class") -- OOP module

EnemyClass = class { -- Our "Enemy" superclass
    name = "Enemy",
    hp = 100,
    dmg = 25,
    image = "assets/enemies/placeholder.png",
}

GoblinClass = EnemyClass:extend { -- Our "Goblin" subclass
    name = "Goblin",
    hp = 50,
    dmg = 10,
    image = "assets/enemies/goblin.png"
}
--- And the same for other enemies

-- To create new objects
Goblin1 = GoblinClass:new() -- The `extend()` method returns the subclass
-- or
Goblin1 = EnemyClass.sub.GoblinClass:new() -- Access from the superclass
```
### Methods

#### `NewClass(attributes: table): Class`
---
<details>
<summary>Note</summary>
{{< box info >}}
**Module returns the method**

This method is returned by the module, so to call it you just need to `require` the module call
the module like it was a function.
```lua
local class = require("love2d-tools.modules.class") --require the module
local my_class = class({}) --call the NewClass method
```
{{< /box >}}
</details>

Creates a new **class**.
##### Arguments:
- `attributes: table`: The attributes of the class.
##### Returns:
- `Class: Class`: The created class

#### `Class:new(self: Class): table`
---
Creates a new **object** from a class. This method is inside all classes.

##### Arguments:
- `self: Class`: The class from which the object comes from.
##### Returns:
- `obj: table`: The object.

#### `Class:extend(self: Class, attributes: table): Class`
---
Creates a **subclass**[^2] from a **superclass**[^3].

##### Arguments:
- `self: Class`: The superclass.
- `attributes: table`: Subclass's  attributes.
##### Returns:
- `subclass: Class`: The subclass.

#### `Class:clone(self: Class): Class`
---
**Creates a copy** of the class. It makes inheriting from a class much easier.

##### Arguments:
- `self: Class`: The class copied.

##### Returns:
- `Copy: Class`: The copy of the class.

#### `Class:merge(self: Class, Class2: Class): Class`
---
**Merges two classes** into one. The classes are not overwritten, a new class with the attributes of both class is returned.

##### Arguments:
- `self: Class`: The first class.
- `Class2: Class`: The second class.

##### Returns:
- `Merged: Class`: Merged classes.

#### `obj:_is(self: table, Class: Class): boolean`
---
Checks if an **object comes from a class** comparing the object's id and the class's id.

##### Arguments:
- `self: table`: The object.
- `Class: Class`: The class.

##### Returns:
- `is: boolean`: True if the object comes from the class, false otherwise.

[^1]: *src: [This wikipedia page](https://en.wikipedia.org/wiki/Object-oriented_programming)*\
Object-oriented programming (OOP) is a programming paradigm based on the concept of objects, which can contain data and code: data in the form of fields (often known as attributes or properties), andcode in the form of procedures (often known as methods). In OOP, computer programs are designed by making them out of objects that interact with one another. 

[^2]: *src: [This article](https://www.tutorialspoint.com/Subclasses-Superclasses-and-Inheritance)*\
A superclass is the class from which many subclasses can be created. The subclasses inherit the characteristics of a superclass. The superclass is also known as the parent class or base class.

[^3]: *src: [This article](https://www.tutorialspoint.com/Subclasses-Superclasses-and-Inheritance)*\
A subclass is a class derived from the superclass. It inherits the properties of the superclass and also contains attributes of its own.
