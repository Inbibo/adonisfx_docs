# Frequently Asked Questions

#### How can I simulate muscles?

Adonis allows to simulate both volumetric and planar muscles using the [AdnMuscle](documentation/maya/muscle.md) and [AdnRibbonMuscle](documentation/maya/ribbon.md) deformers respectively.

#### How can I add activation to the muscles?

In order to add activation to the muscles it is necessary to paint the muscle tendon weights. Then the corresponding AdnSensor and AdnLocator must be configured and the output activation attribute of the locator (e.g. *activationAngle*, *activationDistance*) has to be connected to the *activation* attribute of the muscle deformer. For more information check [how to set up AdnMuscle](documentation/maya/simple_setup.md#adnmuscle-simple-setup) and [how to set up AdnRibbonMuscle](documentation/maya/simple_setup.md#adnribbonmuscle-simple-setup).

#### How can I add volume gain to the muscles?

The [*Volume Ratio*](documentation/maya/muscle.md#solver-attributes) attribute of the AdnMuscle deformer allows to introduce the rate of increase or decrease in volume applied to the simulated muscle.

#### How can I simulate skin?

Skin can be simulated using the [AdnSkin](documentation/maya/skin.md) deformer. This deformer requires a mesh to drive the skin simulation (reference mesh) and a mesh to apply the deformer to (skin mesh). For more information check [how to set up AdnSkin](documentation/maya/simple_setup.md#adnskin-simple-setup).

#### How can I simulate fascia?

Abc

#### Can I simulate muscles, fascia and skin all coupled?

Abc

#### How can I simulate facial skin?

Abc

#### How can I add muscle activations to AdnSimshape?

The AdnSimshape deformer allows to add muscle activation in two ways:

 - Providing a deform mesh together with an Adonis Muscle Patches file previously generated using the Learn Muscle Patches tool.
 - Plugging the activation values directly into the *ActivationList.Activation* attribute. These activation values can be computed from the rest mesh and the deform mesh using the AdnEdgeEvaluator tool.

For more information check [how to add muscle activations](documentation/maya/simple_setup.md#3-adding-muscle-activations) to AdnSimshape.

#### How can I use Machine Learning to add muscle activations to AdnSimshape?

To add muscle activation via Maching Learning, the Learn Muscle Patches tool has to be used to [generate the Adonis Muscle Patches file](documentation/maya/simshape.md#generate-muscle-patches). The requirements of this tool are a neutral mesh (rest mesh with a neutral facial expression) and a set of target meshes (deformed meshes representing facial expressions).

#### Can I add muscle activations to AdnSimshape without an Adonis Muscle Patches file?

AdnSimshape allows to add muscle activation alternatively without the need for the Adonis Muscle Patches file. To do this, the activation values must be plugged directly into the *ActivationList.Activation* attribute. These activation values can be computed from the rest mesh and the deform mesh using the AdnEdgeEvaluator tool. For more information check [how to drive the activations of AdnSimshape using AdnEdgeEvaluator](documentation/maya/edge_evaluator.md#adnsimshape-activation-using-edge-evaluator-node).

#### Can I transfer Adonis nodes configuration to a different asset?

Abc

#### Can I add multiple Adonis deformers to the same mesh?

Abc