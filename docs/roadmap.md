# Overview and Roadmap

This document provides an overview and roadmap for different parts of the ZetaVM project.

## ZetaVM Prototype

The current implementation of ZetaVM is at the prototype stage. There is currently an interpeter, but no garbage collector and no JIT compiler. The current goal is to get the system running quickly with a core set of features, so that we can  prototype, properly the system, iron out bugs, and alter the design as necessary.

## Plush

The first language implemented on top of ZetaVM is called Plush. This language is inspired by JavaScript and Lua, and serves both to bootstrap the system, and to demonstrate to beginners how they can build their own language targetting ZetaVM. The Plush language may eventually have optional extensions, but the core language itself will intentionally be kept simple so that its implementation remains simple and accessible to beginners.

## Core Libraries

A set of core libraries will be provided as part of ZetaVM. These will be written in C++ and implement a set of intput/output APIs to interface with the outside world. The APIs provided will intentionally be kept low-level, simple and minimalistic to minimize the risk of introducing corner cases and undefined behaviors. It is expected that higher-level libraries will be implemented on top of these and provide more user-friendly interfaces.

The core libraries will cover services such as file I/O, console I/O, basic 2D graphics (pixel plotting and blitting), mouse and keyboard input as well as raw PCM audio output. The early prototype version of the VM will implement only the most essential libraries.

## Language Extensions

The Plush language will eventually make it possible for people to write parser extensions. This will allow the addition of new operators, new expression types, and new statement types to the language.

Some possible Plush extensions include:
- Closures
- Template strings
- Regular expressions
- Pattern matching
- Gradual typing
- Variable argument count functions, optional arguments

## Immutable Package Manager

The VM will eventually ship with a package manager. This package manager will make it trivial to immediately upload code you have written from the command-line and make it available to anyone. The package manager will also be used to upload your own language implementation package, making it instantly accessible to anyone using ZetaVM.

Packages will be versioned and immutable. That is, once a package is uploaded, it will be assigned a version number, e.g. `"john/imagelib/56"`. This package version will then be frozen and unchangeable. The aim is to make it so that once code relies on a specific package version, the dependencies can never be changed and broken. Hence, by freezing the core VM semantics, and freezing submitted packages, we will hopefully make it possible to write software that doesn't break.

## JIT Compiler

Once ZetaVM is past the initial prototyping stage, a JIT compiler will be implemented to improve performance. This JIT will likely be based on basic block versioning. The [current plan](https://pointersgonewild.com/2017/06/11/zetas-jitterpreter/) is that the JIT will use the same internal representation as the interpreter, that is, the interpreter will do part of the compilation work.

## SPMD Execution (GPU Support)

Multithreaded programming brings the potential for unpredictability and deadlocks. Zeta will instead offer native support for the Single Program Multiple Data (SPMD) programming model. This is the programming model commonly employed by vertex, pixel and compute shaders running on GPUs. One novel feature, in this respect, is that Zeta will allow the same code to run both on the CPU and GPU, with only minor restrictions. This means that potentially, any language running on Zeta will be able to execute in parallel on GPUs.
