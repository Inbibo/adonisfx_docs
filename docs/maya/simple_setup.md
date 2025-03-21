# A Simple Setup

This page is dedicated to explain, step by step, a simple process of creating and setting every AdonisFX deformer in Maya. The scenarios presented here are intended to provide the minimum required configurations to obtain plausible results.

## AdnMuscle

To create a basic scenario using the AdnMuscle deformer, start with a scene with the following elements:

 - An animation rig.
 - A geometry representing the muscle to simulate.

In this case the proposed example is to simulate a biceps in an animated full body rig. The AdnMuscle deformer will be applied to the mesh of the biceps.

<figure>
  <img src="images/simple_setup_muscle_00.png"> 
  <figcaption><b>Figure 1</b>: Basic setup for biceps simulations.</figcaption>
</figure>

### Create Deformer

To create the AdnMuscle deformer select the mesh of the muscle, then press the ![AdnMuscle](images/adn_muscle.png){style="width:4%"} shelf button or go to AdonisFX Menu > *Solvers* > *Muscle*. This will assign the AdnMuscle deformer to the selected muscle.

To create the AdnMuscle deformer with some initial specialization, double-click the shelf button or press the option box in the menu item. This will display a pop-up window that will allow doing some initial specialization, as well as creating the deformer with a custom name. Once all data has been provided press the *Create* button and the deformer will get created.

<figure>
  <img src="images/simple_setup_muscle_01.png"> 
  <figcaption><b>Figure 2</b>: AdnMuscle custom creation UI.</figcaption>
</figure>

In order to add attachment constraints to the muscle select the targets (joints, geometries or both), then the muscle with the AdnMuscle applied and finally press the ![add target](images/adn_add_target.png){style="width:4%"} button or *Add Targets* in the AdonisFX menu from the Edit Muscle submenu.

Additionally, target geometries that have been added to an AdnMuscle deformer can also be used to define Slide On Geometry Constraints. This constraint type is recommended for muscles in the limbs of the character to better follow the animation.

> - Attachments to geometry and slide on geometry constraints are meant to simulate muscle-to-bone and muscle-to-muscle interactions.
> - For muscle-to-muscle interactions, only unidirectional relationships are supported. This means that having muscles A and B, it is possible to assign A as target of B or B as target of A, but not the two at the same time.

Optionally, add Slide On Segment Constraints. This constraint works in a similar way to Slide On Geometry Constraints, however, instead of providing a geometry a pair of joints of the rig will be specified representing the segment the muscle will slide on. Selecting first the two joints of the rig (shoulder and elbow) and then the muscle geometry, go to AdonisFX Menu > Muscle > *Add Slide On Segment Constraint*.

### Paint Weights

Once the AdnMuscle deformer is properly created it is possible now to paint its weights to correctly set up the deformer properties. To do so, select the simulated mesh and press the ![paint tool](images/adn_paint_tool.png){style="width:4%"} shelf button or go to AdonisFX Menu > *Paint Tool*.

Start by painting attachment weights, painting the influence for each target by selecting the corresponding target from the list and painting its desired influence.

> [!NOTE]
> In this example the influence painting for both types of attachment constraint is shown. The different types of attachments can be used together or not depending on the needs of the simulation and the rig setup.

<figure>
  <img src="images/simple_setup_muscle_paint_transform_attach.png">
  <figcaption><b>Figure 3</b>: Transform Attachment influences (joints and locators).</figcaption>
</figure>

<figure>
  <img src="images/simple_setup_muscle_paint_geometry_attach.png">
  <figcaption><b>Figure 4</b>: Geometry Attachment influences (meshes).</figcaption>
</figure>

Then, paint the muscle tendon weights, by selecting the *Tendon* attribute from the *Attribute* enumerator and paint over the parts of the muscle that should have tendon tissue.

<figure>
  <img src="images/simple_setup_muscle_02.png">
  <figcaption><b>Figure 5</b>: Tendon weights for biceps.</figcaption>
</figure>

Once tendons are painted, when selecting the *Fibers* attribute from the *Attribute* enumerator, painted fibers will be displayed, with a default direction set by the painted tendons. It is now possible to freely comb these fibers if it is desired.

