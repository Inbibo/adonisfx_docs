# A Simple Setup

This page is dedicated to explain, step by step, a simple process of creating and setting every AdonisFX SOP in Houdini. The scenarios presented here are intended to provide the minimum required configurations to obtain plausible results.

## AdnMuscle

## AdnRibbonMuscle

## AdnGlue

To make the simulated muscles behave more compact and avoid large gaps between them, an AdnGlue node can be used. To create a basic scenario using the AdnGlue node, start with a scene with the following elements:

  - A list of simulated muscles to be glued together.
  - A merge node that combines the simulated muscles into a single geometry.

The AdnGlue node will take all the simulated muscles merged as a single input.

> [!NOTE]
> - AdnGlue requires the input geometry to contain a primitive attribute to be able to identify each muscle.
> - If the AdnGlue input does not contain a primitive attribute, click on AdonisFX > Utils > Create Muscle PieceID by having the AdnGlue input selected. This utility will create a `connectivity` node in charge of computing the primitive attribute that will identify each muscle piece.

### Create Node

To create the AdnGlue node, press TAB and navigate to the submenu AdonisFX > Solvers to find the AdnGlue ![AdnGlue](../images/adn_glue.png){style="width:4%"} SOP type. Then connect the merged muscles to the AdnGlue input and select the *Piece Attribute* to allow the SOP to identify each muscle piece.

<figure>
  <img src="images/simple_setup_glue_00.png">
  <figcaption><b>Figure X</b>: AdnGlue SOP creation scenario. Using null nodes with ADN_IN_ and ADN_OUT_ prefixes to encapsulate the AdonisFX deformable section is recommended to keep the net compatible with the API.</figcaption>
</figure>

Input muscles can be added or removed from the existing AdnGlue by connecting or disconnecting them from the merge node. After that, make sure to recook the AdnGlue at preroll start time for this change to take effect.

> [!NOTE]
> Adding and removing inputs requires to revisit and update the paintable maps to ensure that the painted values are correct for the new list of geometries.

The *Max Glue Distance* attribute is set to 0.0 by default. Therefore, for the glue constraints to take effect, this value must be adjusted.

### Paint Weights

To tweak the point attributes of an AdnGlue SOP, an `attribpaint` is needed. To ease the creation and initial configuration of this node, select the AdnGlue SOP and click on AdonisFX > Utils > Make Paintable. This utility will create an `attribcreate` node to define the required point attributes and assign their default values followed by an `attribpaint` node to allow these attributes to be modified. Both nodes are automatically named and properly connected to the AdnGlue node.

<figure>
  <img src="images/simple_setup_glue_01.png">
  <figcaption><b>Figure X</b>: Deformable section after using the "Make Paintable" utility.</figcaption>
</figure>

With the *Max Glue Distance* previously adjusted, the default values of the paintable maps already allow the node to compute the glue constraints.

The most important maps are `adnGlueResistance`, `adnMaxGlueDistanceMultiplier`, and `adnShapePreservation`, which are flooded with a value of 1.0 by default.

Since the *Max Glue Distance* is initially the same for all muscles, you may want to adjust it for specific areas. This can be done by painting the `adnMaxGlueDistanceMultiplier` map. You can paint this map with a value of 0.0 in areas where you do not want the glue constraint to apply. This prevents the creation of the constraint in those areas and can improve the simulation performance.

<figure>
  <img src="images/simple_setup_glue_02.png">
  <figcaption><b>Figure X</b>: Example of Glue Distance Multiplier map painted only on the areas between the left and right pectoralis and abdominis muscles. In this case, the glue constraints will be created only between vertices with non-zero value.</figcaption>
</figure>

The `adnGlueResistance` map modulates the strength of the glue constraint. To reduce the effect of the constraint in specific areas, lower the values in this map accordingly. Glue constraints won't be computed for vertices with a weight value of 0.0.

<figure>
  <img src="images/simple_setup_glue_03.png">
  <figcaption><b>Figure X</b>: Example of Glue Resistance map painted only on the areas between the left and right pectoralis and abdominis muscles. In this case, the glue constraints will be created only between vertices with non-zero value.</figcaption>
</figure>

Finally, shape preservation constraints help to maintain the original shape of the muscles and are flooded to 1.0 by default. These constraints are useful if the gluing produces undesired shape on the output mesh. If that is not the case, flood the map to 0.0, which will make the solver run faster. If shape preservation is required, then increase the values on those areas where the shape has been altered during the simulation.

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

