# Release Notes

## Version 1.5.0

### Core

- Implemented a relaxation algorithm to smooth creases, over compression and over stretching from a geometry surface.

### Maya

- Added support to Maya 2025.
- Implemented an experimental Python API.
- Implemented a mirroring script in Python to easily apply the muscle rig (muscles and sensors) from one side of the character to the other side.
- Added AdnRelax deformer to apply the relaxation algorithm.
- Added fibers multiplier map to AdnMuscle and AdnRibbonMuscle to control the distribution of the activation across the geometry muscle.
- Added a utility to create AdnActivation nodes from the menu.
- Added a utility to remove inputs from an AdnActivation node.
- Prevent painting fibers and tendons on a simulated frame.

### Improvements

- Added further optimizations to AdnSimshape solver.
- Added further optimizations to AdnSkin solver.
- Improved the automation of the Paint Tool to include the AdnDebugLocator in the current selection to easy the debugging process while painting.

### Bug Fixes

- Fixed a but that prevented the fibers flow generation by tendon weights to trigger properly after applying AdnMuscle Maya presets. *AdonisFX-1652*

### Deprecated

- The Exporter and Importer tools are deprecated and removed from the UI. The internal logic in Python is still available but it will be removed or rewritten in an upcoming release. Continuing to use it is not advisable.

### Known Limitations

- Painting functionalities on AdnGlue are not supported if other deformers are applied to the AdnGlue output mesh directly. *AdonisFX-1644*

## Version 1.4.1

### Bug Fixes

- Fixed Attribute Editor Template of AdnSimshape to merge all initialization settings into a single collapsible menu.

### Improvements

- Improved the parallelization handling in AdnSimshape solver.

## Version 1.4.0

### Core

- Implemented a new solver to glue muscles together so they behave more compact: AdnGlue solver.
- Implemented Glue constraints.
- Added parallelization to Distance constraints.
- Added parallelization to Shape Preservation constraints.
- Added Hard constraints to the AdnFat solver.
- Added control to the minimum parallelizable chunk size via the environment variable `MIN_PARALLEL_SIZE`.
- Increased the Logger verbosity in Debug level.

### Maya

- Added AdnGlue node.
- Added AdnActivation node.
- Added support to unidirectional muscle to muscle constraints.
- Added support to Hard Constraints in AdnFat solver including paintable map and stiffness override.
- Optimized AdnFat deformer.
- Optimized AdnSkin deformer.
- Optimized AdonisFX Paint Tool.
- Added color interpolation to the fibers debugger in AdnMuscle and AdnRibbonMuscle to encode the muscle activation.
- Deprecated AdnWeightsDisplayNode.
- Added a shortcut in the AdonisFX menu to upgrade deprecated nodes.
- Added the ability to choose which constraints reinitialize at start time.


### Bug Fixes

- Fixed the solvers at start time to first compute one simulation step and then reinitialize the system. *AdonisFX-1445*
- Fixed a bug in the normalization of the paintable weights on initialization to dump the resulting weights. *AdonisFX-1438*
- Fixed a bug that was preventing the debugger from working if there were any intermediate nodes between the AdonisFX deformer and the shape node. *AdonisFX-1478*
- Fixed a Maya crash when reopening a scene that was saved with an AdonisFX deformer disabled. *AdonisFX-1483*
- Fixed fiber’s direction initialization at start time. *AdonisFX-1499*
- Fixed a bug in the Volume Constraint that was causing flickering if the simulated geometry was far from the center of the world. *AdonisFX-1489*
- Fixed the internal bounding box construction at start time to use the current point positions instead of the point positions at rest. *AdonisFX-1511*

### Deprecated

- The AdnWeightsDisplayNode is deprecated. This deprecation is fully backward-compatible, ensuring that scenes created in earlier versions will work as expected in version 1.4.0. To safely remove deprecated nodes from your scenes, a utility is added in AdonisFX Menu > Utils > *Upgrade Deprecated Nodes*.

### Known Limitations

- Undoing the removal of inputs in AdnGlue does not restore the previous painted weights. *AdonisFX-1523*