To change the fiber size or its color, go to the Attribute Editor in the debug submenu, and customize the color, width and length of the drawn lines.

<figure>
  <img src="images/simple_setup_muscle_03.png">
  <figcaption><b>Figure 6</b>: Muscle fibers combing.</figcaption>
</figure>

Finally, paint Slide On Segment or Slide On Geometry Constraints (if added). It is recommended to paint only the vertices that are not attached to the rig. In this example, the tendons are painted with a value of 0.0, while the rest of the shape is painted to 1.0 or lower values.

<figure>
  <img src="images/simple_setup_muscle_04.png">
  <figcaption><b>Figure 7</b>: Slide on segment weights for biceps.</figcaption>
</figure>

<figure>
  <img src="images/simple_setup_muscle_05.png">
  <figcaption><b>Figure 8</b>: Slide on geometry weights for biceps.</figcaption>
</figure>

### Connect Sensors

To have the muscle changing and responding to external inputs (i.e. the flexion of the arm), AdnSensorRotation can be added to drive the activation of the muscle. 

To do this, first create a rotation locator and sensor to compute the elbow angle. Both elements can be created by selecting the three joints from which to create the rotation locator and sensor (shoulder, elbow and wrist joints) and directly click on the ![adnRotationSensor](images/adn_angle_sensor.png){style="width:4%"} shelf button or go to AdonisFX Menu > Sensors (on the *Create* group) > *Rotation*. With this, both a locator and its corresponding sensor will get created at the same time.

<figure>
  <img src="images/simple_setup_muscle_06.png">
  <figcaption><b>Figure 9</b>: Rotation locator and sensor setup in elbow.</figcaption>
</figure>

Now that the sensor is created it has to be connected to the deformer. To do so, make use of the Connection Editor, which must be opened from the AdonisFX Menu > Sensors (on the *Edit* group) > *Connection Editor*.

With the Connection Editor opened, select the locator from the scene and press the *Reload Left* button, then select the simulated mesh and press the *Reload Right* button. The list widgets will refresh with the respective connectable attributes. Select the *activationAngle* attribute from the locator and the *activation* attribute from the deformer, and click *Make Connection*.

<figure>
  <img src="images/simple_setup_muscle_07.png">
  <figcaption><b>Figure 10</b>: Connection Editor tool.</figcaption>
</figure>

When the elbow is flexed (and therefore the angle from the locator gets smaller) the muscle activation will get higher, simulating a much more realistic scenario.

To tweak additional parameters of the AdnMuscle deformer, check this [page](deformers/muscle).

## AdnRibbonMuscle

The process to set up an AdnRibbonMuscle is very similar to the one of setting up an AdnMuscle. It essentially follows the same steps. Start with the following elements:

 - An animation rig.
 - A geometry representing the muscle to simulate.

In this case a planar muscle will be simulated corresponding to a biceps, which will yield similar results to the case of the AdnMuscle deformer previously shown.

<figure>
  <img src="images/simple_setup_ribbon_muscle_00.png">
  <figcaption><b>Figure 11</b>: Basic setup for planar biceps simulations.</figcaption>
</figure>

### Create Deformer

Similar to AdnMuscle, create the AdnRibbonMuscle deformer by selecting the mesh to deform (the biceps muscle) and then pressing the ![AdnRibbonMuscle](images/adn_ribbon_muscle.png){style="width:4%"} shelf button or go to AdonisFX Menu > *Solvers* > *Ribbon Muscle*.

To create the AdnRibbonMuscle deformer with some initial specialization, double-click the shelf button or press the option box in the menu item. This will display a pop-up window that will allow doing some initial specialization, as well as creating the deformer with a custom name. Once all data has been provided press the *Create* button and the deformer will get created.

<figure>
  <img src="images/simple_setup_ribbon_muscle_01.png">
  <figcaption><b>Figure 12</b>: AdnRibbonMuscle custom creation UI.</figcaption>
</figure>

In order to add attachment constraints to the ribbon muscle select the targets (joints, geometries or both), then the muscle with the AdnMuscle applied and finally press the ![add target](images/adn_add_target.png){style="width:4%"} button or *Add Targets* in the AdonisFX menu from the Edit Muscle submenu.

