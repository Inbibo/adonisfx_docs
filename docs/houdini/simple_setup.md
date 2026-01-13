# A Simple Setup

This page is dedicated to explain, step by step, a simple process of creating and setting the main AdonisFX solvers and deformers SOPs in Houdini. The scenarios presented here are intended to provide the minimum required configurations to obtain plausible results.

## AdnMuscle

## AdnRibbonMuscle

## AdnGlue

## AdnFat

## AdnSkin

## AdnRelax

To create a basic scenario using the AdnRelax SOP, start with a scene with a mesh to apply the relaxation onto. This could be for example the simulated fascia layer.

<figure markdown>
  ![relax simple setup](images/simple_setup_relax_00.png)
  <figcaption><b>Figure X</b>: Basic setup for AdnRelax. The mesh is the result of the fascia simulation to which AdnRelax is going to be applied. </figcaption>
</figure>

### Create Deformer

To create the AdnRelax SOP:

1. Go to the geometry context of the rig containing the geometry to apply the deformer to.
2. Press TAB and navigate to the submenu AdonisFX > Deformer to find the AdnRelax ![Relax button](../images/adn_relax.png){style="width:4%"} SOP type.
3. Create it and connect the geometry to the input.
4. Increase the number of iterations to see the effect of the relaxation algorithm.

### Paint Weights

The AdnRelax paintable maps default to 1.0 if the point attributes are not found in the input source. They act as multipliers for the main relax attributes (i.e., *Smooth*, *Relax*, *Push In Ratio*, and *Push Out Ratio*). Therefore, the relaxation algorithm will be applied uniformly over the entire mesh unless the maps are adjusted.

To tweak the point attributes of an AdnRelax SOP, an `attribpaint` is needed. To easy the creation and initial configuration of this node, select the AdnRelax SOP, and click on AdonisFX > Utils > Make Paintable. This utility will create the node with a proper name, connect it to the AdnRelax and add the paintable point attributes to the attributes list with the default values.

Now the deformed mesh can be refined in specific areas by modifying the paintable attributes. Flood a specific map to 0.0 and paint higher values in the areas where the relaxation algorithm should take effect.

<figure markdown>
  ![relax paintable maps](images/relax_weights.png)
  <figcaption><b>Figure X</b>: Example of paintable weights of AdnRelax SOP applied to the fascia layer of a biped. From left to right: smooth multiplier, relax multiplier, push in ratio multiplier, push out ratio multiplier.</figcaption>
</figure>

The smoothing is modulated by the *Smooth Multiplier* map. Keep it flooded to 1.0 to smooth the surface of the entire mesh, or flood it to 0.0 and paint values of 1.0 in the areas that need smoothing.

The relaxation is modulated by the *Relax Multiplier* map. Keep it flooded to 1.0 to relax the surface of the entire mesh, or flood it to 0.0 and paint values of 1.0 in the areas that need relaxation.

After smoothing and relaxation are applied, the mesh may lose some volume or detail. Push in and push out adjustments can be used to recover volume and detail. The attributes *Push In Ratio* and *Push Out Ratio* are set to 0.0 by default, to apply these adjustments, increase their values. Then, use the *Push In Ratio Multiplier* and *Push Out Ratio Multiplier* maps to modulate the specific areas where these adjustments will take effect.

If a specific area shows volume loss, flood the *Push Out Ratio Multiplier* to 0.0 and paint values of 1.0 in areas that need to recover volume so that the push out adjustment moves the vertices outward along their normals.

If a specific area has lost detail, flood the *Push In Ratio Multiplier* to 0.0 and paint values of 1.0 in areas that need more detail so that the push in adjustment moves the vertices inward, opposite to the direction of their normals.

<figure markdown>
  ![relax example results](images/simple_setup_relax_01.png)
  <figcaption><b>Figure X</b>: Example of AdnRelax results with a distribution of weights shown in Figure X. On the left, the input geometry before applying the relaxation; on the right the output geometry resulting from the relaxation. The parameters of the deformer in this example are: iterations set to 25, pin enabled, smooth and relax set to 0.5, push-in and push-out set to 1.0, and thresholds set to -1.0.</figcaption>
</figure>

## AdnPush

## AdnSkinMerge

## AdnSimshape
