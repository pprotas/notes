---
id: lua
aliases:
  - Lua
tags: []
---

# Lua

Lua is a lightweight programming language designed primarily for embedded use in applications. It originated as a language for extending software applications, and is still in use for that purpose to this day. Lua is not often used as the "main" programming language for an application, but rather as a scripting language that can be used to extend the core functionality of an application by its users.

Examples of video games that use Lua as an embedded scripting language are Garry's Mod, World of Warcraft, Dota 2 and Roblox. Other popular applications that use Lua as a scripting language or Neovim, Redis, Nginx and Wireshark.

## Key language features

> [!note] This is not an exhaustive documentation of the Lua syntax
>
> See the [Lua Reference Manual](https://www.lua.org/manual/5.4/) for Lua's official documentation

### Syntax

Lua has very simple syntax that is easy to learn and familiar to many programmers. You can look it up on the internet, there is no need to go in detail in this note.

### Typing

The language uses dynamic typing. In the manual this is defined as "the variables never have types, but the values do".

### Performance

The code is compiled to bytecode and then interpreted by a virtual machine. In the cases of LuaJIT, it is compiled during runtime.

Lua uses a garbage collector for memory management.

Coroutines are supported in Lua, also called _collaborative multithreading_. These coroutines represent an independent thread of execution.

### Tables

Tables are Lua's most important data structures. They are the foundation of many other types. Tables are like [[arrays]] and [[hash-tables|hash tables]] in one.

Tables are creating using the `{}` syntax:

```lua
a_table = {} -- Creates a new empty table
```

They can be given keys by assigning any value except `nil` or `NaN` to them:

```lua
a_table = { x = 10 }
print(a_table["x"]) -- Prints 10
print(a_table.x) -- Same thing
```

Tables are also arrays (arrays are also indexed from `1` in Lua!):

```lua
an_array = { 10, 20, 30 }
print(an_array[1]) -- Prints 10
```

They can also be used as objects with functions:

```lua
Point = { __index = Point }

function Point:new(x) -- Constructor for Point
  return setmetatable({ x = x }, Point) 
end

function Point:get_x() -- The semicolon `:` syntax is used to automatically pass `self` as the first argument
  return self.x
end

local my_point = Point:new(10)

print(my_point:get_x()) -- Prints 10
```

The above example shows how minimal Lua syntax is, and it requires some more effort from the programmer to implement things that are taken for granted in other languages, like classes. And indeed, there are no built-in classes in Lua, but rather [[prototype-based-programming|prototypes]] are used.

These metatables that are used to implement prototypes can be used to implement other things as well, like operator overloading. They are a very powerful concept that's used to modify the behavior of Lua values under specific conditions. Read more about them in the manual!
