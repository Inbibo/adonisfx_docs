# Release Notes

## Version 1.1.0

### Bug Fixes

- Filtered characters to get valid identifiers in Maya for Linux. *AdonisFX-1033*
- Fixed element selection check at node creation. *AdonisFX-1031*
- Fixed error messages not displaying the proper status of the AdnSimshape collider connections. *AdonisFX-1034*
- Prevent AAD file export if there is nothing to export or the only thing to export failed. *AdonisFX-1032*
- Fixed manipulation of referenced nodes while using the AdonisFX paint tool. *AdonisFX-1147*
- Fixed a bug that did not allow to add attachments on a muscle deformer created on referenced geometry. *AdonisFX-506*
- Fixed import of the constraint weight arrays on sparse arrays. *AdonisFX-1155*
- Fixed a bug that caused geometry sliding constraints to not find valid triangles to slide on initialization. *AdonisFX-1165*
- Fixed paint flood operation not working correctly for multi influence constraints. *AdonisFX-1146*

### Features

- Extended AdonisFX menu with *Documentation*, *Tutorials* and *About* sections. *AdonisFX-1095*
- Added the ability to prevent the debugging of features if the geometry is not visible, hidden or isolated. *AdonisFX-802*
- Added a warning dialog in AdnSkin and AdnSimshape when the *Max Sliding Distance* is considered too high for a mesh, which could freeze Maya. *AdonisFX-997*, *AdonisFX-466*
- Added the ability to debug the *Sliding Surface* in AdnSkin and AdnSimshape. *AdonisFX-997*, *AdonisFX-466*
- Added attachment to geometry constraints to AdnMuscle and AdnRibbonMuscle, allowing the muscle to be attached directly to a geometry. *AdonisFX-1081*
- Added a new AdonisFX deformer in charge of merging the results given by the skin simulation mesh and the animation mesh. *AdonisFX-1103*
- Added slide on geometry constraints to AdnMuscle and AdnRibbonMuscle, allowing the muscle to slide directly on a geometry. *AdonisFX-1140*
- Added mass support for AdnMuscle and AndRibbonMuscle deformers, allowing better control to achieve the desired results. *AdonisFX-1079*
- Added *Point Mass Mode* to AdonisFX deformers, which allows to specify either a mass per point or a density value from which point masses are computed. *AdonisFX-1079*
- Added importer/exporter support for AdnSkinMerge deformer and new constraints: attachment to geometry and slide on geometry. *AdonisFX-1142*
- Added *Refresh Debugger* utility to the AdonisFX menu to create missing debug nodes and connections. *AdonisFX-1171*

## Version 1.0.3

### Bug Fixes

- Fixed a bug that caused muscles simulation to fail in very specific scenarios due to a precision issue in the initialization of Slide On Segment constraints. *AdonisFX-1138*

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
- Fixed a bug in the validation of floating licenses that was preventing to load the plugin without admin permissions. *AdonisFX-724*
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
- Propietary set of constraints integrated in AdonisFX solvers:
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

- A deformers specialised for each AdonisFX solver:
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
- A debugger system compound by an AdnData node and an AdnDebugLocator to visualize information internal to the solvers such as connections to attachments, fiber directions, etc.

### Known Limitations

- The *Max Sliding Distance* parameter in AdnSkin and AdnSimshape is represented in scene units. The higher this value is, the more units in the space the sliding constraint allows a vertex to slide on. If the polygons of the target geometry to slide on are very little compared to that value, then the sliding constraint will be time and memory consuming. *AdonisFX-997*
- The activations debugger in AdnSimshape is limited to the Parallel and Serial evaluation modes. *AdonisFX-1026*
