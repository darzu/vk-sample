# Shaders

This folder contains the shaders used by the samples. Source files are available as GLSL and also come with precompiled SPIR-V files that are consumed by the samples. To recompile shaders you can use the `compileshaders.py` scripts in the Shaders/GLSL folder or any other means that can generate Vulkan SPIR-V from GLSL or HLSL. One such option is [this extension for Visual Studio](https://github.com/SaschaWillems/SPIRV-VSExtension).

NOTE:
need to have "glslangvalidator.exe " in path
https://github.com/SaschaWillems/SPIRV-VSExtension?tab=readme-ov-file#glsl-standalone-reference-compiler
https://vulkan.lunarg.com/