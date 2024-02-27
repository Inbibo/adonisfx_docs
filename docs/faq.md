# Frequently Asked Questions

#### How can I simulate muscles?

Adonis provides with two solvers for muscle simulation depending on the necessity of simulating volume preservation. In Maya, muscles with volume preservation can be simulated with [AdnMuscle](documentation/maya/muscle.md) deformer, while [AdnRibbonMuscle](documentation/maya/ribbon.md) is for planar muscles.

#### How can I add activation to the muscles?

In order to add activation to the muscles it is necessary to define the fibers direction. This can be achieved by: first, paitning the tendon weights to generate an initial estimation of fibers direction; and second, combing the fibers through the AdonisFX Paint Tool to customaize the final fibers flow along the surface. Once the muscle has a valid fiber direction at each vertex, then the activation attribute triggers the contraction of the fibers. Ultimately, the level of activation can be modulated by an Adonis sensor to connect the constraction of the muscle to the animation of the rig. For more information about connecting sensors to muscles, please check [how to set up AdnMuscle](documentation/maya/simple_setup.md#adnmuscle-simple-setup) and [how to set up AdnRibbonMuscle](documentation/maya/simple_setup.md#adnribbonmuscle-simple-setup).

#### How can I add volume gain to the muscles?

The [*Volume Ratio*](documentation/maya/muscle.md#solver-attributes) attribute of an AdnMuscle allows to simulate volume gain (volume ratio greater than 1) and loss (volume ration lower than 1). The influence of this attribute depends on the value of *Volume Preservation*, where 0 means no effect, and 1 means maximum effect.

#### How can I simulate skin?

Skin can be simulated using the [AdnSkin](documentation/maya/skin.md) deformer. This deformer requires a mesh to drive the skin simulation (reference mesh) and a mesh to apply the deformer to (skin mesh). For more information please check [how to set up AdnSkin](documentation/maya/simple_setup.md#adnskin-simple-setup).

#### How can I simulate fascia?

Similarly to a skin simulation setup, the fascia can be simulated using [AdnSkin](documentation/maya/skin.md) deformer as well. In this case, it is recommended to use values of *Rest Length Multiplier* lower than 1. This deformer also requires a mesh to drive the simulation (one reference mesh, i.e. the internal muscle geometries combined) and a mesh to apply the deformer to (fascia geometry).

#### Can I simulate muscles, fascia and skin all coupled?

Yes, you can simualte muscles, fascia and skin following these steps:

- Configure every muscle geometry with an AdnMuscle deformer.
- Combine all muscle geometries into a single geometry.
- Configure the fascia with an AdnSkin deformer: Select the combined mesh, then the fascia and then create the skin deformer). It is recommended to use values of *Rest Length Multiplier* lower than 1.
- Configure the skin with an AdnSkin deformer: Select the fascia, then the skin geo and then create the skin deformer).

#### How can I simulate facial skin?

You can use AdnSimshape deformer. This deformer allows to reproduce the elasticty and the change in stiffness of a facial geometry thanks to the features of the AdnSimshape solver. Please, check [this section](documentation/maya/simshape.md) to know more about how to configure this solver.

#### How can I add muscle activations to facial simulation?

The AdnSimshape deformer allows to add muscle activation in two ways:

 - Providing a deform mesh together with an Adonis Muscle Patches file previously generated using the Learn Muscle Patches tool.
 - Plugging the activation values directly into the *ActivationList.Activation* attribute. These activation values can be computed from the rest mesh and the deform mesh using the AdnEdgeEvaluator tool.

For more information, check [how to add muscle activations](documentation/maya/simple_setup.md#3-adding-muscle-activations) to AdnSimshape.

#### How can I use Machine Learning to add muscle activations to AdnSimshape?

To add muscle activation via Maching Learning, the Learn Muscle Patches tool has to be used to [generate the Adonis Muscle Patches file](documentation/maya/simshape.md#generate-muscle-patches). The requirements for this tool are a neutral mesh (facial geometry at rest) and a set of target meshes with deformation representing all facial expressions to drive the learning.

#### Can I add muscle activations to AdnSimshape without an Adonis Muscle Patches file?

AdnSimshape allows to add muscle activation alternatively without the need for the Adonis Muscle Patches file. To do this, the activation values must be plugged directly into the *ActivationList.Activation* attribute. These activation values can be computed from the rest mesh and the deform mesh using the AdnEdgeEvaluator tool. For more information check [how to drive the activations of AdnSimshape using AdnEdgeEvaluator](documentation/maya/edge_evaluator.md#adnsimshape-activation-using-edge-evaluator-node).

#### Can I transfer Adonis nodes configuration to a different asset?

Yes, you can use the AdonisFX [Export](documentation/maya/tools.md#adonisfx-export-tool) and [Import](documentation/maya/tools.md#adonisfx-import-tool) Tools to generate and load respectively an Adonis Asset Definition (AAD) file. From an scene with an asset fully configured with Adonis deformers, you can select the parent transform object and launch the Exporter. From there, you can decide which settings to export and the destination path for the AAD file. Then, in a different scene with a compatible asset, you can launch the Importer, browse the AAD file and assign deformers from the file to the meshes in the hierarhcy of the asset.

#### What units is ADonis designed?

Adonis solvers interpret input units as meters. This means that in order to simulate external forces, the Space Scale may need to be adjusted. For example, to apply Gravity with a value of 9.8 m/s<sup>2</sup>, the Space Scale should be set to 0.01.
