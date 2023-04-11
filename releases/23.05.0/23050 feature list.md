
# O3DE 23.05.0 Feature List

**Status:** In-Progress

Release 23.05.0 consists of .... Here are some highlights, followed by a detailed list of features broken down by SIG.

* Highlight 1
* Highlight 2


## sig-build

* Test Impact Analysis Framework rollout ([#10660](https://github.com/o3de/o3de/issues/10660))
	* Test Impact Analysis Framework (TIAF) is a system to determine which tests need to run for every source change. The idea behind it is to only run the tests you need to (that might be impacted by the change). The system is now deployed for both Python and native C++ tests. Developers working on O3DE should on average see a reduction in the time they have to wait for their tests to run.


## sig-content

* Adds support for global python scripts per asset type to simply customizations in the scene pipeline.
* A new Asset Browser experience has been prepared and turned on by default. The new Asset Browser experience includes three new layout modes (table view, thumbnail view, list view), file operations (add/delete/edit/rename/move), asset drag and drop support, URL bar for easy sharing and editing, breadcrumb and navigation bar, new detached Asset Browser inspector panel, filter options to hide unusable editor or engine assets, and all new asset icons.
	* To disable the new Asset Browser, disable the ed_useWIPAssetBrowserDesign console variable from the Tools menu
	* If the new Asset Browser layout is not properly set, restore the default layout from the View -> Layouts menu option
	* Searching is disabled in the table view while this feature is being developed, please use the thumbnail view or list view to search for assets
* Gems creators can now specify compatible platforms, which can be filtered against in the gem catalog.
* Users can choose to edit existing gems .json files via the Create a Gem Wizard or CLI.
* O3DE utility widgets in the AzQtComponents library are now exposed to Python and Pyside. This allows Python-based developers of tools and gems to use or extend AzQtComponents for tools, plugins, or automation.
* Provides the ability to manage and visualize prefab overrides from O3DE Editor's Entity Outliner. Users can now override prefabs by adding/removing entities, nested prefabs, and components or changing component properties. For more information, please refer to the [user guide](https://www.o3de.org/docs/learning-guide/tutorials/entities-and-prefabs/override-a-prefab/). (NOTE: Link not live until release)
* Versioning Framework allows the engine to understand what version it is and adds the ability for feature, gem, template, and project creators to specify versions that the engine can compare and potentially validate against.
* Ability to install multiple versions of O3DE on the same drive, and projects are aware of which O3DE version they were created in and last used with. UX adjustments to better communicate engine version to the user.
* Ability to download an O3DE Linux Snap package from the Snap Store and from O3DE.org binaries. Snap packaging improves installation time and reduces (in many cases eliminates) the need to download dependencies.
* Adds an optional mode to improve AssetProcessor start-up time when users are just making code changes.
* Updates to 3D viewport Documentation ([#2062](https://github.com/o3de/o3de.org/pull/2062))
	* The 3D viewport documentation has been completely overhauled to make it much easier to follow. Many new viewport features are now also documented too.
* Viewport UI Switcher Improvements ([#13108](https://github.com/o3de/o3de/pull/13108), [#13036](https://github.com/o3de/o3de/pull/13036))
* Multiple fixes and improvements to editor ‘Be this camera’ functionality ([#14269](https://github.com/o3de/o3de/pull/14269), [#15119](https://github.com/o3de/o3de/pull/15119))
* Several small improvements to viewport camera behavior ([#12882](https://github.com/o3de/o3de/pull/12882), [#13408](https://github.com/o3de/o3de/pull/13408), [#13433](https://github.com/o3de/o3de/pull/13433), [#13590](https://github.com/o3de/o3de/pull/13590), [#13626](https://github.com/o3de/o3de/pull/13626), [#13628](https://github.com/o3de/o3de/pull/13628), [#13669](https://github.com/o3de/o3de/pull/13669))

## sig-core

 * A new performance metrics logging API has been added to AzCore.  
The API provides the following classes that can be used to output JSON recorded metrics: The pair of `AZ::Metrics::IEventLogger` and `AZ::Metrics::JsonTraceEventLogger`, and the other pair of `AZ::Metrics::IEventFactory` and `AZ::Metrics::EventFactoryImpl`  
The `AZ::Metrics::JsonTraceEventLogger` implements the `AZ::Metrics::IEventLogger` interface which allows logging metrics to the [Google Trace Event Format](https://docs.google.com/document/d/1CvAClvFfyA5R-PhYUmn5OOQtYMH4h6I0nSsKchNAySU/preview#).
The `AZ::Metrics::EventFactoryImpl` implements the `AZ::Metrics::IEventFactory` API and provides a registrar for mapping a numeric identifier to `AZ::Metrics::IEventLogger` implementations.  
Metrics files should ideally be output to an active projects `<project-root>/user/Metrics` directory.  
  The metrics are loadable in a chromium based browser `about::tracing` page or via [chromium's standalone trace viewer application](https://google.github.io/trace-viewer/).  For more examples of how to use the performance metrics logging API see the examples usages in the [Performances Metrics Gathering API document](https://development--o3deorg.netlify.app/docs/user-guide/programming/metrics/).    
	 * Associated PR's:   
		 * https://github.com/o3de/o3de/pull/12252  
		 * https://github.com/o3de/o3de/pull/12476  
		 * https://github.com/o3de/o3de/pull/12483  
		 * https://github.com/o3de/o3de/pull/13202  
		 * https://github.com/o3de/o3de/pull/13596
* AZ Allocators are now created on-demand, instead of requiring explicit Create and Destroy calls. This allows AZStd containers, which use AZ Allocators, to be used anywhere, including in global static variables. Developers who are subclassing the PoolAllocator, would need to change their code to ensure all their construction happens in the constructor instead of in the Create() method.
* Improvements to the Scene Settings UX to remove points of friction and confusion, with a focus on improvements to default prefabs, LOD and character based workflows.
* Updates the Open Asset Import Library to version 5.2.5 to support asset pipeline improvements. Brings a large number of important bug fixes for compression, out-of-bounds errors, crashes, memory allocation and import issues.
* Upgraded Google Benchmark library ([#13630](https://github.com/o3de/o3de/pull/13630))
* Fixed Math unit tests on Android and enabled NEON instructions by default ([#13739](https://github.com/o3de/o3de/pull/13739), [#13783](https://github.com/o3de/o3de/pull/13783), [#13792](https://github.com/o3de/o3de/pull/13792))


## sig-docs-community

* Feature 1
* Feature 2

## sig-graphics-audio

* DccScriptingInterface Gem configures and bootstraps DCC tools like Maya and Blender from the Editor, and provide workflow utilities like a streamlined 'Scene Exporter' to get cleaner content to O3DE projects.
* Added RHI Bindless support which allows RHI to manage bindless heap for all image and buffer views across all backends. It caches view descriptors on the gpu memory and provides access to the index in the unbounded array to RPI at runtime. This index can be used by features to indirectly access image or buffer views on the gpu within the shader. Instead of managing your own custom unbounded arrays for buffer and image views features can now just use the one managed by RHI. As a result RHI bindless support is now being used by Terrain and Ray Tracing.
* Material canvas is now available for users to create new, custom shaders and materials. Material canvas is built upon the combined foundations of script canvas and material editor, offering most of the same features and UX as both. Users are able to visually edit, drag, drop, connect, and configure graphical nodes that are automatically transformed into all of the required source files that would otherwise need to be hand created and manually managed.  
	* Typically, the generated source files include shader configurations, AZSL source, material types, and a default material. As these files are generated, they are automatically recognized and processed by the AP, displayed in the viewport, and made available for use in the material editor, material component, and other aspects of the engine that use shaders and materials.  
	* Approximately 150 nodes are provided out-of-the-box. Most of those represent AZSL intrinsic functions, constant values, input values, output nodes, and other types. Material output nodes are the main notes for any material graph. They define a template that encapsulates all of the data and dependencies to tell material canvas what to generate when it compiles the graph. Once a material output node has been added to the graph, users will begin to see files generating, assets building, in the viewport updating with subsequent changes.  
	* All current material graph nodes are implemented as simple JSON configuration files, listening all of the input and output slots, data types, default values, snippets of shader code, and other metadata. The new library is fully extensible and customizable by simply adding new JSON files.  
	* Material canvas can also open and provides tooling for creating and editing the material graph node files. These can live in any gems or projects but they must have a unique UUID in every file. There are several examples for all of the existing nodes in the material canvas project.  
	* Like material editor, most or all aspects of the tool are also exposed through behavior context reflection for Python automation.  
	* Additional testing and documentation are in progress.     
	* PR: https://github.com/o3de/sig-graphics-audio/issues/51  
	* Known issues:  
		*  Load times need to be improved for graphs that contain thousands of nodes.  
		* Undo redo performance needs to be improved for graphs containing thousands of nodes.  
		* Undo redo currently selects all nodes in a graph.  
		* More advanced or artist friendly nodes need to be created to extend the node library.  
		* Previews rely on shader compilation times which also need to be optimized but there are settings in the tools->settings dialog to disable shader compilation for unused platforms.  
		* Some changes do not always immediately refresh the viewport due to some asset reloading edge cases.
		* The layout of node slots is not cleanly aligned and needs to be improved.
		* Notes do not always resize to there will come a minimum size when making and breaking connections.
		* General material types can include several shader files packaged more compactly. In the meantime, users will have to be mindful of where they save their material graphs since more complicated material templates and output nodes will produce several files.
		* Switching to multi view and XR pipelines causes a crash in material editor and material canvas.
* CPU performance has been improved such that an 8 core CPU with an nVidia 2080 can handle 9000 static and 1000 dynamic entities at greater than 30fps at 1080p
* Added support for Terrain nodes in Landscape Canvas  
	* Added a generic paintbrush workflow and implemented the ability to paint both heights and color directly in the editor viewport for the Terrain System  
	* Added the Terrain Developer Guide that explains how developers can use and extend the terrain system.  
	* The paint brush workflow also includes runtime scripting support for real-time modifications of the terrain using a painting API.  
	* Here are some documentation links, they'll need to get fixed up to point to the release branch of the docs:  
		* Tutorial on creating terrain from images using Landscape Canvas: https://www.o3de.org/docs/learning-guide/tutorials/environments/create-terrain-from-images/  
		* Image Gradient Component with Paint Brush support: https://development--o3deorg.netlify.app/docs/user-guide/components/reference/gradients/image-gradient/  
		* Terrain Macro Material Component with Paint Brush support: https://development--o3deorg.netlify.app/docs/user-guide/components/reference/terrain/terrain-macro-material/  
		* Generalized Paint Brush documentation: https://development--o3deorg.netlify.app/docs/user-guide/components/reference/paintbrush/paintbrush/  
		* Terrain Developer Guide: https://development--o3deorg.netlify.app/docs/user-guide/visualization/environments/terrain/terrain-developer-guide/
* Sphere and disk lights now support shadow caching, which is accessible as a checkbox on the light component. This makes it so shadows do not re-render when nothing in their field of view has changed, and can greatly accelerate shadows on mostly static scenes. Models which have vertex animation in the shader can toggle on "Always moving" in the mesh component to ensure that they will always trigger updates when in the view of a cached shadow.
* Added support for stereoscopic rendering (i.e VR support) via OpenXr within O3de. This support was added through the Vulkan backend and it has been extensively tested using Quest 2. As part of this effort we are able to support Link mode where the rendering is done on PC and can be viewed on a stereoscopic display or the app can be run on the device natively. A special optimized VR pipeline has been added to Atom to help support running the app natively on the device.
* The texture streaming support has been expanded to Vulkan backend. Now we have image streaming control which can load or evict texture mips automatically at runtime based on the streaming image pool's budget.
* The shader library, material system, and builders have been updated to support a layer of abstraction between lighting and materials, called the material pipeline. It uses new builders and new features from the asset system to build unique shaders for each render pipeline. Material types can provide custom data structures and evaluator functions for vertex, pixel, geometry, and lighting stages. The builder inserts any of the custom include files with overridden data types and functions as it builds all of the combinations of shaders listed in the material pipeline.  
	* The result of this is a concrete material type referencing all of the different combinations of shaders for each pipeline, with the customization stitched in. All of this is saved to the intermediate assets folder and processed by the AP to generate Final product material types and shaders. The material pipeline also includes a Lua script that will be invoked whatever material properties or the active render pipeline changes to enable or disable shaders based on the current state.  
	* All of the PBR as well as other shaders and material types included with atom have been converted to the system.  
	* All of the ASV samples and tests have also been updated to use this system. ASV also includes different experimental render and material pipelines to demonstrate how existing materials that use this system can be applied to a standard, deferred rendering pipeline.
	* Known issues:  
		* It takes more time to compile shaders for all of the active pipelines.
		* Material editor and material canvas crash switching to Multiview at XR pipelines.
		* The organization of all of the shader and material files needs to be simplified to make it easier to find shader and material files.
		* There are several to do items as a result of these changes that need to be addressed.


## sig-network

* Adds new warnings when client and server have differences in networked code and properties to aid debugging of these issues.
* Provides method for code separation between client and server side code to prevent any exposure of server side logic to clients. Provides a new Unified Launcher target to aid local testing.
* Provides a more out-of-the-box demonstration of Amazon GameLift using the new multiplayer sample with workflow refinements to make it easier to setup and use.

 
## sig-operations

* Feature 1
* Feature 2

## sig-platform

* New XR and OpenXRVk gems add VR support for OpenXR compatible devices. https://github.com/o3de/o3de/issues/12372  
	* Added support for Meta Quest 2 using a new multi-view render pipeline with simplified render passes for VR devices.
	* O3DE levels run on Meta Quest 2 in two ways: natively on device or from PC transmitting to device via Link cable.  
	* O3DE editor's game mode runs on Meta Quest 2 (Link cable only), allowing to immediately experience in VR the changes done to your levels.  
	* New 'XR Camera Movement' component provides head-tracking camera movement and basic VR controller input to navigate through a level.  
	* Added OpenXRTest project with test levels (DefaultLevel and XR_Office) ready to run on Meta Quest 2.
	* Documented how to build and run OpenXR in O3DE (https://github.com/o3de/o3de-extras/wiki/Build-and-Run-OpenXR-in-O3DE), how to do profiling on Meta Quest 2 (https://github.com/o3de/o3de-extras/wiki/Profiling-tools-for-Meta-Quest-2) and how to do advanced GPU profiling on Meta Quest 2 (https://github.com/o3de/o3de-extras/wiki/Advanced-GPU-profiling-tools-for-Meta-Quest-2).


## sig-security

* Feature 1
* Feature 2

## sig-simulation

* Add support for PhysX 5.1 ([#13624](https://github.com/o3de/o3de/issues/13624)) (_see Known Issues and New and Noteworthy for details_)
	* O3DE now comes with optional support for PhysX 5.1 (PhysX 5.1 is off by default but may be enabled with `-DAZ_USE_PHYSX5=ON` when building O3DE). PhysX 5.1 brings a host of performance improvements as well as several new features.
* Add support for compliant contacts ([#14852](https://github.com/o3de/o3de/issues/14852) - PhysX 5.1 only)
	* By using compliant contacts rigid bodies are able to model the way materials compress under collision. This is particularly important in fields such as robotics.
* Streamline PhysX Workflow UX ([#10668](https://github.com/o3de/o3de/issues/10668)) (_see Upgrade Steps section for details)_
	* A number of changes were made to clarify various PhysX authoring workflows. These included:
		* Make it easier for customers to understand static vs dynamic rigid bodies ([#14418](https://github.com/o3de/o3de/pull/14418))
			* Introduced a new Static Rigid Body Component to make a clearer distinction between dynamic and static colliders. New terminology was also introduced to distinguish kinematic or simulated dynamic rigid bodies.
		* Make it easier to author PhysX colliders ([#14850](https://github.com/o3de/o3de/pull/14850), [#14926](https://github.com/o3de/o3de/pull/14926), [#14907](https://github.com/o3de/o3de/issues/14907), [#14997](https://github.com/o3de/o3de/pull/14997))
			* Split the existing PhysX Collider in to PhysX Primitive Collider and PhysX Mesh Collider. This made creating simple colliders faster (e.g. Box/sphere/capsule etc...) and separated the more complex case that requires a PhysX Mesh Asset (.pxmesh product) to be created in FBX Settings.
			* PhysX Mesh Collider component card shows the collider shape type of the PhysX Mesh Asset.
			* Fixed Asset Scale in PhysX Mesh Collider component when asset used is exported as primitives.
		* Improve UX for rigid body component card ([#14024](https://github.com/o3de/o3de/pull/14024), [#13890](https://github.com/o3de/o3de/pull/13890), [#13557](https://github.com/o3de/o3de/pull/13557))
			* A number of small quality of life improvements to make the rigid body component card easier to use and understand.
		* Added support for ‘Coordinate System Change’ modifier to PhysX tab in Scene Settings. ([#14649](https://github.com/o3de/o3de/issues/14649))
* Shape Offset Support ([#12370](https://github.com/o3de/o3de/issues/12370))
	* A significant change to how several (box, capsule and sphere) shape components define their dimensions. A new ‘offset’ property has been introduced to provide support for asymmetrical editing (e.g. Moving one side of a box does not also change the other). This dramatically improves the authoring experience of manipulating shapes. Component Modes supporting manipulators and 3D viewport editing have also been added.
* Animation Asset Import Improvements ([#12387](https://github.com/o3de/o3de/issues/12387))
	* A number of quality of life improvements to the animation import process to make the overall experience more robust and straightforward.
* Animation Editor Unified Inspector Window ([#10666](https://github.com/o3de/o3de/issues/10666))
	*  A significant overhaul was made to the O3DE Animation Editor UI to bring it more inline with other O3DE tools. Numerous panels were either combined or removed to improve usability and consistency.
* Animation Editor AnimGraph Performance Visualizer ([#13490](https://github.com/o3de/o3de/pull/13490))
	* Added an option to display timing information for nodes in an AnimGraph to give real-time information on how long each node is taking to process. This gives invaluable information when profiling/optimizing an AnimGraph. _A big thank to our friends at FragLab for contributing this feature back to O3DE_.
* Character Performance Improvements ([#13920](https://github.com/o3de/o3de/pull/13920), [#14461](https://github.com/o3de/o3de/pull/14461))
	* Improved performance in several character systems.
* Physics Profiling and Performance Improvements ([#13169](https://github.com/o3de/o3de/pull/13169), [#13258](https://github.com/o3de/o3de/pull/13258), [#13061](https://github.com/o3de/o3de/pull/13061), [#13021](https://github.com/o3de/o3de/pull/13021), [#14666](https://github.com/o3de/o3de/pull/14666), [#14350](https://github.com/o3de/o3de/pull/14350))
* Physics Viewport Improvements ([#14199](https://github.com/o3de/o3de/pull/14199))
	* Physics colliders can now be clicked and selected in the 3D viewport
* Add support for reduced coordinate articulations ([#14851](https://github.com/o3de/o3de/issues/14851) - PhysX 5.1 only)
	* Reduced coordinate articulations are incredibly important for both robust and accurate simulation of joints. They are used extensively in robotics simulations when simulating devices such as a robotic arm.
	* This feature is in an early experimental state and must be enabled in the Settings Registry option: `/Amazon/Physics/EnableReducedCoordinateArticulations`
* PhysX simulation runs on multiple threads on Linux. ([#14075](https://github.com/o3de/o3de/pull/14075))
* Removed deprecated Physics and Blast legacy materials. ([#9840](https://github.com/o3de/o3de/issues/9840), [#9839](https://github.com/o3de/o3de/issues/9839))
* Blast Gem moved to experimental branch in o3de-extras. ([#13584](https://github.com/o3de/o3de/pull/13584))

## sig-testing

* Feature 1
* Feature 2

## sig-ui-ux
* Feature 1
* Feature 2

## Known Issues

* Levels and prefabs containing Polygon Prism components need to be re-saved when switching from PhysX 4 to PhysX 5.1 and vice versa.

## New and Noteworthy

* PhysX 5.1 shows a 15% increase in simulation performance compared with PhysX 4.
* With PhysX 5.1, mobile assets now use the more optimal structure eBVH34.

## Upgrade Steps

*   [#10668](https://github.com/o3de/o3de/issues/10668) - Static Rigid Body ([#14418](https://github.com/o3de/o3de/pull/14418)) and Dynamic and Static Collider Change ([#14850](https://github.com/o3de/o3de/pull/14850))
	*    See [upgrade steps](https://github.com/o3de/o3de/issues/10668#issuecomment-1476180502).