## Version 1.3.1

### Improvements

- Improved the floating licensing setup to allow connection with both interactive and batch servers without the need of a switch in the environment configuration. This change is fully backward compatible. *AdonisFX-1384*

## Version 1.3.0

### Core

- Implemented a new solver for fat simulation.
- Implemented a new constraint to preserve the internal shape of fat tissue.
- Implemented a new constraint to preserve the volume of fat tissue.
- Extended all existing solvers to support stiffness overrides per constraint type.

### Maya

- Added AdnFat deformer.
- Added stiffness overrides per constraint type to all deformers.
- Implemented dynamic loading of AdonisFX shelf and removed the `MAYA_SHELF_PATH` configuration from the module file.
- Improved UX to prevent informative dialogs to prompt.
- Improved UX to prevent dialogs to prompt when running commands from script.

### Bug Fixes

- Fixed a bug that was redistributing the masses per point in very specific cases and only if the painted masses map was not the default one.
- Fixed a bug that was causing the velocity damping not to work when point masses were too large.

### Known Limitations

- Interaction muscle-to-muscle is not supported. *AdonisFX-1211*
- Exporter and Importer do not support locators and sensors. *AdonisFX-1215*

## Version 1.2.0

### Core

- Added support for multiple targets in AdnSkin solver.
- Extended the uber constraints initialization to build constraints with the closest point on the closest target.
- Allow all the solvers to use the internal triangulation of the geometry to build the constraints.
- Extended the distance, fiber and shape preservation constraints initialization to build constraints based on the triangulated mesh.
- Added support in AdnSkin solver to simulate even if no targets are provided.

### Maya

- Added *Targets* array plug to AdnSkin deformer to connect multiple targets.
- Added *Triangulate Mesh* option to all AdonisFX deformers to enable or disable the use of the triangulated version of the mesh for building the constraints.
- Added two new buttons to the shelf and two new entries in the menu to add and remove targets from an AdnSkin deformer.
- Added support for debugging distance and fiber constraints.

### Known Limitations

- Slide on geometry constraints in Fast mode are limited to simple setups. They need to run in Quality mode to ensure stability in complex scenarios. *AdonisFX-1213*
- Volume ratio gain effect is dependent on the total volume of the muscle. This might require using volume ratios with a range different to the default [0, 2] if needed. *AdonisFX-1137*
- Interaction muscle-to-muscle is not supported. *AdonisFX-1211*
- Exporter and Importer do not support locators and sensors. *AdonisFX-1215*
- Fat simulation is limited to the current features in AdnSkin solver. *AdonisFX-879*

## Version 1.1.2

### Bug Fixes

- Fixed a bug in the Slide Collision Constraints that was overcorrecting in case of intersection with the collider with a magnitude greater than the collision threshold. *AdonisFX-1258*

## Version 1.1.1

### Bug Fixes

- Fixed a bug in how gravity was evaluated. Now the value from the UI represented in m/s<sup>2</sup> is converted to cm/s<sup>2</sup>. *AdonisFX-1250*

### Considerations for backward compatibility

- Due to the fix introduced in this version, in order to have the scenes created with previous versions work the same way, it is needed to set the gravity value in all AdonisFX nodes divided by 100. For example, if the AdonisFX setup in v1.1.0 (or older) used a gravity of 980, now this attribute needs to be changed to 9.8. If the setup did not use gravity, no adjustment needs to be done.

## Version 1.1.0

### Core

- Attachment to geometry constraints in AdnMuscle and AdnRibbonMuscle solvers. Multiple target geometries are supported.
- Slide on geometry constraints in AdnMuscle and AdnRibbonMuscle solvers. Multiple target geometries are supported.
- Shape preservation constraints integrated in AdnMuscle, AdnRibbonMuscle, AdnSkin and AdnSimshape solvers.
- Point mass support integrated in AdnMuscle and AdnRibbonMuscle to control the dynamics of the system.
- Compute point mass distribution based on the density and volume or area.

### Maya

