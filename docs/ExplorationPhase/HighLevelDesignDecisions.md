
# 8) High Level Design Decisions

**Project name:** VulkanSceneGraph preferred, may need to use VkSceneGraph is permission from Khronos is not secured.

**Language:** C++17 minumum standard.

**Build tool:** lead choice CMake due to familiarity and market penetration.

**Source code control:** git hosted on github.

**Maths :** local GLSL style maths class, inspired by GLSL, GLM and the Vulkan conventions.

**Windowing:** local native Windowing integrated with core VSG library, with ability to use 3rd party Windowing

**Vulkan integration:** Aim for coherent naming and granularity as underlying Vulkan API

* lightweight local C++ wrappers of Vulkan objects, naming and style inspired by Vulkan C API.
* Provide convenient and robust setup and clean of resources.
* Standard naming VkFeature -> vsg::Feature in include/vsg/vk/Feature.h
* Cmd naming VkCmdFeature -> vsg::Feature, subclassed from vsg::Command
* State VkCmdFeature -> vsg::Feature, subclassed from vsg::StateComponent


**Single library:** all core, maths, nodes, utilities, vulkan and viewer provided in libvsg library, can be either be used as static or dynamic library.

**Namespace:** vsg used for all categories of functionality in keeping

**Headers:** .h used for public classes/functions

Categories of functionality placed in appropriately name subdirectories i.e.
* include/vsg/core/Object.h
* include/vsg/nodes/Group.h
* include/vsg/vk/Instance.h
For convenience high level include/vsg/all.h head to includes all vsg/*/*.h

**Source:** .cpp extension used

Categories of functionality placed in appropriate name subdirectories i.e.
* src/vsg/core/Visitor.cpp
* src/vsg/viewer/Viewer.cpp


**Memory:** To address the main performance scene graph bottleneck have a general goal of improving cache coherency and lowering memory bandwidth load.

Intrusive reference counting twice as memory efficient as std::shared_ptr<>, and results in ~50% better traversals speeds. Use vsg::ref_ptr<>, vsg::observer_ptr<> and vsg::Object.

Use std::atomic to provide efficient, thread safe reference counts

To minimize the size of majority of internal scene graph nodes and leave nodes the ancillary data that only few objects required are moved out of the
Base vsg::Object/Node classes into an vsg::Auxiliary object.

**Unification:**
All vsg::Object support intrusive reference counting and meta data support All vsg::Object support type safe query via vsg::Visitor

All uniform and vertex array data can be handled via the Data interface Single value data via the vsg::Value template Array data via the vsg::Array template

The main scene graph and the rendering backends command graph utilize the same scene graph hierarchy.

Vulkan Compute and Graphics to be supported with the same Vulkan wrappers, scene graph and command graph hierarchies.


**Usage models:** Application developers will be able to dispatch data directly to Vulkan using the VSG’s Vulkan wrappers in a form of an immediate mode, creating their own command graphs that using standard vsg command visitors or their own custom visitors, through to using visitor to cull the main scene graph down to a command graph each frame and dispatching this vulkan.


**Introspection:** Not explored during Exploration Phase so will need to be addressed in future. Aim to provide introspection/reflection for all core scene graph objects to provide support for reading/writing scene graph objects and open the door to scripting.


**IO:** Support for loading 3rd party images and 3d models is currently deemed outwith the scope core libvsg library.  Only IO supported will be via the native scene graph objects support for reflection. This IO support will enable scene graphs, images and shaders to read and written without
any additional libraries.


Support for 3rd party images, 3d models and shaders will be provided by add
on libraries. To aid with porting of OpenSceneGraph application a osg2vsg
library will be developed so that all loaders that the OpenSceneGraph has will
be available.  These 3rd party on libraries providing image. 3d model and shaders will form an important part of testing of the VSG project as it evolves and are expected to development in conjunction with the VSG project.
