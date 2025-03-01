---
title: "Zap, my new project"
date: "2025-02-01T10:00:00-03:00"
tags: ["project", "zap"]
#title-images: ["/photo6.png",]
#ending-images: []
author: "nykenik"
draft: false
table-of-contents: true
toc-auto-numbering: true
---
<!-- introduction -->
## Intro
I recently started a project called *"Zap"* (original name was *"LunarForge"*), a lightweight game engine with Ruby scripting.
<!--more-->
<!-- rest of the content -->
## What is Zap?
Zap is a lightweight, 2D, game engine completely written in C++ with Ruby scripting. It uses an object-oriented system for creating games.

## Why did I create Zap?
The original idea behind Zap was learning about creating a custom game engine in C++. It was a good way of learning more about the internals of games, how to use C++ to make an engine from scratch, etc. The current purpouse of Zap continues being that, but I now also want to make it a good and reliable game engine for everyone to use that's completely open source (like [Godot](https://godotengine.org/)) and allows you to create all types of games.

Zap also serves (or will serve, seeing it's [current state](#the-current-state-of-zap)) as a game engine that I will probably use a lot when creating my own games, as being the creator makes it so I know how to use every single feature, menu and module.

## The current state of Zap
Zap is in a very early state, not even having a GUI. 

I am currently developing the core, which consists of 3 parts:
- Game object creation and managment system (or *GOCMS* for friends).
- Scene system using `JSON`.
- Scripting system using [`mruby`](https://mruby.org/).

The next step is creating the GUI with the wonderful [*Dear ImGui*](https://github.com/ocornut/imgui).

[Here](https://github.com/Nykenik24/Zap/blob/main/ROADMAP.md) is the full roadmap for Zap.

## The future of Zap
I hope Zap continues, as it's the first project that I **really** enjoy developing. 

With the current state of Zap and it's development process, I think Zap will have a bright future (i hope so). 

## Help in development
Zap is a very ambitious project, and I am only one, so if you want to contribute to Zap, feel free to do so! 

At some moment I will need help from other people to continue developing Zap, it would be *impossible* to fully make Zap without other people pushing me to do it and fixing or adding things I would totally struggle for days if I wanted to implement.

## Support Zap
I don't have a Patreon, Ko-fi or any other donation method, so if you want to support the development of Zap, [star the repository!](https://github.com/Nykenik24/Zap).