Additionally, target geometries that have been added to an AdnRibbonMuscle deformer can also be used to define Slide On Geometry Constraints. This constraint type is recommended for muscles in the limbs of the character to better follow the animation.

> [!NOTE]
> - Attachments to geometry and slide on geometry constraints are meant to simulate muscle-to-bone and muscle-to-muscle interactions.
> - For muscle-to-muscle interactions, only unidirectional relationships are supported. This means that having muscles A and B, it is possible to assign A as target of B or B as target of A, but not the two at the same time.

Optionally, add Slide On Segment Constraints. This constraint works in a similar way to Slide On Geometry Constraints, however, instead of providing a geometry a pair of joints of the rig can be specified representing the segment the muscle will slide on. Selecting first the two joints of the rig (shoulder and elbow) and then the muscle geometry, go to AdonisFX Menu > Muscle > *Add Slide On Segment Constraint*.

### Paint Weights

Once the ribbon muscle deformer is properly created it is possible now to paint its weights to correctly set up the deformer properties. To do so, select the simulated mesh and press the ![paint tool](images/adn_paint_tool.png){style="width:4%"} shelf button or go to AdonisFX Menu > *Paint Tool*.

Start by painting attachment weights, painting the influence for each target by selecting the corresponding target from the list and painting its desired influence.

> [!NOTE]
> In this example the influence painting for both types of attachment constraint is shown. The different types of attachments can be used together or not depending on the needs of the simulation and the rig setup.

<figure>
  <img src="images/simple_setup_ribbon_muscle_paint_transform_attach.png">
  <figcaption><b>Figure 13</b>: Transform Attachment influences (joints and locators).</figcaption>
</figure>

<figure>
  <img src="images/simple_setup_ribbon_muscle_paint_geometry_attach.png">
  <figcaption><b>Figure 14</b>: Geometry Attachment influences (meshes).</figcaption>
</figure>

Then, paint the muscle tendon weights, by selecting the *Tendon* attribute from the *Attribute* enumerator and painting over the parts of the muscle to represent tendon tissue.

<figure>
  <img src="images/simple_setup_ribbon_muscle_02.png">
  <figcaption><b>Figure 15</b>: Tendon weights for planar biceps.</figcaption>
</figure>

Now that tendons are painted, when selecting the *Fibers* attribute from the *Attribute* enumerator, painted fibers will be displayed, with a default direction set by the painted tendons. It is now possible to freely comb these fibers if it is desired.

In case the fiber or its color has to be manipulated, go to the Attribute Editor, in the debug submenu, and customize the color, width and length of the drawn lines.

<figure>
  <img src="images/simple_setup_ribbon_muscle_03.png">
  <figcaption><b>Figure 16</b>: Muscle fibers combing.</figcaption>
</figure>

Finally, paint Slide On Segment or Slide On Geometry Constraints (if added). It is recommended to paint only the vertices that are not attached to the rig. In this example, the tendons are painted with a value of 0.0, while the rest of the shape is painted to 1.0 or lower values.

<figure>
  <img src="images/simple_setup_ribbon_muscle_04.png">
  <figcaption><b>Figure 17</b>: Slide on segment weights for planar biceps.</figcaption>
</figure>

<figure>
  <img src="images/simple_setup_ribbon_muscle_05.png">
  <figcaption><b>Figure 18</b>: Slide on geometry weights for planar biceps.</figcaption>
</figure>

### Connect Sensors

