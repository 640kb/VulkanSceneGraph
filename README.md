![VulkanSceneGraph](https://raw.githubusercontent.com/vsg-dev/VulkanSceneGraph/master/docs/images/VSGlogo.png)

VulkanSceneGraph (VSG), is a modern, cross platform, high performance scene graph library built upon [Vulkan](https://www.khronos.org/vulkan/) graphics/compute API. The software is written in [C++17](https://en.wikipedia.org/wiki/C%2B%2B17), and follows the [CppCoreGuidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines) and [FOSS Best Practices](https://github.com/coreinfrastructure/best-practices-badge/blob/master/doc/criteria.md).  The source code is published under the [MIT License](LICENSE.md).

This repository contains C++ headers and source and CMake build scripts to build the libvsg library.  Additional support libraries and examples are provided in separate repositories, links to these are provided below.  The software currently builds under Linux (desktops variants through to Jetson & Raspberry Pi), Windows (VisualStudio, MinGW & Cygwin), Android, and macOS & iOS (using [MoltenVk](https://github.com/KhronosGroup/MoltenVK)).

## Links Further Information

The [VulkanSceneGraph](https://www.vulkanscenegraph.org) website provide detailed features of the project, tutorial and reference documentation, while this repository provides the source code and build support for creating the VulkanScenGraph library.

Quick links to resources hosted on the website:
* [Features](https://www.vulkanscenegraph.org/features) - tour of features you'll find in the VulkanSceneGraph and companion projects.
* [Screenshots](https://www.vulkanscenegraph.org/screenshots) - screenshots from VulkanSceneGraph exmples and 3rd party library and applications
* [Tutorial](https://www.vulkanscenegraph.org/tutorial) - mulit-part tutorial that takes you from introduction to scene graphs to multi-threading and optimization.
* [Documentation](https://www.vulkanscengraph.org/documentation) - doxygen generated reference documentation and links to 3rd party learning materials
* [Discussion](https://github.com/vsg-dev/VulkanSceneGraph/discussions) - Discussion forum hosted on github.
* [Services](https://www.vulkanscengraph.org/services) - List of companinies connected to the VulkanSceneGraph project that can provide professional services


## Links Companion projects that offer additional features:
* [vsgXchange](https://github.com/vsg-dev/vsgXchange) reading and writing of 3rd party image and 3d models and HTTP support.
* [vsgExamples](https://github.com/vsg-dev/vsgExamples) tests & examples.
* [osg2vsg](https://github.com/vsg-dev/osg2vsg) OpenSceneGraph integration library that enables converting of OSG to VSG scene graph and use of OpenSceneGraph loaders.
* [vsgImGui](https://github.com/vsg-dev/vsgImGui) ImGui integration enabling UI in graphics window.
* [vsgQt](https://github.com/vsg-dev/vsgQt) Qt integration with VulkanSceneGraph.
* [vsgUnity](https://github.com/vsg-dev/vsgUnity) plugin for Unity that provides export to native VulkanSceneGraph binary/ascii format.
* [MyFirstVsgApplication](https://github.com/vsg-dev/MyFirstVsgApplication) simple standalone VSG application that can be used as a template for your own applications.
* [vsgFramework](https://github.com/vsg-dev/vsgFramework) template project that uses CMake FetchContent to pull in all the main libraries associated with VulkanSceneGraph and dependencies and builds them together.
* [vsgSDL](https://github.com/ptrfun/vsgSDL) SDL integration with VulkanSceneGraph.
* [vsgvr](https://github.com/geefr/vsgvr) OpenVR integration with VulkanSceneGraph.

## Quick Guide to building the VSG

### Prerequisites:
* C++17 compliant compiler i.e.. g++ 7.3 or later, Clang 6.0 or later, Visual Studio S2017 or later.
* [Vulkan](https://vulkan.lunarg.com/) 1.1 or later.
* [CMake](https://www.cmake.org) 3.7 or later.

The above dependency versions are known to work so they've been set as the current minimum, it may be possible to build against older versions.  If you find success with older versions let us know and we can update the version info.

Download VulkanSDK from [LunarG](https://vulkan.lunarg.com/sdk/home), unpack into local directory and set VUKAN_SDK environment variable to the include/lib directory within it. For Linux it would typically be along the lines of:

    export VULKAN_SDK_VERSION=1.2.162.1
    export VULKAN_SDK=${PWD}/VulkanSDK/${VULKAN_SDK_VERSION}/x86_64

    mkdir VulkanSDK
    wget https://sdk.lunarg.com/sdk/download/${VULKAN_SDK_VERSION}/linux/vulkansdk-linux-x86_64-${VULKAN_SDK_VERSION}.tar.gz -O VulkanSDK/vulkansdk-linux-x86_64-${VULKAN_SDK_VERSION}.tar.gz
    tar zxf VulkanSDK/vulkansdk-linux-x86_64-${VULKAN_SDK_VERSION}.tar.gz -C VulkanSDK/

Once you've downloaded and unpacked the VulkanSDK you'll want to put VULKAN_SDK into your user environment variable setup so that CMake's find_package(Vulkan) can find the VulkanSDK's location.

### Command line build instructions:

To build and install the static libvsg library (.a/.lib) in source:

    git clone https://github.com/vsg-dev/VulkanSceneGraph.git
    cd VulkanSceneGraph
    cmake .
    make -j 8
    sudo make install

Full details on how to build of the VSG (Unix/Windows/Android/macOS) can be found in the [INSTALL.md](INSTALL.md) file.
