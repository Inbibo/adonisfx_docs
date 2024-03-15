# Frequently Asked Questions

## How can I simulate muscles?

Adonis provides with two solvers for muscle simulation. The use of one or the other depends on the necessity of simulating volume preservation. In Maya, muscles with volume preservation can be simulated with [AdnMuscle](maya/muscle.md) deformer, while [AdnRibbonMuscle](maya/ribbon.md) is for planar muscles. For more information about connecting sensors to muscles, please check [how to set up AdnMuscle](maya/simple_setup.md#adnmuscle-simple-setup) and [how to set up AdnRibbonMuscle](maya/simple_setup.md#adnribbonmuscle-simple-setup).

## How can I add activation to the muscles?

In order to add activation to the muscles it is necessary to define the fibers direction. This can be achieved by: first, painting the tendon weights to generate an initial estimation of fibers direction; and second, combing the fibers through the AdonisFX Paint Tool to customize the final fibers flow along the surface. Once the muscle has a valid fiber direction at each vertex, then the [*Activation*](maya/muscle.md#solver-attributes) attribute triggers the contraction of the fibers. Ultimately, the level of activation can be modulated by an Adonis sensor to connect the contraction of the muscle to the animation of the rig. For more information about connecting sensors to muscles, please check [how to set up AdnMuscle](maya/simple_setup.md#adnmuscle-simple-setup) and [how to set up AdnRibbonMuscle](maya/simple_setup.md#adnribbonmuscle-simple-setup).

## How can I add volume gain to the muscles?

The [*Volume Ratio*](maya/muscle.md#solver-attributes) attribute of an AdnMuscle allows to simulate volume gain (volume ratio greater than 1) and loss (volume ration lower than 1). The influence of this attribute depends on the value of *Volume Preservation*, where 0 means no effect, and 1 means maximum effect.

## How can I simulate skin?

Skin can be simulated using the [AdnSkin](maya/skin.md) deformer. This deformer requires a reference mesh to drive the skin simulation (i.e. the fascia) and a mesh to apply the deformer to (skin mesh). For more information please check [how to set up AdnSkin](maya/simple_setup.md#adnskin-simple-setup).

## How can I simulate fascia?

Similarly to a skin simulation setup, the fascia can be simulated using [AdnSkin](maya/skin.md) deformer as well. In this case, it is recommended to use values of *Rest Length Multiplier* lower than 1. This deformer also requires a mesh to drive the simulation (one reference mesh, i.e. the internal muscle geometries combined) and a mesh to apply the deformer to (fascia geometry).

## Can I simulate muscles, fascia and skin all coupled?

Yes, you can simulate muscles, fascia and skin following these steps:

- Configure every muscle geometry with an AdnMuscle deformer.
- Combine all muscle geometries into a single geometry.
- Configure the fascia with an AdnSkin deformer: Select the combined mesh, then the fascia and then create the skin deformer. It is recommended to use values of *Rest Length Multiplier* lower than 1.
- Configure the skin with an AdnSkin deformer: Select the fascia, then the skin geo and then create the skin deformer.

## How can I simulate facial skin?

You can use AdnSimshape deformer. This deformer allows to reproduce the elasticity and the change in stiffness of a facial geometry thanks to the features of the AdnSimshape solver. Please, check [this section](maya/simshape.md) to know more about how to configure this solver.

## How can I add muscle activations to facial simulation?

The AdnSimshape deformer allows to add muscle activation in two ways:

 - Providing a deform mesh together with an Adonis Muscle Patches file previously generated using the Learn Muscle Patches tool.
 - Plugging the activation values directly into the *ActivationList.Activation* attribute. These activation values can be computed from the rest mesh and the deform mesh using the AdnEdgeEvaluator node (check [this section](maya/edge_evaluator.md)).

For more information, check [how to add muscle activations](maya/simple_setup.md#3-adding-muscle-activations) to AdnSimshape.

## How can I use Machine Learning to add muscle activations to AdnSimshape?

To add muscle activation via Machine Learning, the Learn Muscle Patches tool has to be used to [generate the Adonis Muscle Patches file](maya/simshape.md#generate-muscle-patches). The requirements for this tool are a neutral mesh (facial geometry at rest) and a set of target meshes with deformation representing all facial expressions to drive the learning.

## Can I add muscle activations to AdnSimshape without an Adonis Muscle Patches file?

AdnSimshape allows to add muscle activation alternatively without the need for the Adonis Muscle Patches file. To do this, the activation values must be plugged directly into the *ActivationList.Activation* attribute. These activation values can be computed from the rest mesh and the deform mesh using the AdnEdgeEvaluator tool. For more information check [how to drive the activations of AdnSimshape using AdnEdgeEvaluator](maya/edge_evaluator.md#adnsimshape-activation-using-edge-evaluator-node).

## Can I transfer Adonis nodes configuration to a different asset?

Yes, you can use the AdonisFX [Export](maya/tools.md#adonisfx-export-tool) and [Import](maya/tools.md#adonisfx-import-tool) Tools to generate and load respectively an Adonis Asset Definition (AAD) file. From an scene with an asset fully configured with Adonis deformers, you can select the parent transform object and launch the Exporter. From there, you can decide which settings to export and the destination path for the AAD file. Then, in a different scene with a compatible asset, you can launch the Importer, browse the AAD file and assign deformers from the file to the meshes in the hierarchy of the asset.

## For what units is Adonis designed?

Adonis solvers interpret input units as meters. This means that in order to simulate external forces, the Space Scale may need to be adjusted. For example, to apply Gravity with a value of 9.8 m/s<sup>2</sup>, the Space Scale should be set to 0.01.

## Can I activate AdonisFX offline?
Yes, both online and offline activation is supported. Please, visit the [licensing](licensing.md#licensing) page for more information.

## Can I use my Node-Locked license on more than one machine?
No. To be able to move a node-locked license to a different machine, you have to deactivate the license and reactivate it on the newly configured machine. For more flexibility and no hardware specific licensing restriction you should purchase floating licenses.

## Does the use of AdonisFX require internet access?
If the activation happened through an online activation, then yes. However, if the license had been activated offline, then internet access is needed only to validate the license. This validation is triggered by the licensing system on plug-in load every 5 days, which requires connection to the internet. If this verification fails because of the machine has no internet access, then you can still use AdonisFX for a grace period of 14 days. After that, the license has to be re-verified with our servers, which again requires connection to the internet.

## How can I switch between node-locked licensing an floating licensing inside of AdonisFX?
You can use the environment variable `ADN_LICENSE_MODE` set to `0` for node-locked licensing and `ADN_LICENSE_MODE` set to `1` for floating licensing.

## What do I need to be able to use floating licensing?
You will need to configure and activate the licensing server, make sure that client machines have access to it.

## Can I move the license server to a different machine?
Yes. This process requires you to deactivate it and then activate it on the new machine. For more information visit the [licensing](licensing.md#licensing) page or contact support.

## How can I change the port number of my licensing server?
Change the server `port` number in the `TurboFloatServer-config.xml` before running the server.

## I want to know more about how leases are dropped, how can I see the notifications in my server?
You can find and modify when leases are dropped inside of the `TurboFloatServer-config.xml` file. In there you can also specify where to store the log file and with which verbosity it will write to it.
For more information visit the [licensing](licensing.md#licensing) page or [https://wyday.com/limelm/help/turbofloat-server/](https://wyday.com/limelm/help/turbofloat-server/).

## I can't connect to my licensing server for floating licensing. What should I do?
Make sure that your firewall configuration allows the connection and try using the `ping` command to check the connectivity. If the connection is valid but AdonisFX can't load, please contact support.

## Can I activate the floating licensing server offline?
Yes, [here](licensing.md#install-server) you can find the instructions for that. Once the activation is completed and the server is running, the licensing system will require to verify the status of your server as often as it is specified in the `TurboFloatServer-config.yml` file. This verification requires connection to the internet. Please, check the configuration of `days_between` and `grace` settings in that file for more information.

## My floating server is offline, what will happen?
Whenever trying to load AdonisFX, the plug-in will take several seconds before erroring out as it could not reach the floating server. This should happen on plug-in load and should not affect the functionalities of the plug-in while using it.