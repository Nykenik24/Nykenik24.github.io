---
title: "Love2d Tools"
subtitle: "Love2d tools documentation"
date: 2024-12-30T14:06:42+01:00
draft: false
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
Download the [latest release](https://github.com/Nykenik24/love2d-tools/releases).
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
#### Documented modules
---
Here are the modules with already made documentation.
- OOP
- Timer
- Input

#### Modules to document
---
Here are the modules that will have documentation, but it's not made.
- Message Bus
- State Machine
- Vector2
- Mathx
- Tablex
- Logger
- Debug

#### Not documented modules
---
Here are the modules that will not have any documentation.
- Easing
- Database

## OOP
### Overview
The **OOP** module implements **Object Oriented Programming** [^1], including objects, subclasses, etc. This makes for a very useful module when it comes to entities:\
Lets imagine we have an enemy called *goblin*, an enemy called *skeleton* and an enemy called *slime*. Classes would allow us to implement them easily with a superclass[^2], making a 
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
### Custom types
- `Class`
    - `attributes: table`: Class's attributes.
    - `sub: table`: Class's subclasses[^3].
    - `id: string`: Class's identification pattern. Class's objects will have the same id.
    - All methods below that start with `Class:`.

### Methods

#### `NewClass(attributes: table): Class`
---
<details>
<summary>Note</summary>
{{< box info >}}
**Module returns the method**

This method is returned by the module, so to call it you just need to `require` the module and call
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
Creates a **subclass** [^3] from a **superclass**[^2].

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

## Timer
### Overview
This module allows you to create simple timers, allowing to delay attacks, create eased animations, etc.

### Custom types
- `Timer`
    - `orig: number`: Original duration.
    - `seconds: number`: Countdown from `orig` to 0.
    - `rounded_seconds: integer`: Rounded `seconds`.
    - `elapsed: boolean`: True if timer ended.
    - `OnEnd: function`: Called when timer ends. Made to be modified.
    - All methods below that start with `Timer:`.

### Methods

#### `new(duration: number): Timer`
---
<details>
<summary>Note</summary>
{{< box info >}}
**Module returns the method**

This method is returned by the module, so to call it you just need to `require` the module and call
the module like it was a function.
```lua
local timer = require("love2d-tools.modules.timer") --require the module
local my_timer = timer(5) --call the `new` method
```
{{< /box >}}
</details>

Creates a new **timer**.

##### Arguments:
- `duration: number`: Timer's duration.

##### Returns:
- `timer: Timer`: The new timer.

#### `Timer:Update(self: Timer, dt: number): number, boolean`
---
Updates the timer, has to be called in the `love.update(dt)` function.

##### Arguments:
- `self: Timer`: The timer.
- `dt: number`: Delta time[^4].

##### Returns:
- `seconds: number`: Countdown from `Timer.orig` to 0.
- `elapsed: boolean`: True if timer ended.

#### `Timer:Reset(self: Timer, new_duration?: number): number`
---
Resets the timer to `Timer.orig`, or to the optional parameter `new_duration`.

##### Arguments:
- `self: Timer`: The timer.
- `new_duration (optional): number`: New timer duration.

##### Returns:
- `seconds: number`: Countdown from `Timer.orig` to 0.

## Input
### Overview
The input module allows you to easily map keys to certain actions and check if mouse is hovering an area or being held.

### Custom types
- `Area`
    - `x1: number`: Left side.
    - `y1: number`: Top.
    - `x2: number`: Right side.
    - `y2: number`: Bottom.

    ![Area](/img/mouse-area_love2d-tools.png)

### Keyboard methods

#### `Map(key: string, func: function, ...?: table): table`
---
Maps a key to an action.

##### Arguments:
- `key: string`: Key to map.
- `func: function`: Action.
- `... (optional): table`: `func`'s arguments.

##### Returns:
- `keybind: table`: The keybind with the action and args.

#### `Input:UpdateKeys(current: string)`
---
Updates all keybinds. Has to be called inside `love.keypressed(key)`, not inside `love.update`, with first argument (`current`) being `love.keypressed`'s first argument (`key`).
{{< box info >}}
**Example**

```lua
function love.keypressed(key)
   Input:UpdateKeys(key)
end
```
{{< /box >}}

##### Arguments:
- `current: string`: The key that was pressed now.

### Mouse methods

#### `IsHovering(x1: number, y1: number, x2: number, y2: number): boolean`
---
Checks if mouse is hovering a certain area *(see **input --> custom types**)*.

##### Arguments:
- `x1: number`: Left side.
- `y1: number`: Top.
- `x2: number`: Right side.
- `y2: number`: Bottom.

##### Returns:
- `hovering: boolean`: True if it is hovering.

#### `IsHoldingMouse(): boolean, number`
---
Checks if the user is holding a mouse button. If they are then returns also what mouse button.

##### Returns:
- `Holded: boolean`: True if a mouse button is being holded.
- `Button: number`: Mouse button being holded.
    - **1**: Left button.
    - **2**: Right button.
    - **3**: Middle button.
    - **0**: No button is being holded.

#### `MouseButtonHolded(button: number): boolean`
---
Checks if a specific mouse button is being holded.

##### Arguments:
- `button: number`: Mouse button.
    - **1**: Left button.
    - **2**: Right button.
    - **3**: Middle button.
    - **0**: No button is being holded.

##### Returns:
- `holded: boolean`: The mouse button is being holded.

#### `IfHovering(area: Area, func: function, ...?: table): boolean, any`
Checks if the mouse is hovering `area`, calls `func` with `...` *(args)* and returns:
- If it is hovering.
- `func` returned values.

##### Arguments:
- `area: Area`: Area that has to be hovered.
- `func: function`: Function called if hovered.
- `... (optional): table`: `func`'s argument.

## Message Bus
### Overview
Message bus that handles publishers and subscribers, giving a simple **EDA**[^5] implementation to make your game events.

### Methods

#### `NewSubPoint(idlen?: number): table`
---
Creates a new **subscription point**.

##### Arguments:
- `idlen (optional): number`: Subscription point ID length. Default is 16.

##### Returns:
- `SubPoint: table`: A subscription point object with an ID and a method to retrieve messages.

#### `GetMsg(type: string|nil): any`
---
Retrieves messages for a subscription point or broadcasts.

##### Arguments:
- `type: string or nil`: The type of message to retrieve:
    - `nil`: Messages only for the subscription point.
    - `broadcast`: Messages for all subscription points.

##### Returns:
- `Content: any`: Content of the message.

#### `SendMessage(id: string, content: any)`
---
Sends a message to an specific subscription point.

##### Arguments:
- `id: string`: The **ID** of the subscription point.
- `content: any`: The **content** of the message.

#### `Broadcast(content: any): table`
---
Sends a message to **ALL** subscription points.

##### Arguments:
- `content: any`: The content to broadcast to all subscription points.

##### Returns:
- `Broadcast: table`: An object with a position and a method to end the broadcast.

[^1]: **OOP** *src: [This wikipedia page](https://en.wikipedia.org/wiki/Object-oriented_programming)*\
Object-oriented programming (OOP) is a programming paradigm based on the concept of objects, which can contain data and code: data in the form of fields (often known as attributes or properties), andcode in the form of procedures (often known as methods). In OOP, computer programs are designed by making them out of objects that interact with one another. 

[^2]: **Superclass** *src: [This article](https://www.tutorialspoint.com/Subclasses-Superclasses-and-Inheritance)*\
A superclass is the class from which many subclasses can be created. The subclasses inherit the characteristics of a superclass. The superclass is also known as the parent class or base class.

[^3]: **Subclass** *src: [This article](https://www.tutorialspoint.com/Subclasses-Superclasses-and-Inheritance)*\
A subclass is a class derived from the superclass. It inherits the properties of the superclass and also contains attributes of its own.

[^4]: **Delta time** *src: [This wikipedia page](https://en.wikipedia.org/wiki/Delta_timing)*\
Delta time or delta timing is a concept used amongst programmers in relation to hardware and network responsiveness. In graphics programming, the term is usually used for variably updating scenery based on the elapsed time since the game last updated, (i.e. the previous "frame") which will vary depending on the speed of the computer, and how much work needs to be done in the program at any given time. This also allows graphics to be calculated separately if graphics are being multi-threaded.

[^5]: **EDA** *src: [This wikipedia page](https://en.wikipedia.org/wiki/Event-driven_architecture)*\
Event-driven architecture (EDA) is a software architecture paradigm concerning the production and detection of events. Event-driven architectures are evolutionary in nature and provide a high degree of fault tolerance, performance, and scalability. However, they are complex and inherently challenging to test. EDAs are good for complex and dynamic workloads. 
