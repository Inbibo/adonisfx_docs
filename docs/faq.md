# Frequently Asked Questions

## Simulation

### How can I simulate muscles?

AdonisFX provides two solvers for muscle simulation. The use of one or the other depends on the necessity of simulating volume preservation. Muscles with volume preservation can be simulated with **AdnMuscle** deformer, while **AdnRibbonMuscle** is for planar muscles. For more information about a simple setup, please check their respective sections in *A Simple Setup* page.

### How can I add activation to the muscles?

In order to add activation to the muscles it is necessary to define the fibers direction. This can be achieved by: first, painting the tendon weights to generate an initial estimation of fibers direction; and second, combing the fibers to customize the final fibers flow along the surface. Once the muscle has a valid fiber direction at each vertex, then the activation attribute triggers the contraction of the fibers. Ultimately, the level of activation can be modulated by an AdonisFX sensor to connect the contraction of the muscle to the animation of the rig. For more information about connecting sensors to muscles, please check the **Connect Sensors** section in **A Simple Setup** page.

### How can I combine multiple activation values?

Multiple activation values from different AdonisFX sensors (AdnSensorPosition, AdnSensorDistance, AdnSensorRotation) can be combined into a single value using the **AdnActivation** node. This node allows overriding, adding, subtracting, multiplying and dividing multiple input activations to compute a single output value. For more details please refer to the **AdnActivation** page.

### How can I add volume gain to the muscles?

The *Volume Ratio* attribute of an AdnMuscle allows to simulate volume gain (volume ratio greater than 1) and loss (volume ratio lower than 1). The influence of this attribute depends on the value of *Volume Preservation*, where 0 means no effect, and 1 means maximum effect.

### How can I simulate interaction between muscles?

AdonisFX provides two ways of simulating muscle-to-muscle interactions:

- Using the AdnMuscle deformer. The AdnMuscle deformer allows configuring geometry targets to simulate external constraints (e.g. attachment to geometry and slide on geometry constraints). A simulated muscle can be assigned as a target to another simulated muscle in the same way as any other geometry target would be added (e.g. bones). Detailed instructions for adding and removing targets can be found in the **Advanced** section of the **AdnMuscle** page.

- Using the AdnGlue node. A set of muscles already simulated with AdnMuscle deformers can be further processed using the AdnGlue node. This node glues the muscles together, making them behave more compact and reducing large gaps thanks to the glue constraints. For more information on how to configure a simple setup, refer to **A Simple Setup** page.

### How can I simulate skin?

Skin can be simulated using the **AdnSkin** deformer. This deformer requires one or more target meshes (i.e. the fat) to drive the skin simulation and a mesh to apply the deformer to (skin mesh). For more information on how to configure a simple setup, refer to **A Simple Setup** page.

### How can I simulate fascia?

Similarly to a skin simulation setup, the fascia can be simulated using **AdnSkin** deformer as well. In this case, it is recommended to use values of *Rest Length Multiplier* lower than 1. This deformer also requires one mesh (a single target, i.e. the muscle geometries combined) or multiple meshes (multiple targets, i.e. the muscle geometries separated) to drive the simulation and a mesh to apply the deformer to (fascia geometry).

### How can I simulate fat?

Fat can be simulated using the **AdnFat** deformer. This deformer requires one base mesh (i.e. the fascia) to drive the fat simulation and a mesh to apply the deformer to (fat mesh). Both meshes must have the same vertex count and triangulation. For more information on how to configure a simple setup, refer to **A Simple Setup** page.

### Can I simulate muscles, fascia, fat and skin all coupled?

Yes, you can simulate muscles, fascia, fat and skin following these steps:

