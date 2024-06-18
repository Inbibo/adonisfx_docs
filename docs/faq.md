# Frequently Asked Questions

## How can I simulate muscles?

AdonisFX provides with two solvers for muscle simulation. The use of one or the other depends on the necessity of simulating volume preservation. In Maya, muscles with volume preservation can be simulated with [AdnMuscle](maya/muscle) deformer, while [AdnRibbonMuscle](maya/ribbon) is for planar muscles. For more information about a simple setup, please check their respective sections in this [page](maya/simple_setup).

## How can I add activation to the muscles?

In order to add activation to the muscles it is necessary to define the fibers direction. This can be achieved by: first, painting the tendon weights to generate an initial estimation of fibers direction; and second, combing the fibers through the AdonisFX Paint Tool to customise the final fibers flow along the surface. Once the muscle has a valid fiber direction at each vertex, then the activation attribute triggers the contraction of the fibers. Ultimately, the level of activation can be modulated by an AdonisFX sensor to connect the contraction of the muscle to the animation of the rig. For more information about connecting sensors to muscles, please check this [section](maya/simple_setup#connect-sensors).

## How can I add volume gain to the muscles?

The *Volume Ratio* attribute of an AdnMuscle allows to simulate volume gain (volume ratio greater than 1) and loss (volume ratio lower than 1). The influence of this attribute depends on the value of *Volume Preservation*, where 0 means no effect, and 1 means maximum effect.

## How can I simulate skin?

Skin can be simulated using the [AdnSkin](maya/skin) deformer. This deformer requires a reference mesh to drive the skin simulation (i.e. the fascia) and a mesh to apply the deformer to (skin mesh). A simple setup is explained [here](maya/simple_setup#adnskin).

## How can I simulate fascia?

Similarly to a skin simulation setup, the fascia can be simulated using [AdnSkin](maya/skin) deformer as well. In this case, it is recommended to use values of *Rest Length Multiplier* lower than 1. This deformer also requires a mesh to drive the simulation (one reference mesh, i.e. the internal muscle geometries combined) and a mesh to apply the deformer to (fascia geometry).

## Can I simulate muscles, fascia and skin all coupled?

Yes, you can simulate muscles, fascia and skin following these steps:

- Configure every muscle geometry with an AdnMuscle deformer.
- Combine all muscle geometries into a single geometry.
- Shrinkwrap the skin geometry to the combined muscles geometry to obtain the fascia geometry.
- Configure the fascia with an AdnSkin deformer: Select the combined muscles geometry, then the fascia geometry and then create the skin deformer. It is recommended to use values of *Rest Length Multiplier* lower than 1.
- Configure the skin with an AdnSkin deformer: Select the fascia, then the skin geo and then create the skin deformer.

## How can I simulate facial skin?

You can use [AdnSimshape](maya/simshape) deformer. This deformer allows to reproduce the elasticity and the change in stiffness of a facial geometry thanks to the features of the AdnSimshape solver. Please, check this [section](maya/simple_setup#adnsimshape) where a simple setup is explained or this [page](maya/simshape) to know more about this solver.

## How can I add muscle activations to facial simulation?

The AdnSimshape deformer allows to add muscle activation in two ways:

 - Providing a deform mesh together with an AdonisFX Muscle Patches file previously generated using the Learn Muscle Patches tool.
 - Plugging the activation values directly into the *ActivationList.Activation* attribute. These activation values can be computed from the rest mesh and the deform mesh using the AdnEdgeEvaluator node (visit this [page](maya/edge_evaluator)).

More details can be found [here](maya/simple_setup#add-muscle-activations).

## How can I use Machine Learning to add muscle activations to AdnSimshape?

To add muscle activation via Machine Learning, the Learn Muscle Patches tool has to be used to generate the AdonisFX Muscle Patches file. The requirements for this tool are a neutral mesh (facial geometry at rest) and a set of target meshes with deformation representing all facial expressions to drive the learning. Follow this [link](maya/simshape#generate-muscle-patches) to know more.

## Can I add muscle activations to AdnSimshape without an AdonisFX Muscle Patches file?

AdnSimshape allows to add muscle activation alternatively without the need for the AdonisFX Muscle Patches file. To do this, the activation values must be plugged directly into the *ActivationList.Activation* attribute. These activation values can be computed from the rest mesh and the deform mesh using the AdnEdgeEvaluator tool. Read how to drive the activations of AdnSimshape using AdnEdgeEvaluator [here](maya/edge_evaluator#how-to-use).

## Can I transfer AdonisFX nodes configuration to a different asset?

Yes, you can use the AdonisFX [Exporter](maya/tools#exporter) and [Importer](maya/tools#importer) Tools to generate and load respectively an AdonisFX Asset Definition (AAD) file. From an scene with an asset fully configured with AdonisFX deformers, you can select the parent transform object and launch the Exporter. From there, you can decide which settings to export and the destination path for the AAD file. Then, in a different scene with a compatible asset, you can launch the Importer, browse the AAD file and assign deformers from the file to the meshes in the hierarchy of the asset.

## For what units is AdonisFX designed?

AdonisFX solvers interpret input units as meters. In order to simulate external forces like gravity with realism, you need to take some considerations into account:

 - If Maya preferences are configured in centimeters, then all distances in the viewport are measured in centimeters. In this scenario, a gravity magnitude of 9.8 means that the effective gravity of the system is 9.8 cm/s<sup>2</sup>. To make this value equivalent to the Earth's gravity you have to either set the space scale to 0.01 or alternatively, change the gravity to 980. Both methods will make AdonisFX use a gravity of 9.8 m/s<sup>2</sup>.
 - If Maya preferences are cofnigured in meters, then all distances in the viewport are measured in meters. In this scenario, a gravity magnitude of 9.8 corresponds to the Earth's gravity and no further adjustments are needed.
 - For realistic results, ensure that the AdonisFX gravity and space scale settings are coherent with the scale of the character and the Maya scene units.
 - It is not mandatory to use a factor of 9.8 for the gravity. AdonisFX solvers are not restrictive in this regard. Sometimes, if you aim for a creative and artistic effect, you can experiment with different values.

## Does AdonisFX require internet access?
The use of AdonisFX itself does not require access to the internet but the licensing system does. In node-locked licenses, the workstation needs connection to the internet to validate the activation on plug-in load at least every 19 days. After that, the product can be used without internet connection. In floating licenses, it is the server that will need to connect to the internet at least every 19 days to validate the activation, meaning that users' workstations or nodes on farm do not need internet access.

## Can I activate node-locked licenses offline?
No, node-locked licensing requires internet access to activate. Check the [licensing](licensing#node-locked-licensing) page for more information.

## Can I activate floating licensing server offline?
No, floating licensing requires internet access to activate the server. To be more specific, only the machine running the server needs access, while the users' machines do not require connection to the internet. Check the [licensing](licensing#floating-licensing) page for more information.

## Can I use my node-locked license on more than one machine?
It depends on the purchased product plan. For Indie licenses, only one activation is allowed. To be able to move the license to a different machine, you will need to deactivate the license and reactivate it on the newly configured machine. Please, contact support if that is your case. For Solo licenses, up to two activations are allowed. This means that you can activate your product key in two different machines. For more flexibility and no hardware specific licensing restriction you should purchase floating licenses.

## How can I switch between node-locked licensing an floating licensing inside of AdonisFX?
You can use the environment variable `ADN_LICENSE_MODE` set to `0` for node-locked licensing and `ADN_LICENSE_MODE` set to `1` for floating licensing.

## What do I need to be able to use floating licensing?
You will need to configure and activate the licensing server, make sure that client machines have access to it.

## Can I move the license server to a different machine?
Yes. This process requires you to deactivate it and then activate it on the new machine. For more information visit the [licensing](licensing#activate-server) page or contact support.

## How can I change the port number of my licensing server?
Change the server `port` number in the `TurboFloatServer-config.xml` before running the server.

## I want to know more about how leases are dropped, how can I see the notifications in my server?
You can find and modify when leases are dropped inside of the `TurboFloatServer-config.xml` file. In there you can also specify where to store the log file and with which verbosity it will write to it.
For more information visit the [licensing](licensing#install-server) page or visit this [link](https://wyday.com/limelm/help/turbofloat-server/).

## I can't connect to my licensing server for floating licensing. What should I do?
Make sure that your firewall configuration allows the connection and try using the `ping` command to check the connectivity. If the connection is valid but AdonisFX can't load, please contact support.

## How can I transfer the results of skin simulation to the final mesh?
Make use of the [AdnSkinMerge](maya/skin_merge) deformer to blend animated and simulated meshes into a single final mesh. Launch the Skin Merge tool, select the final mesh, add the animated and simulated target meshes and click on Create. Then you only need to paint the blend weight to define the influence of the simulated mesh targets over the animated ones. You can find more information [here](maya/simple_setup#adnskinmerge).
