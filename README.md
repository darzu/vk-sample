# Vulkan C++ examples and demos

A comprehensive collection of open source C++ examples for [Vulkan®](https://www.khronos.org/vulkan/), the new generation graphics and compute API from Khronos.

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=BHXPMV6ZKPH9E)

## Table of Contents
+ [Official Khronos Vulkan Samples](#official-khronos-vulkan-samples)
+ [Cloning](#Cloning)
+ [Assets](#Assets)
+ [Building](#Building)
+ [Running](#Running)
+ [Shaders](#Shaders)
+ [A note on synchronization](#a-note-on-synchronization)
+ [Examples](#Examples)
+ [Credits and Attributions](#credits-and-attributions)

## Official Khronos Vulkan Samples

Khronos has made an official Vulkan Samples repository available to the public ([press release](https://www.khronos.org/blog/vulkan-releases-unified-samples-repository?utm_source=Khronos%20Blog&utm_medium=Twitter&utm_campaign=Vulkan%20Repository)).

You can find this repository at https://github.com/KhronosGroup/Vulkan-Samples

As I've been involved with getting the official repository up and running, I'll be mostly contributing to that repository from now, but may still add samples that don't fit there in here and I'll of course continue to maintain these samples.

## Cloning
This repository contains submodules for external dependencies and assets, so when doing a fresh clone you need to clone recursively:

```
git clone --recursive https://github.com/SaschaWillems/Vulkan.git
```

Existing repositories can be updated manually:

```
git submodule init
git submodule update
```

## Assets

**Important notice:** As of may 2023 assets have been moved to a [submodule](https://github.com/SaschaWillems/Vulkan-Assets). If you have cloned the repository before this date, you may need to initialize and update submodules. If you do a fresh clone, no action is required to get the assets.

## Building

The repository contains everything required to compile and build the examples on Windows using a C++ compiler that supports C++14.

See [BUILD.md](BUILD.md) for details on how to build for the different platforms.

## Running

Once built, examples can be run from the bin directory. The list of available command line options can be brought up with `--help`:
```
 -v, --validation: Enable validation layers
 -br, --benchruntime: Set duration time for benchmark mode in seconds
 -vs, --vsync: Enable V-Sync
 -w, --width: Set window width
 -f, --fullscreen: Start in fullscreen mode
 --help: Show help
 -h, --height: Set window height
 -bt, --benchframetimes: Save frame times to benchmark results file
 -b, --benchmark: Run example in benchmark mode
 -g, --gpu: Select GPU to run on
 -bf, --benchfilename: Set file name for benchmark results
 -gl, --listgpus: Display a list of available Vulkan devices
 -bw, --benchwarmup: Set warmup time for benchmark mode in seconds
```

Note that some examples require specific device features, and if you are on a multi-gpu system you might need to use the `-gl` and `-g` to select a gpu that supports them.

## Shaders

Vulkan consumes shaders in an intermediate representation called SPIR-V. This makes it possible to use different shader languages by compiling them to that bytecode format. The primary shader language used here is [GLSL](shaders/glsl).

## A note on synchronization

Synchronization in the master branch currently isn't optimal und uses ```vkDeviceQueueWaitIdle``` at the end of each frame. This is a heavy operation and is suboptimal in regards to having CPU and GPU operations run in parallel. I'm currently reworking this in the [this branch](https://github.com/SaschaWillems/Vulkan/tree/proper_sync_dynamic_cb). While still work-in-progress, if you're interested in a more proper way of synchronization in Vulkan, please take a look at that branch.


## Examples

#### [First triangle](examples/triangle/)
Basic and verbose example for getting a colored triangle rendered to the screen using Vulkan. This is meant as a starting point for learning Vulkan from the ground up. A huge part of the code is boilerplate that is abstracted away in later examples.

#### [Deferred shading shadow mapping](examples/deferredshadows/)

Adds shadows from multiple spotlights to a deferred renderer using a layered depth attachment filled in one pass using multiple geometry shader invocations.

## Credits and Attributions
See [CREDITS.md](CREDITS.md) for additional credits and attributions.