- Configure every muscle geometry with an AdnMuscle deformer.
- Optionally apply AdnGlue to reduce gaps between muscles.
- Generate the fascia geometry. Check this [answer](faq#how-can-i-generate-the-fascia-geometry) to know how to complete this step in Maya.
- Configure the fascia with an AdnSkin deformer (having the muscle geometries or the glue output as targets.) It is recommended to use values of *Rest Length Multiplier* lower than 1.
- Configure the fat with an AdnFat deformer (having the fascia as base mesh).
- Configure the skin with an AdnSkin deformer (having the fat as target).

### How can I simulate facial skin?

You can use **AdnSimshape** deformer. This deformer allows to reproduce the elasticity and the change in stiffness of a facial geometry thanks to the features of the AdnSimshape solver. Please, check **A Simple Setup** page where a simple setup is explained or the dedicated **AdnSimshape** page to know more about this solver.

### How can I add muscle activations to facial simulation?

The AdnSimshape deformer allows to add muscle activation in two ways:

 - Providing a deform mesh together with an AdonisFX Muscle Patches file previously generated using the Learn Muscle Patches tool.
 - Ingesting the activation values directly into the AdnSimshape node. These activation values can be computed from the rest mesh and the deform mesh using the AdnEdgeEvaluator node (for more information visit the **AdnEdgeEvaluator** page).

More details can be found in the **Add muscle activations** section in **A Simple Setup** page.

### How can I use Machine Learning to add muscle activations to AdnSimshape?

To add muscle activation via Machine Learning, the Learn Muscle Patches tool has to be used to generate the AdonisFX Muscle Patches file. The requirements for this tool are a neutral mesh (facial geometry at rest) and a set of target meshes with deformation representing all facial expressions to drive the learning. Go to the **Generate Muscle Patches** section in the **AdnSimshape** page to know more.

### Can I add muscle activations to AdnSimshape without an AdonisFX Muscle Patches file?

AdnSimshape allows to add muscle activation alternatively without the need for the AdonisFX Muscle Patches file. To do this, the activation values must be ingested directly into the AdnSimshape node. These activation values can be computed from the rest mesh and the deform mesh using the AdnEdgeEvaluator tool. Read how to drive the activations of AdnSimshape using AdnEdgeEvaluator in the dedicated **AdnEdgeEvaluator** page.

### For what units is AdonisFX designed?

The AdonisFX simulation engine works in centimeters. 

For example for Maya, the unit system also works internally in centimeters, disregarding any preferences set for the viewport. AdonisFX then works in centimeters in conjunction with Maya, disregarding any working units set in the Maya preferences.

For Houdini, the scene units are generally presented in meters. Given that AdonisFX works in centimeters internally, in some cases, the mesh has to be scaled accordingly to represent the right scaling. This may be one of the contributing factors to incorrect looking simulations when comparing to Maya.

For example in Maya, is typical to model creatures 10 times smaller in order to avoid precision issues. Imagine the example of a creature that is supposed to be 1.7 meters tall (170 Maya units). Then in Maya to avoid precision issues, this creature may be modeled to be 17 centimeters tall (17 Maya units).
In this case you can adjust the simulation for this scaling factor by applying the AdonisFX Space Scale attribute to 10. This will ensure that AdonisFX will scale everything internally so that the simulation of the 17 units creature will look like if it was actually 170 units tall. Similar criteria can be applied to Houdini, however, it is still advisable to check the scaling of the characters when transferring between DCCs.

### How can I transfer the results of skin simulation to the final mesh?
Make use of the **AdnSkinMerge** deformer to blend animated and simulated meshes into a single final mesh. Create and configure the node providing the final mesh and add the simulation and animation meshes. Then you only need to paint the blend weight to define the influence of the simulated mesh targets over the animated ones. You can find more information in the **AdnSkinMerge** page.

### How can I control the area in which my muscle should activate?

For muscles, controlling the area in which the muscle should activate and bulge can be achieved by painting the fibers multiplier paintable map. Painting this map allows the muscle to contract and concentrate activations in certain areas without affecting unpainted areas. For example, painting the fibers multiplier map to 0.0 in the tendinous area will concentrate activations in the belly of the muscle, which is painted with a value of 1.0, giving a more realistic and controlled look to the activation. Read how to use the fibers multiplier map in the **AdnMuscle** and **AdnRibbonMuscle** pages.

## Workflows

### Can I mirror the muscles setup?

Yes, a Python script is provided to transfer the muscle setup of an asset from left to right and vice versa. This script includes the mirroring of AdonisFX muscles, locators and sensors. It mirrors not only the scalar attributes and paintable maps, but also the connections and dependencies between all of them. Know more about the mirroring in the **Mirror** page.

### How can I generate the fascia geometry using Maya tools?

In order to obtain a plausible fascia geometry, we can use two techniques that require the muscle geometries and the skin geometry as inputs.

The first approach is to use the shrinkwrap deformer provided by Maya. This solution should produce good results for low poly geometries.

- Create a copy of the skin geometry that will become your fascia.
- Combine all muscle geometries into a single geometry. It may be advisable to include the bone geometries along with the muscles to avoid gaps.
- Select the combined muscles geometry, then select the copy of the skin geometry.
- Apply the shrinkwrap deformer and adjust its settings until the desired fascia geometry is achieved.
- Delete the history of the fascia geometry.

The second approach is to use nCloth to apply a pressured simulation. This solution could work better for high-end fascia simulations. The procedure is the following:

- Create a copy of the skin geometry that will become your fascia.
- Combine all muscle geometries into a single geometry. It may be advisable to include the bone geometries along with the muscles to avoid gaps.
- Select the fascia geometry and click nCloth > Create nCloth.
- Select the muscles geometry and click on nCloth > Create Passive Collider.
- Select the nucleus node, set the gravity to 0.0 and adjust the space scale according to your asset.
- Select the nCloth node and keyframe the pressure attribute to 0.0 at the first frame of the scene.
- Advance some frames (e.g. ten frames) and keyframe the pressure to -1.0.
- Select the fascia geometry and click nCloth > Create New nCache > nObject.
- Once the simulation finishes, choose the fascia that looks best within the simulated frame range.
- Delete the history of the fascia geometry.

As a final step for both approaches, you may want to smooth the resulting fascia geometry with sculpting tools to polish the final result.

### How can I upgrade a Maya scene from AdonisFX v1 to v2?

Go to AdonisFX menu > Utils and press *Upgrade v1.x To v2.x*. This option performs an upgrade to all AdonisFX solvers to make v1.x rigs compatible with v2.x. This upgrade affects the painted values in the maps that are affected by the *Maps Remap Mode* attribute added in v2.0.0 to all solvers (i.e., shape preservation, attachments and sliding in muscle solver, uber constraints in skin solver). Due to how this remapping modifies how the painted values from the plugs are transferred to the solver, this utility updates those values in order to get simulation results as consistent as possible with v1.x.

Additionally, since the *Concrete* material has been deprecated, this upgrade script also checks whether any nodes in the scene are using an invalid material. If an invalid material is found, it will be automatically replaced with the default material.

As a final step to support the addition of the *currentTime* plug in AdnSkinMerge we provide inside of the upgrade process a way to connect the *time1.outTime* to every node that has a *currentTime* plug.

### How can I reconnect the time to the *currentTime* plug in Maya if I had accidentally broken the connection?

Go to AdonisFX menu > Utils and press *Reconnect Current Time*. This option will search for all AdonisFX nodes in the scene with a *currentTime* plug and connect the *time1.outTime* plug to it.
This is necessary to ensure a correct cooking of the nodes.

## Cross-DCC Support

### In which scale do I have to work when transferring a rig from Maya to Houdini?
Internally, our solvers always operate in centimeters (cm) across all supported DCCs. Since Maya uses centimeters by default, while Houdini typically uses meters (1 unit = 1 meter), rigs imported into Houdini usually need to be scaled up by a factor of 100 to match Maya's simulation scale.
In some cases (for example, Houdini's Alembic SOP), this conversion may be applied automatically.
A good way to verify the correct scale in Houdini is to check the point coordinates in the *Geometry Spreadsheet*. The values should be consistent with centimeter units.

### Are there guidelines for building rigs in Houdini?
Yes. Each deformer chain affecting a single geometry must be enclosed in a deformable region.
A deformable region is defined using two SOP Null nodes with a specific naming convention:
- Start node: `ADN_IN_<geo_name>`.
- End node: `ADN_OUT_<geo_name>`.
All AdonisFX deformers affecting `geo_name` should be placed between these nodes.
This structure allows components such as the API to correctly identify which SOP nodes affect which geometries, ensuring smooth transfer to other DCCs.

### Do geometries need preprocessing in Houdini?
Yes. Before using AdonisFX:
- Geometry must be unpacked.
- PolySoup primitives are not supported and should be avoided.

### Does AdonisFX in Houdini support transforms?
No. AdonisFX operates purely in geometry (SOP) space. Any transforms applied at the object level (world transform matrices) are not supported. Make sure to apply transforms directly to point positions before processing geometry with AdonisFX.

## Debugging

### How can I change the logger level?

AdonisFX Logger has different levels of execution: (0) Debug, (1) Info, (2) Warning, (3) Error. The level is determined by an environment variable `ADN_LOGGER_LEVEL`. If not defined, AdonisFX Logger Level is set to Info by default. This allows the system to print Info, Warning and Error messages to the console. If more verbosity is required, it is possible to modify the level to Debug. For that, the environment variable `ADN_LOGGER_LEVEL` has to be set to `0`. Note that for this change to take effect, the AdonisFX plugin must be reloaded.

## Performance

### How can I control the multithreading of AdonisFX solvers?

AdonisFX nodes use multithreading based on a threshold that determines the minimum number of elements required for parallel processing. If the number of elements to process exceeds this threshold, multithreading will be applied, otherwise, the code will execute sequentially. This threshold is set to `16` by default, but can be adjusted by modifying the value of the `ADN_MIN_PARALLEL_SIZE` environment variable. Modify this value carefully, as it can improve performance in some cases but may also reduce it depending on your CPU.

## Licensing

### Does AdonisFX require internet access?
The use of AdonisFX itself does not require access to the internet but the licensing system does. In node-locked licenses, the workstation needs connection to the internet to validate the activation on plug-in load at least every 19 days. After that, the product can be used without internet connection. In floating licenses, it is the server that will need to connect to the internet at least every 19 days to validate the activation, meaning that users' workstations or nodes on farms do not need internet access.

### Can I activate the node-locked licenses offline?
No, node-locked licensing requires internet access to activate. Check the [licensing](licensing#node-locked-licensing) page for more information.

### Can I activate the floating licensing server offline?
No, floating licensing requires internet access to activate the server. To be more specific, only the machine running the server needs access, while the users' machines do not require connection to the internet. Check the [licensing](licensing#floating-licensing) page for more information.

### Can I use my node-locked license on more than one machine?
It depends on the purchased product plan. For Indie licenses, only one activation is allowed. To be able to move the license to a different machine, you will need to deactivate the license and reactivate it on the newly configured machine. Please, contact support if that is your case. For Solo licenses, up to two activations are allowed. This means that you can activate your product key in two different machines. For more flexibility and no hardware specific licensing restriction you should purchase floating licenses.

### How can I switch between node-locked licensing and floating licensing inside of AdonisFX?
You can use the environment variable `ADN_LICENSE_MODE` set to `0` for node-locked licensing and `ADN_LICENSE_MODE` set to `1` for floating licensing. The license gets verified only once when the plug-in is loaded. This means that if a change like this one needs to be applied, then the application has to be restarted to load the plug-in again from a new process.

### What do I need to be able to use floating licensing?
First of all, the licensing server has to be installed, configured and activated previously (check this [section](licensing#floating-licensing)). Then, the client machine(s) on which AdonisFX will be used have to be configured to allow them to connect to the server to request leases. The configuration simply requires to set a few environment variables: `ADN_LICENSE_MODE` to `1`; and `ADN_LICENSE_SERVER` and `ADN_LICENSE_SERVER_BATCH` to the IP address and port (e.g. `127.0.0.1:13`) of the interactive and batch floating server respectively.

### Can I move the license server to a different machine?
Yes. This process requires you to deactivate it and then activate it on the new machine. For more information visit the [licensing](licensing#activate-server) page or contact support.

### How can I change the port number of my licensing server?
Change the server `port` number in the `TurboFloatServer-config.xml` before running the server.

### I want to know more about how leases are dropped, how can I see the notifications on my server?
You can find and modify when leases are dropped inside of the `TurboFloatServer-config.xml` file. In there you can also specify where to store the log file and with which verbosity it will write to it.
For more information visit the [licensing](licensing#install-server) page or visit this [link](https://wyday.com/limelm/help/turbofloat-server/).

### I can't connect to my licensing server for floating licensing. What should I do?
Make sure that your firewall configuration allows the connection and try using the `ping` command to check the connectivity. If the connection is valid but AdonisFX can't load, please contact support.
