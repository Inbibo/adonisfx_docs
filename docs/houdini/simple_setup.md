# A Simple Setup

This page is dedicated to explain, step by step, a simple process of creating and setting every AdonisFX SOP in Houdini. The scenarios presented here are intended to provide the minimum required configurations to obtain plausible results.

## AdnMuscle

## AdnRibbonMuscle

## AdnGlue

## AdnFat

## AdnSkin

## AdnRelax

## AdnPush

## AdnSkinMerge

To create a basic scenario using the AdnSkinMerge SOP, start with a scene with the following elements:

  - One or more animation meshes with deformation.
  - One or more simulation meshes, for example with an AdnSkin deformer applied and properly configured.
  - A final mesh without animation or deformation.

The AdnSkinMerge deformer will be applied to the final mesh which will be the result of blending the animation and simulation meshes.

<figure>
  <img src="images/simple_setup_skin_merge_00.png">
  <figcaption><b>Figure X</b>: Minimum required geometries to configure an AdnSkinMerge SOP. From left to right: Animation Mesh, Simulation Mesh and Final Mesh to apply the AdnSkinMerge SOP.</figcaption>
</figure>

### Create Deformer

To create the AdnSkinMerge node, press TAB and navigate to the submenu AdonisFX > Solvers to find the AdnSkinMerge ![AdnSkinMerge](../images/adn_skin_merge.png){style="width:4%"} SOP type. Then connect the final mesh to the AdnSkinMerge input and go to the *Targets* tab to provide the *anim* and *sim* meshes. Make sure the initialization time corresponds to the start time where all the geometries are in rest pose.

<figure>
  <img src="images/simple_setup_skin_merge_01.png">
  <figcaption><b>Figure X</b>: AdnSkinMerge SOP creation scenario. Using null nodes with ADN_IN_ and ADN_OUT_ prefixes to encapsulate the AdonisFX deformable section is recommended to keep the net compatible with the API.</figcaption>
</figure>

### Paint Weights

To tweak the point attributes of an AdnSkinMerge SOP, an `attribpaint` is needed. To ease the creation and initial configuration of this node, select the AdnSkinMerge SOP and click on AdonisFX > Utils > Make Paintable. This utility will create an `attribcreate` node to define the required point attributes and assign their default values followed by an `attribpaint` node to allow these attributes to be modified. Both nodes are automatically named and properly connected to the AdnSkinMerge node.

<figure style="width: 70%;" markdown>
  <img src="images/simple_setup_skin_merge_02.png">
  <figcaption><b>Figure X</b>: Deformable section after using the "Make Paintable" utility.</figcaption>
</figure>

Once the `attribpaint` node is created the weights can be painted to blend the animation and simulation meshes into the final mesh.

The `adnBlend` attribute represents the level of influence of the simulated mesh: a value of 0.0 makes the vertices follow the animated inputs, while a value of 1.0 makes the vertices follow the simulated inputs.

To have a smooth transition from the simulated mesh to the animated mesh, smooth the painting in the areas near the edges between the simulation and animation meshes.

<figure>
  <img src="images/simple_setup_skin_merge_03.png">
  <figcaption><b>Figure X</b>: Blend weights painted map.</figcaption>
</figure>

With this basic paint setup the AdnSkinMerge SOP will now show the results of skin simulation transferred to the final mesh.

## AdnSimshape
