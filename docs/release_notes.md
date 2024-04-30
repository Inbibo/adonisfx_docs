# Release Notes

## Version 1.0.2

### Improvements

- Optimized the debugger system to increase the performance especially in complex scenes with multiple deformers debugging information at the same time. *AdonisFX-1110*
- Extended the licensing tools to support Trial Extension requests. *AdonisFX-1108*

### Bug Fixes

- Fixed a bug that was crashing Maya on startup if the plugin was configured to auto load during the trial period. *AdonisFX-1097*

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
- The debugger system draws debug data independently to the visibility of the mesh. *AdonisFX-802*
- Enabling and disabling fibers display from the AdonisFX menu does not restore the previous status of the debug settings of the affected deformers. *AdonisFX-998*
- The AdonisFX Paint Tool does not refresh the painted maps if the attachments or the slide on segment constraints are removed while the tool is opened. Restarting the tool is needed. *AdonisFX-999*
- The AdnLocatorRotation does not draw the angle shape if the three inputs (start, mid and end positions) are aligned, i.e. when the angle is 180 degrees. *AdonisFX-1000*
- The Importer tool creates and configures the deformers assuming that all the required inputs exist in the scene. If any of those is not found (e.g. target mesh in AdnSkin), they have to be reassigned to an existing object manually. *AdonisFX-1001*
