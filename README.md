

## Cloning
```
gh repo clone darzu/vk-sample
```

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
Forked from: https://github.com/SaschaWillems/Vulkan.

See [CREDITS.md](CREDITS.md) for additional credits and attributions.