- Added AdnSkinMerge deformer to blend the results from animated and simulated input geometries.
- Added support for attachment to geometry in AdnMuscle and AdnRibbonMuscle solvers.
- Added support to slide on geometry in AdnMuscle and AdnRibbonMuscle solvers.
- Added support for shape preservation in AdnMuscle, AdnRibbonMuscle, AdnSkin and AdnSimshape solvers.
- Added mass attributes in AdnMuscle and AndRibbonMuscle deformers to provide more control over the dynamics of the simulated object.
- Added *Point Mass Mode* to AdnSimshape, AdnSkin, AdnMuscle and AdnRibbonMuscle which allows to specify either a mass per point or a density value from which point masses will be computed.
- The debugger system improved to be dependent on the visibility of the simulated geometry.
- Added a sanity check to *Max Sliding Distance* attribute to warn the user if the input value is too high for the given target mesh.
- Updated debugger system to visualize attachment to geometry constraints, slide on geometry constraints, shape preservation constraints and sliding surface.
- Extended Importer and Exporter tools to support AdnSkinMerge deformer and new constraints (attachment to geometry and slide on geometry).
- Added *Refresh Debugger* utility to the AdonisFX menu to create missing debug nodes and connections.
- Allow source nodes of any type in the *Sensors Connection Editor*.
- Extended AdonisFX menu with *Documentation*, *Tutorials* and *About* sections.

### Bug Fixes

- Fixed AdonisFX Paint Tool initialization of simulated nodes with intermediate nodes. *AdonisFX-1184*
- Fixed a bug that caused sliding constraints to not find valid triangles to slide on if the initial closest point on the target lies on an edge. *AdonisFX-1165*
- Fixed importer to support sparse array maps. *AdonisFX-1155*
- Fixed manipulation of referenced nodes while using the AdonisFX paint tool. *AdonisFX-1147*
- Fixed paint flood operation not normalizing the weights properly. *AdonisFX-1146*
- Fixed error messages not displaying the proper status of the AdnSimshape collider connections. *AdonisFX-1034*
- Filtered characters to get valid identifiers when creating nodes with a custom name in Linux. *AdonisFX-1033*
- Prevent Exporter from generating the AAD file if there is no valid data to export. *AdonisFX-1032*
- Fixed a bug that did not allow adding attachments on a muscle deformer created on referenced geometry. *AdonisFX-506*

### Known Limitations

- Slide on geometry constraints in Fast mode are limited to simple setups. They need to run in Quality mode to ensure stability in complex scenarios. *AdonisFX-1213*
- Volume ratio gain effect is dependent on the total volume of the muscle. This might require using volume ratios with a range different to the default [0, 2] if needed. *AdonisFX-1137*
- Interaction muscle-to-muscle is not supported. *AdonisFX-1211*
- Exporter and Importer do not support locators and sensors. *AdonisFX-1215*
- Fat simulation is limited to the current features in AdnSkin solver. *AdonisFX-879*

## Version 1.0.4

### Bug Fixes

- Updated third party libraries to address a problem in the licensing system that raised the Server Error Code 28 and prevented the activation of the product. *AdonisFX-1182*

## Version 1.0.3

### Bug Fixes

- Fixed a bug that caused muscle simulation to fail in very specific scenarios due to a precision issue in the initialization of Slide On Segment constraints. *AdonisFX-1138*

### Improvements

- Improved the update of painted maps for Attachments and Slide On Segment constraints at initialization. *AdonisFX-1136*

## Version 1.0.2

### Bug Fixes

- Fixed a bug that was crashing Maya on startup if the plugin was configured to auto load during the trial period. *AdonisFX-1097*
- Fixed the debugger system where the performance was limited in complex scenes with multiple deformers debugging information at the same time. *AdonisFX-1110*

### Improvements

- Extended the licensing system to support Trial Extension requests. *AdonisFX-1108*

## Version 1.0.1

### Bug Fixes