<figure>
  <img src="images/simple_setup_skin_merge_04.png">
  <figcaption><b>Figure X</b>: Result of AdnSkinMerge in a specific frame. From left to right: Animation Mesh, Simulation Mesh and Final Mesh.</figcaption>
</figure>

## AdnSimshape

To create a basic scenario using the AdnSimshape SOP, start with a scene with the following elements:

 - An animated facial mesh to which to apply the deformer.
 - A rest mesh.
 - Optionally, a deformation mesh with only the facial deformation (no animation) to allow muscle activations.

All these meshes must have the same number of vertices and correspond to the same facial model.

<figure>
  <img src="images/simple_setup_simshape_00.png">
  <figcaption><b>Figure X</b>: Basic setup for facial simulations. From left to right: rest mesh, deformation mesh and animation mesh.</figcaption>
</figure>

### Create Deformer

To create the AdnSimshape node, press TAB and navigate to the submenu AdonisFX > Solvers to find the AdnSimshape ![AdnSimshape](../images/adn_simshape.png){style="width:4%"} SOP type. Then connect the animated mesh to the first input, the rest mesh to the third input and the deformation mesh to the fourth input.

<figure>
  <img src="images/simple_setup_simshape_01.png">
  <figcaption><b>Figure X</b>: AdnSimshape SOP creation scenario. Using null nodes with ADN_IN_ and ADN_OUT_ prefixes to encapsulate the AdonisFX deformable section is recommended to keep the net compatible with the API.</figcaption>
</figure>

### Paint Weights

To tweak the point attributes of an AdnSimshape SOP, an `attribpaint` is needed. To ease the creation and initial configuration of this node, select the AdnSimshape SOP and click on AdonisFX > Utils > Make Paintable. This utility will create an `attribcreate` node to define the required point attributes and assign their default values followed by an `attribpaint` node to allow these attributes to be modified. Both nodes are automatically named and properly connected to the AdnSimshape node.

The most important paintable map is the `adnAttractForce` as this is the value that dictates how much of each simulated vertex should follow the animation. This value is flooded by default to 1.0, meaning that by default the simulated mesh will follow the animation completely, without displaying dynamics.

In high deformation areas, such as around the mouth or under the eyes, add medium to low values (in this case painting with a value of 0.4).

Painting lower Attraction Force weights in meatier areas of the face, such as under the neck or in the cheeks to show more dynamics in these regions. In this case a value of 0.15 will be applied.

The lowest values (0.1 in this case) will be applied to the area under the jaw where dynamics will appear the most.

<figure>
  <img src="images/simple_setup_simshape_02.png">
  <figcaption><b>Figure X</b>: Attraction Force weights for medium dynamics areas.</figcaption>
</figure>

After painting similar weights to the ones displayed and pressing playback to check the animation, realistic dynamics should be simulated in the face. Many more paintable weights to better customize and tweak face dynamics are available and fully explained in the documentation for [AdnSimshape](solvers/simshape).

### Add muscle activations

To further have a realistic depiction of facial dynamics, facial muscle activations can be simulated. The AdnSimshape deformer has two methods of handling muscle activations:

 - AdonisFX Muscle Patches file.
 - Edge Evaluator Node.

Refer to this [section](solvers/simshape#muscle-activations) to see how to use Muscle Patches files. However, in this example, it is taken advantage of the AdnEdgeEvaluator SOP. The process is the following:

- Press TAB and navigate to the submenu AdonisFX > Utils to find the AdnEdgeEvaluator ![Edge Evaluator button](../../images/adn_edge_evaluator.png){style="width:4%"} SOP type.
- Connect the deformation mesh to the first input and the rest mesh to de second input.
- Cook the AdnEdgeEvaluator node and the `adnCompression` point attribute will be written into the geostream.
- Transfer the `adnCompression` point attribute to the geostream of the first input of AdnSimshape with the name `adnActivation`.
- Select the *Plug Values* options in the *Activation Mode* dropdown located in the *Muscles Activation Settings* section of the AdnSimshape node.

<figure>
  <img src="images/simple_setup_simshape_03.png">
  <figcaption><b>Figure X</b>: Example of the AdnEdgeEvaluator SOP usage in conjunction with AdnSimshape SOP to drive the activations. </figcaption>
</figure>

The output activation values can be debugged by checking the option *Write Out Activation* and visualizing the `adnOutActivation` point attribute.