The process to connect and AdnSensor to an AdnRibbonMuscle is the exact same to the one followed [here](#connect-sensors).

<figure>
  <img src="images/simple_setup_ribbon_muscle_06.png">
  <figcaption><b>Figure 19</b>: Connection Editor tool with AdnRotation sensor connected to AdnRibbonMuscle.</figcaption>
</figure>

To tweak additional parameters of the AdnRibbonMuscle deformer, check this [page](deformers/ribbon).

## AdnGlue

To make the simulated muscles behave more compact and avoid large gaps between them, an AdnGlue node can be used. To create a basic scenario using the AdnGlue node, start with a scene with the following elements:

  - A list of simulated muscles to be glued together.

The AdnGlue node will take all the simulated muscles provided as inputs and generate one combined output mesh with glue constraints applied.

### Create Node

To create the AdnGlue node, select the simulated muscles and press the ![AdnGlue](images/adn_glue.png){style="width:4%"} shelf button or go to AdonisFX Menu > *Solvers* > *Glue*. This will connect the selected muscles to the inputs plug of the AdnGlue node and create a combined output mesh as the result of the simulation.

<figure>
  <img src="images/simple_setup_glue_00.png"> 
  <figcaption><b>Figure 20</b>: AdnGlue deformer creation scenario.</figcaption>
</figure>

After the node creation, input muscles can be added or removed from the existing AdnGlue by pressing AdonisFX > Glue > *Add Inputs* or AdonisFX > Glue > *Remove Inputs* respectively.

The *Max Glue Distance* attribute is set to 0.0 by default. Therefore, for the glue constraints to take effect, this value must be adjusted. We recommend enabling the debugger and selecting the *Glue Constraints* option to inspect the connections created based on the specified *Max Glue Distance*.

<figure>
  <img src="images/simple_setup_glue_01.png"> 
  <figcaption><b>Figure 21</b>: Debugging the Glue Constraints connections with a Max Glue Distance of 0.1.</figcaption>
</figure>

### Paint Weights

> [!NOTE]
> AdnGlue requires the use of the Maya Paint tool (not the AdonisFX paint tool) for the paintable weights setup.

Once the AdnGlue node is properly created, you can use Maya Paint Tool to paint its weights and correctly set up the node properties. With the *Max Glue Distance* previously adjusted, the default values of the paintable maps already allow the node to compute the glue constraints.

The most important maps are *Glue Resistance*, *Max Glue Distance Multiplier*, and *Shape Preservation*. The first two are flooded with a value of 1.0 by default, while the last one is flooded with 0.0.

Since the *Max Glue Distance* is initially the same for all muscles, you may want to adjust it for specific areas. This can be done by painting the *Max Glue Distance Multiplier* map. You can paint this map with a value of 0.0 in areas where you do not want the glue constraint to apply. This prevents the creation of the constraint in those areas and can improve the simulation performance.

<figure>
  <img src="images/simple_setup_glue_02.png"> 
  <figcaption><b>Figure 22</b>: Glue Distance Multiplier map painted in specific areas where muscles are supposed to be glued together.</figcaption>
</figure>

<figure>
  <img src="images/simple_setup_glue_03.png"> 
  <figcaption><b>Figure 23</b>: Displaying the Glue Constraints debugger after painting the Glue Distance Multiplier in the target area.</figcaption>
</figure>

The *Glue Resistance* map modulates the strength of the glue constraint. To reduce the effect of the constraint in specific areas, lower the values in this map accordingly. Glue constraints won't be computed for vertices with a weight value of 0.0.

<figure>
  <img src="images/simple_setup_glue_04.png"> 
  <figcaption><b>Figure 24</b>: Glue Resistance map painted in specific areas where muscles are supposed to be glued together.</figcaption>
</figure>

Finally, shape preservation constraints help to maintain the original shape of the muscles. These constraints are useful if the gluing produces undesired shape on the output mesh. If that is not the case, then this map can stay unmodified (0.0) which will make the solver run faster. If shape preservation is required, then increase the values on those areas where the shape has been altered during the simulation.

> [!NOTE]
> In case you are experiencing issues trying to paint weights on the AdnGlue output geometry, find in the [limitations section of AdnGlue](nodes/glue#limitations) a proposed workaround.

## AdnFat

To create a basic scenario using the AdnFat deformer, start with a scene with the following elements:

  - One base mesh to which the fat layer will be attached to. This could be for example the fascia.
  - A fat tissue mesh without animation or deformation.

The AdnFat deformer will get applied to the second selected mesh which will become the simulated mesh (the fat tissue).

<figure>
  <img src="images/simple_setup_fat_00.png"> 
  <figcaption><b>Figure 25</b>: Basic setup for fat simulations.</figcaption>
</figure>

> [!NOTE]
> - The base mesh and the fat mesh must have the same vertex count and triangulation.
> - The base mesh must be provided, otherwise the Fat solver will abort the simulation.

### Create Deformer

To create the AdnFat deformer first select the base mesh and then the fat tissue mesh. Then press the ![AdnFat](images/adn_fat.png){style="width:4%"} shelf button or go to AdonisFX Menu > *Fat*.

To create the AdnFat deformer with some initial specialization, double-click the shelf button or press the option box in the menu item. This will display a pop-up window that will allow doing some initial specialization, as well as creating the deformer with a custom name. Once all data has been provided press the *Create* button and the deformer will get created.

<figure>
  <img src="images/simple_setup_fat_01.png"> 
  <figcaption><b>Figure 26</b>: AdnFat deformer creation scenario.</figcaption>
</figure>

After basic configuration, to alter the dynamics of the fat layer (e.g. adding or reducing the jiggle) it is advisable to tweak the main attributes like: *Iterations*, *Substeps*, *Global Damping Multiplier* or the per-constraint stiffness values in the *Override Constraint Stiffness* section.

### Paint Weights

> [!NOTE]
> AdnFat requires the use of the Maya Paint tool (not the AdonisFX paint tool) for the paintable weights setup.

With the default paint setup provided when creating a new AdnFat, the simulation should already create plausible results. However, below we walk you through the three main maps that can be altered to modify the behavior of the fat simulation.

In the case of the AdnFat deformer, use the Maya Paint tool to set up and paint its paintable weight attributes. The most important paintable maps are *Shape Preservation*, *Volume Shape Preservation* and *Hard Constraints*. The first two are flooded to 1.0 by default, while the last one is flooded to 0.0.

With the *Shape Preservation* being flooded to 1.0 by default the solver will try to maintain the internal structural shape properties of the fat layer. Reducing this map's values can increase the amount of jiggling in the fat tissue in combination with different other parameters. However, reducing the *Shape Preservation* map can decrease the fat layer's ability to maintain its shape. Finding the right balance will allow you to get the desired results. It may be advisable to keep this map flooded to 1.0 and reduce its value in areas that don't require any structural shape preservation.

On the other hand, *Volume Shape Preservation* will also try to maintain the shape of the fat volume but with different computation mechanisms than *Shape Preservation*. It is advisable to keep this map flooded to 1.0 for best results and only reduce its value (by flooding the mesh) whenever the shape of the fat layer can be altered during simulation.

Finally, the *Hard Constraints* map provides additional control for stronger attachments to the base mesh. In most cases, this map can be left unmodified so that the solver does not apply this constraint. However, when there is a large enough gap between the simulated mesh and the base mesh in areas close to edges (e.g. neck, wrists or ankles), it can be useful to paint them with a value of 1.0 to mitigate excessive motion.

<figure>
  <img src="images/simple_setup_fat_shape_preserve.png"> 
  <figcaption><b>Figure 27</b>: Shape Preservation Constraints weights paint.</figcaption>
</figure>

## AdnSkin

To create a basic scenario using the AdnSkin deformer, start with a scene with the following elements:

  - One or more target meshes with deformation.
  - A skin mesh without animation or deformation.

The AdnSkin deformer will get applied to the last mesh which will become the simulated mesh.

<figure>
  <img src="images/simple_setup_skin_00.png"> 
  <figcaption><b>Figure 28</b>: Basic setup for skin simulations: target mesh (grey) and skin mesh to simulate (red).</figcaption>
</figure>

### Create Deformer

To create the AdnSkin deformer select one or more target meshes (optional, they can be added later) and then the skin mesh. Then press the ![AdnSkin](images/adn_skin.png){style="width:4%"} shelf button or go to AdonisFX Menu > *Skin*.

To create the AdnSkin deformer with some initial specialization, double-click the shelf button or press the option box in the menu item. This will display a pop-up window that will allow doing some initial specialization, as well as creating the deformer with a custom name. Once all data has been provided press the *Create* button and the deformer will get created.

<figure>
  <img src="images/simple_setup_skin_01.png"> 
  <figcaption><b>Figure 29</b>: AdnSkin deformer creation scenario.</figcaption>
</figure>

### Paint Weights

Once the AdnSkin deformer is properly created it is possible now to paint its weights to correctly set up the deformer properties. To do so, select the simulated mesh and press the ![paint tool](images/adn_paint_tool.png){style="width:4%"} shelf button or go to AdonisFX Menu > *Paint Tool*.

Start by painting *Soft Constraints* by selecting the option from the attribute enumerator. Flood this weight to a low value of 0.2 to have a uniform distribution of soft constraints. This will help the skin to follow the target mesh.

<figure>
  <img src="images/simple_setup_skin_soft.png"> 
  <figcaption><b>Figure 30</b>: Soft Constraints weights paint.</figcaption>
</figure>

Now paint *Hard Constraints* in two steps. First, flood this weight to a value of 0.1 to help the skin (together with the soft weights) to follow the target mesh. Then, set the edges to 1.0 to attach them strongly to the target mesh.

<figure>
  <img src="images/simple_setup_skin_hard.png"> 
  <figcaption><b>Figure 31</b>: Hard Constraints weights paint.</figcaption>
</figure>

Then select the *Slide Constraints* attribute and paint weights only in those areas where the skin is supposed to slide over the target mesh. In this case, focus these weights over the scapulas and the joints of the limbs.

<figure>
  <img src="images/simple_setup_skin_slide.png"> 
  <figcaption><b>Figure 32</b>: Slide Constraints weights paint.</figcaption>
</figure>

Finally, select the *Sliding Distance Multiplier* attribute and paint weights to 1.0 only in the sliding areas. This will ensure that the vertices with sliding properties will get assigned with the maximum sliding distance (defined by the *Max Sliding Distance* attribute), while the non-sliding vertices will get assigned with 0.0 sliding distance, which will improve the performance of the simulation.

<figure>
  <img src="images/simple_setup_skin_slide_multiplier.png"> 
  <figcaption><b>Figure 33</b>: Sliding Distance Multiplier weights paint.</figcaption>
</figure>

The order of painting is important because after every stroke a normalization of weights soft, hard and slide is performed to ensure that the sum is less or equal to 1.0. In this example, after painting *Slide Constraints*, both *Hard Constraints* and *Soft Constraints* will update, reducing their respective values in the areas painted with maximum sliding.

With this basic paint setup the AdnSkin deformer will already show plausible results, expected of the skin to the target mesh. However, the possible parameters and tweaks to display high fidelity dynamics can be seen in the documentation for [AdnSkin](deformers/skin).

## AdnRelax

To create a basic scenario using the AdnRelax deformer, start with a scene with a mesh to apply the relaxation onto. This could be for example the simulated fascia layer.

<figure>
  <img src="images/simple_setup_relax_00.png">
  <figcaption><b>Figure 34</b>: Basic setup for AdnRelax. The mesh is the result of the fascia simulation to which AdnRelax is going to be applied. </figcaption>
</figure>

### Create Deformer

To create the AdnRelax deformer:

1. Select the mesh to apply the deformer onto.
2. Press the ![AdnRelax](images/adn_relax.png){style="width:4%"} shelf button or go to AdonisFX Menu > Deformers > *Relax*.
3. Increase the number of iterations to see the effect of the relaxation algorithm.

### Paint Weights

> [!NOTE]
> AdnRelax requires the use of the Maya Paint tool (not the AdonisFX paint tool) for the paintable weights setup.

The AdnRelax paintable maps are flooded to 1.0 by default because they act as multipliers for the main relax attributes (i.e., *Smooth*, *Relax*, *Push In Ratio*, and *Push Out Ratio*). Therefore, the relaxation algorithm will be applied uniformly over the entire mesh unless the maps are adjusted.

The deformed mesh can be refined in specific areas by modifying the multiplier maps. Flood a specific map to 0.0 and paint higher values in the areas where the relaxation algorithm should take effect.

<figure markdown>
  ![relax paintable maps](images/relax_weights.png)
  <figcaption><b>Figure 35</b>: Example of paintable weights of AdnRelax deformer applied to a fascia layer. From left to right: smooth multiplier, relax multiplier, push in ratio multiplier, push out ratio multiplier.</figcaption>
</figure>

The smoothing is modulated by the *Smooth Multiplier* map. Keep it flooded to 1.0 to smooth the surface of the entire mesh, or flood it to 0.0 and paint values of 1.0 in the areas that need smoothing.

The relaxation is modulated by the *Relax Multiplier* map. Keep it flooded to 1.0 to relax the surface of the entire mesh, or flood it to 0.0 and paint values of 1.0 in the areas that need relaxation.

After smoothing and relaxation are applied, the mesh may lose some volume or detail. Push in and push out adjustments can be used to recover volume and detail. The attributes *Push In Ratio* and *Push Out Ratio* are set to 0.0 by default, to apply these adjustments, increase their values. Then, use the *Push In Ratio Multiplier* and *Push Out Ratio Multiplier* maps to modulate the specific areas where these adjustments will take effect.

If a specific area shows volume loss, flood the *Push Out Ratio Multiplier* to 0.0 and paint values of 1.0 in areas that need to recover volume so that the push out adjustment moves the vertices outward along their normals.

If a specific area has lost detail, flood the *Push In Ratio Multiplier* to 0.0 and paint values of 1.0 in areas that need more detail so that the push in adjustment moves the vertices inward, opposite to the direction of their normals.

<figure markdown>
  ![relax example results](images/simple_setup_relax_01.png)
  <figcaption><b>Figure 36</b>: Example of AdnRelax results with a distribution of weights shown in Figure 35. On the left, the input geometry before applying the relaxation; on the right the output geometry resulting from the relaxation. The parameters of the deformer in this example are: iterations set to 25, pin enabled, smooth and relax set to 0.5, push-in and push-out set to 1.0, and thresholds set to -1.0.</figcaption>
</figure>

## AdnSkinMerge

To create a basic scenario using the AdnSkinMerge deformer, start with a scene with the following elements:

  - One or more animation meshes with deformation.
  - One or more simulation meshes, for example with an AdnSkin deformer applied and properly configured.
  - A final mesh without animation or deformation.

The AdnSkinMerge deformer will be applied to the final mesh which will  be the result of blending the animation and simulation meshes.

<figure>
  <img src="images/simple_setup_skin_merge_00.png"> 
  <figcaption><b>Figure 37</b>: Basic setup for skin merge. Meshes isolated for better visualization. From left to right: Final Mesh, Animation Mesh, Simulation Mesh.</figcaption>
</figure>

### Create Deformer

To create the AdnSkinMerge deformer press the ![AdnSkinMerge](images/adn_skin_merge.png){style="width:4%"} shelf button or go to *AdonisFX Menu* > *Deformers* (on the *Create* group) > *Skin Merge*.

With this action the Create Skin Merge UI will open, allowing to add all the required elements to create the deformer. To add the required meshes select the mesh in the scene and press the corresponding *Add Selected* button. You may also set up a custom name and initialization time in this window before creating the deformer. Make sure the initialization time corresponds to the start time where all the geometries are in rest pose.

When everything has been properly set up, press the *Create* button to create the AdnSkinMerge deformer.

<figure>
  <img src="images/simple_setup_skin_merge_01.png"> 
  <figcaption><b>Figure 38</b>: Create Skin Merge window with corresponding meshes added.</figcaption>
</figure>

### Paint Weights

> [!NOTE]
> AdnSkinMerge requires the use of the Maya Paint tool (not the AdonisFX paint tool) for the paintable weights setup.

Once the AdnSkinMerge deformer is created the weights can be painted to blend the animation and simulation meshes into the final mesh.

The *Blend* attribute represents the level of influence of the simulated mesh: a value of 0.0 makes the vertices follow the animated inputs, while a value of 1.0 makes the vertices follow the simulated inputs.

To have a smooth transition from the simulated mesh to the animated mesh, smooth the painting in the areas near the edges between the simulation and animation meshes.

<figure>
  <img src="images/simple_setup_skin_merge_02.png"> 
  <figcaption><b>Figure 39</b>: Blend weights painted map.</figcaption>
</figure>

With this basic paint setup the AdnSkinMerge deformer will now show the results of skin simulation transferred to the final mesh.

## AdnSimshape

To create a basic scenario using the AdnSimshape deformer, start with a scene with the following elements:

 - An animated facial mesh to which to apply the deformer.
 - A rest mesh.
 - Optionally, a deformation mesh with only the facial deformation (no animation) to allow muscle activations.

All these meshes must have the same number of vertices and correspond to the same facial model.

<figure>
  <img src="images/simple_setup_simshape_00.png"> 
  <figcaption><b>Figure 40</b>: Basic setup for facial simulations.</figcaption>
</figure>

### Create Deformer

To create the AdnSimshape deformer it is required to select first the rest mesh and then the animated mesh. In this scenario, the animated mesh will be used as the simulated mesh.

Press the ![AdnSimshape](images/adn_simshape.png){style="width:4%"} shelf button or go to AdonisFX Menu > *Simshape*.

To create the AdnSimshape deformer with some initial specialization, double-click the shelf button or press the option box in the menu item. This will display a pop-up window that will allow doing some initial specialization, as well as creating the deformer with a custom name. Once all data has been provided press the *Create* button and the deformer will get created.

<figure>
  <img src="images/simple_setup_simshape_01.png"> 
  <figcaption><b>Figure 41</b>: AdnSimshape deformer creation scenario.</figcaption>
</figure>

To add the deformation mesh to the deformer first select the deformation mesh, then the simulated mesh (which is the animation mesh) and then go to AdonisFX Menu > Simshape (on the *Edit* group) > Add *Deform Mesh*. A message will notify that the addition of the rest mesh has been done correctly.

### Paint Weights

> [!NOTE]
> AdnSimshape requires the use of the Maya Paint tool (not the AdonisFX paint tool) for the paintable weights setup.

In the case of the AdnSimshape, use the Maya Paint tool to set up and paint its paintable weight attributes. The most important paintable map is the *Attraction Force* as this is the value that dictates how much of each simulated vertex should follow the animation. This value is flooded by default to 1.0, meaning that by default the simulated mesh will follow the animation completely, without displaying dynamics.

In high deformation areas, such as around the mouth or under the eyes, add medium to low values (in this case painting with a value of 0.4).

<figure>
  <img src="images/simple_setup_simshape_02.png"> 
  <figcaption><b>Figure 42</b>: Attraction Force weights for medium dynamics areas.</figcaption>
</figure>

Painting lower Attraction Force weights in meatier areas of the face, such as under the neck or in the cheeks to show more dynamics in these regions. In this case a value of 0.15 will be applied.

<figure>
  <img src="images/simple_setup_simshape_03.png"> 
  <figcaption><b>Figure 43</b>: Attraction Force weights for high dynamics areas.</figcaption>
</figure>

The lowest values (0.1 in this case) will be applied to the area under the jaw where dynamics will appear the most. 

<figure>
  <img src="images/simple_setup_simshape_04.png"> 
  <figcaption><b>Figure 44</b>: Attraction Force weights for highest dynamics areas.</figcaption>
</figure>

After painting similar weights to the ones displayed and pressing playback to check the animation, realistic dynamics should be simulated in the face. Many more paintable weights to better customize and tweak face dynamics are available and fully explained in the documentation for [AdnSimshape](deformers/simshape).

### Add muscle activations

To further have a realistic depiction of facial dynamics, facial muscle activations can be simulated. The AdnSimshape deformer has two methods of handling muscle activations:

 - AdonisFX Muscle Patches file.
 - Edge Evaluator Node.

Refer to this [section](deformers/simshape#muscle-activations) to see how to use Muscle Patches files. However, in this example, it is taken advantage of the AdnEdgeEvaluator Node. To create this node, select the rest mesh, then the deformation mesh, and then go to AdonisFX Menu > Nodes > *Edge Evaluator*. Then, once created, connect it to the AdnSimshape deformer via AdonisFX Menu > Simshape (on the *Edit* group) > *Connect Activations Plug*.

In the attribute editor of the AdnSimshape deformer, under the *Muscles Activation* section, the *Plug Values* will be enabled as a new valid *Activation Mode* option. To better visualize activations, press the ![AdnMuscle](images/adn_simshape_debugger.png){style="width:4%"} shelf button or go to AdonisFX Menu > Simshape (on the *Edit* group) > *Activations Debugger*.