- Fixed a bug that was making Maya freeze when creating an AdnSkin deformer with the playback cache enabled. *AdonisFX-1087*
- Fixed a bug in the validation of floating licenses that was preventing loading the plugin without admin permissions. *AdonisFX-724*
- Fixed a bug that was preventing the licensing system to locate the licensing configuration file properly in some cases. *AdonisFX-1072*
- Fixed a bug in the AdnSimshape activations debugger to support DG evaluation mode. *AdonisFX-1026*
- Fixed a bug in the importer tool where it was attempting to assign a string value to a matrix plug. *AdonisFX-1090*
- Fixed the *Draw Fibers* and *Hide Fibers* shortcuts to be undoable and avoid affecting muscles that are debugging other features different to fibers. *AdonisFX-998*
- Fixed the *Remove Attachments* and *Remove Slide On Segment Constraint* shortcuts to prevent the user to remove attachments and segments that are currently in use by the AdonisFX Paint Tool. *AdonisFX-999*
- Fixed the AdnLocatorRotation to draw a valid angle shape if the three inputs (start, mid and end positions) are aligned. *AdonisFX-1000*
- Fixed the importer tool to run a validation before creating a deformer whose minimum requirements can't be found in the scene. *AdonisFX-1001*


## Version 1.0.0

### Core

- Solver for skin simulation.
- Solver for volumetric and planar muscle simulation.
- Solver for facial simulation.
- Proprietary set of constraints integrated in AdonisFX solvers:
    - Fibers contraction
    - Volume preservation
    - Attachments
    - Slide on segment
    - Slide on surface
    - Soft constraint on polygon
    - Hard constraint on polygon
    - Slide collision on surface
- A Machine Learning module to extract facial muscles data and their fiber directions from a set of facial expressions.

### Maya

- A deformers specialized for each AdonisFX solver:
    - AdnSkin
    - AdnMuscle
    - AdnRibbonMuscle
    - AdnSimshape
- Nodes to evaluate relative distances, angles, velocities and accelerations between transform nodes in the scene: AdnSensorPosition, AdnSensorDistance, AdnSensorRotation.
- Locators to visualize relative distances, angles, velocities and accelerations between transform nodes in the scene: AdnLocatorPosition, AdnLocatorDistance, AdnLocatorRotation.
- Plain AdnLocator with a custom shape for visualization purposes.
- AdnEdgeEvaluator: A node to compute the compression map of a deformed geometry.
- AdnWeightsDisplayNode: A node to visualize the paintable maps while painting from the AdonisFX Paint Tool.
- AdnLearnMusclePatches: Command to execute the ML process for facial muscles generation.
- Learn Muscle Patches Tool: An intuitive UI to configure and run the AdnLearnMusclePatches command.
- Sensors Connection Editor: A simple UI to make connections easily from sensors and locators to AdonisFX deformers.
- AdonisFX Paint Tool: Custom tool to manipulate the paintable maps of the AdonisFX deformers to ensure that the solvers receive valid distribution of weights.
- A debugger system composed by an AdnData node and an AdnDebugLocator to visualize information internal to the solvers such as connections to attachments, fiber directions, etc.

### Known Limitations

- The *Max Sliding Distance* parameters in AdnSkin and AdnSimshape are represented in scene units. The higher this value is, the more units in the space the sliding constraint allows a vertex to slide on. If the polygons of the target geometry to slide on are very little compared to that value, then the sliding constraint will be time and memory consuming. *AdonisFX-997*
- The activations debugger in AdnSimshape is limited to the Parallel and Serial evaluation modes. *AdonisFX-1026*
- The debugger system draws debug data independently to the visibility of the mesh. *AdonisFX-802*
- Enabling and disabling fibers display from the AdonisFX menu does not restore the previous status of the debug settings of the affected deformers. *AdonisFX-998*
- The AdonisFX Paint Tool does not refresh the painted maps if the attachments or the slide on segment constraints are removed while the tool is opened. Restarting the tool is needed. *AdonisFX-999*
- The AdnLocatorRotation does not draw the angle shape if the three inputs (start, mid and end positions) are aligned, i.e. when the angle is 180 degrees. *AdonisFX-1000*
- The Importer tool creates and configures the deformers assuming that all the required inputs exist in the scene. If any of those is not found (e.g. target mesh in AdnSkin), they have to be reassigned to an existing object manually. *AdonisFX-1001*
