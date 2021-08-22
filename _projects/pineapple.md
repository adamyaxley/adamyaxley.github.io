---
layout: project
title: Pineapple Game Engine
description: 2D game engine utilizing modern C++ to provide an intuitive API and a decoupled plugin system
date: 2012-06-30
links:
  - url: https://github.com/adamyaxley/Pineapple
    text: View on GitHub
  - url: /download/pineapple_game_engine_dissertation.pdf
    text: Read the 2012 Dissertation
---
# Background

The Pineapple Game Engine was the result of my dissertation for my Bachelors degree at Warwick University. Since then, it has continued to live on as a hobbyist project. Originally it could be used to create small games and simulations that could run on Windows, Linux and Nintendo DS. Writing a cross platform game engine completely from scratch was _definitely_ my most valuable learning experience as a computer scientist.

# Dissertation Abstract

This project explores a solution that removes the bottleneck that is present in scripting language based game engines. Using a compiled language for game logic instead of an interpreted language has major advantages, such as a huge performance increase, and removing the possibility of decompilation. Two case studies of current scripting language based game engines are analysed and a platform agnostic game engine is developed in C++ that features the same power and simplicity that scripting languages are popular for.

{% include youtube.html id='7F0ujPC0nj8' %}

# Engine Architecture
The engine consists of one or more Worlds that contain zero or more Objects. The World is responsible for stepping the Objects forward in time based on some Input, storing newly created Objects, and removing any Objects that were destroyed. This simulation loop is executed indefinitely until the world is manually ended.

A simple but complete Hello World in Pineapple could be:

```c++
#include <Pineapple/Pineapple.h>

struct HelloWorld : public pa::Object
{
  HelloWorld(pa::World& world) : pa::Object(world)
  {
    pa::Log::info("Hello World");
    getWorld().end();
  }
};

int main()
{
  // Create the world
  pa::World world;

  // Create the first object
  world.create<HelloWorld>();

  // Process main loop without any Input
  while (world.step(pa::Time(1.f / 60.f)));

  return 0;
}
```

# Plugins
There are three types of plugins: Platform, Graphics and Sound. The interface for each plugin type is predefined and set in stone and therefore makes plugins of the same type completely interchangeable.

* Platform
  * Windows
  * X11
  * Android
  * iOS
* Graphics
  * OpenGL
* Sound
  * FMOD