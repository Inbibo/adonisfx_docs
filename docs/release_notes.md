# Release Notes

## Version 1.1.0

### Core

- Attachment to geometry constraints in AdnMuscle and AdnRibbonMuscle solvers. Multiple target geometries are supported.
- Slide on geometry constraints in AdnMuscle and AdnRibbonMuscle solvers. Multiple target geometries are supported.
- Point mass support integrated in all solvers to control the dynamics of the system.

### Maya

- Added AdnSkinMerge deformer to blend the results from animated and simualted input geometries.
- Added support for attachment to geometry in AdnMuscle and AdnRibbonMuscle solvers.
- Added support to slide on geometry in AdnMuscle and AdnRibbonMuscle solvers.
- Added mass attributes in AdnMuscle and AndRibbonMuscle deformers to provide more control over the dynamics of the simulated object.
- Added *Point Mass Mode* to AdnSimshape, AdnSkin, AdnMuscle and AdnRibbonMuscle which allows to specify either a mass per point or a density value from which point masses will be computed.
- Debugger system improved to be dependent to the visibility of the simulated geometry.
- Added a sanity check to *Max Sliding Distance* attribute to warn the user if the input value is too high for the given target mesh.
- Updated debugger system to visualize attachment to geometry constraints, slide on geometry constraints and sliding surface.
- Extended Importer and Exporter tools to support AdnSkinMerge deformer and new constraints (attachment to geometry and slide on geometry).
- Added *Refresh Debugger* utility to the AdonisFX menu to create missing debug nodes and connections.
- Extended AdonisFX menu with *Documentation*, *Tutorials* and *About* sections.

### Bug Fixes

- Filtered characters to get valid identifiers in Maya for Linux. *AdonisFX-1033*
- Fixed element selection check at node creation. *AdonisFX-1031*
- Fixed error messages not displaying the proper status of the AdnSimshape collider connections. *AdonisFX-1034*
- Prevent Exporter to generate the AAD file if there is no valid data to export. *AdonisFX-1032*
- Fixed manipulation of referenced nodes while using the AdonisFX paint tool. *AdonisFX-1147*
- Fixed a bug that did not allow to add attachments on a muscle deformer created on referenced geometry. *AdonisFX-506*
- Fixed import of the constraint weight arrays on sparse arrays. *AdonisFX-1155*
- Fixed a bug that caused geometry sliding constraints to not find valid triangles to slide on initialization. *AdonisFX-1165*
- Fixed paint flood operation not normalizing the weights properly. *AdonisFX-1146*

## Version 1.0.4

### Bug Fixes

- Updated third party libraries to address a problem in the licensing system that raised the Server Error Code 28 and prevented the activation of the product. *AdonisFX-1182*

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
- The debugger system draws debug data independently to the visibility of the mesh. *AdonisFX-802*
- Enabling and disabling fibers display from the AdonisFX menu does not restore the previous status of the debug settings of the affected deformers. *AdonisFX-998*
- The AdonisFX Paint Tool does not refresh the painted maps if the attachments or the slide on segment constraints are removed while the tool is opened. Restarting the tool is needed. *AdonisFX-999*
- The AdnLocatorRotation does not draw the angle shape if the three inputs (start, mid and end positions) are aligned, i.e. when the angle is 180 degrees. *AdonisFX-1000*
- The Importer tool creates and configures the deformers assuming that all the required inputs exist in the scene. If any of those is not found (e.g. target mesh in AdnSkin), they have to be reassigned to an existing object manually. *AdonisFX-1001*
