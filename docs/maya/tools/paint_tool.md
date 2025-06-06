# Paint Tool

The **AdonisFX Paint Tool** is meant to be used for the manipulation of the paintable attributes of the AdnSkin, AdnMuscle and AdnRibbonMuscle deformers. Its functionalities are very similar to the standard Maya paint tool functionalities plus the ability to paint attributes with multiple influences (e.g. attachment to transform constraints) where a single vertex can adopt a different weight value for the same attribute driven by multiple influent external objects. Also, it ensures the normalization of dependent attributes like hard, soft and slide constraints in AdnSkin deformer.

<figure>
  <img src="../images/tools_paint_tool.png" caption="AdonisFX Paint Tool"> 
  <figcaption><b>Figure 1</b>: AdonisFX Paint Tool.</figcaption>
</figure>

The use of this tool is required for the correct setup of skin, muscle and ribbon muscle solvers. After every stroke, the internal logic processes the painted map and updates all dependent maps to keep the configuration of the solver safe. For example, if the influence of one target of an AdnMuscle which has two targets assigned is painted, then the tool will update the weights of the other target to ensure that the addition of both is normalized at each vertex (the normalization process is independent for transform and geometry targets). The same applies if hard constraints of an AdnSkin deformer are painted: the soft and slide constraints maps will be updated internally to keep the addition of the three maps normalized. Thanks to this logic, switching attributes (see Figure 2 and Figure 3) or selecting influences (see Figure 4) from the AdonisFX Paint Tool provides automatic feedback to the user of the current status of all the maps.

> [!NOTE]
> AdnSimshape and AdnSkinMerge do not require this tool. Their paintable maps can be manipulated through the standard Maya paint context.

To open the tool:

  1. Select the mesh with the AdonisFX deformer applied to.
  2. Press the paint tool ![paint tool](../images/adn_paint_tool.png){style="width:4%"} shelf button or go to AdonisFX Menu > *Paint Tool*.

> [!NOTE]
> - The paint context is configured from the given selection to allow painting.
> - Make sure to select the transform node of the mesh.
> - If the context does not allow painting, it is probably because the selected node is not a transform mesh node with an AdonisFx paintable deformer. Please, select the transform mesh node and click *Refresh From Selection* or restart the AdonisFX Paint Tool.

If the selection provided is valid, meaning the selected mesh has one of the AdonisFX deformers listed before, then the paint context will get configured and the user can paint. The map to be painted is the one associated with the selected attribute in the enumerator exposed at the top of the UI.

> [!NOTE]
> - With the optimizations introduced to the AdonisFX Paint Tool in version 1.4.0, the AdnWeightsDisplayNode is deprecated and no longer needed.
> - This deprecation is fully backward-compatible, meaning that scenes created in earlier versions will continue to work seamlessly in version 1.4.0.
> - In addition, we recommend using the utility available under AdonisFX Menu > Utils > *Upgrade Deprecated Nodes*, which safely removes any instances of the AdnWeightsDisplayNode from your scenes.

Depending on the deformer and the attribute selected the UI can adjust to support multi-influence attributes by exposing the influences or restricting certain functionalities of the tool. In the following sections, the specific behavior of the tool for each deformer is presented.

### Paint Tool on AdnMuscle and AdnRibbonMuscle

In the specific case of muscle deformers, the tool will display the following attributes:

<figure markdown>
  ![Paint Tool Muscle Attributes example](../images/tools_paint_tool_muscle_attributes_00.png) 
  <figcaption><b>Figure 2</b>: Paintable attributes in AdonisFX muscle deformer (Part 1). </figcaption>
</figure>

<figure markdown>
  ![Paint Tool Muscle Attributes example](../images/tools_paint_tool_muscle_attributes_01.png) 
  <figcaption><b>Figure 3</b>: Paintable attributes in AdonisFX muscle deformer (Part 2). </figcaption>
</figure>

  - **Attachments To Geometry** and **Attachments To Transform**
    - If any of these attribute types is selected, then a list widget is shown with the names of the targets connected to the deformer (see Figure 4).
    - Select the desired target to paint from the list widget and paint the weight values.
    - When selecting a target in the list, the object will also get selected in the scene, facilitating its identification.
    - If more than one target was added to the system, then the paint tool will normalize the weights automatically after a stroke has been completed, meaning that the sum of all attachment constraint weights in a vertex will always add up to a maximum value of 1.0.
    - If any target is removed or added to the system, then the paint tool will refresh the list on mouse hover over the UI.

    <figure>
      <img src="../images/tools_paint_tool_attachment_attribute.png"> 
      <figcaption><b>Figure 4</b>: AdonisFX Paint Tool listing multiple transform attachments.</figcaption>
    </figure>

  - **Compression Resistance** and **Stretching Resistance**
    - Compression resistance is set to 1.0 by default. With this value, the solver will apply the corrections to the edges needed to keep the lengths at rest. Set values lower than 1.0 to linearly reduce the amount of correction applied by the solver when the edges get compressed.
    - Stretching resistance is set to 1.0 by default. With this value, the solver will apply the corrections to the edges needed to keep the lengths at rest. Set values lower than 1.0 to linearly reduce the amount of correction applied by the solver when the edges get stretched.
  - **Fibers**
    - When selecting the fibers attribute, the fibers debugger will automatically get enabled, displaying the muscle fibers.
    - The initial direction displayed will be the one estimated by tendon weights.
    - To modify the fibers direction, comb the fibers towards the desired direction.
    - For better precision adjust the set direction using the *Smooth* brush.
    - To get all fibers more tightly aligned in a homogeneous way, press the flood button while having the *Smooth* brush selected.
  - **Fibers Multiplier**
    - Fibers Multiplier is set to 1.0 by default. With this value the solver will apply the activation uniformly throughout the muscle.
    - Set a value lower than 1.0 to decrease the effect of the activation in those areas. For example, paint only the belly of the muscle to 1.0 to concentrate activations in that area and paint the map to 0.0 in the tendinous area.
  - **Global Damping**
    - By default, this map is set to 1.0.
    - This value is scaled by the *Global Damping Multiplier* during simulation to control the amount of damping the solver will apply at each vertex.
  - **Masses**
    - Masses are set to 1.0 by default. This will mean that by default the solver will consider that the muscle has a uniform mass.
  - **Shape Preservation**
    - Shape preservation weights are set to 0.0 by default in AdnMuscle and AdnRibbonMuscle. Modify this value to allow the solver to apply corrections to the current vertex to maintain the initial state of the shape formed with the surrounding vertices.
  - **Slide On Geometry**
    - If this attribute is selected, a list widget is shown with the names of the targets connected to the deformer (see Figure 4).
    - Select the desired target to paint from the list widget and paint the weight values.
    - When selecting a target in the list, the object will also get selected in the scene, facilitating its identification.
    - If more than one target was added to the system, then the paint tool will normalize the weights automatically after a stroke has been completed, meaning that the sum of all sliding on geometry constraint weights in a vertex will always add up to a maximum value of 1.0.
    - If any target is removed or added to the system, then the paint tool will refresh the list on mouse hover over the UI.
  - **Slide On Segment**
    - Slide on Segment Constraints operate similarly to attachment constraints, as they are both multi-influence attributes.
    - The entries in the list widget correspond in this case to the segments added to the constraint, with the name of the segment being "*root_transform* - *tip_transform*".
    - Select the desired segment to paint from the list widget and paint the weight values.
    - When selecting a segment in the list the two scene objects that form the root and tip of the segment will get selected as well, facilitating their identification.
    - If more than one segment was added to the system, then the paint tool will normalize the weights automatically after a stroke has been completed, meaning that the addition of all slide on segment constraint weights in a vertex will always add up to a maximum value of 1.0.

    <figure>
      <img src="../images/tools_paint_tool_sos_attribute.png"> 
      <figcaption><b>Figure 5</b>: AdonisFX Paint Tool listing multiple segments.</figcaption>
    </figure>

  - **Sliding Distance Multiplier**
    - Sliding distance Multiplier is set to 1.0 by default. With this value, every vertex of the geometry will be able to slide along every vertex of the target surface.
    - It is suggested to lower the value in those areas where slide constraints are less relevant or not present for better performance without losing quality.
  - **Tendons**
    - It is recommended to paint values of 1.0 wherever the tendon tissue is and values of 0.0 in the rest of the mesh.
    - This painting will internally trigger an automatic estimation of fibers direction which can be displayed using the debug functionalities of the deformer.

> [!NOTE]
> - Fibers and Tendon weights should only be painted on the initialization frame for AdnMuscle and AdnRibbonMuscle, being the initialization frame the lowest value between Preroll Start Time and Start Time.
> - Some of the Paint Tool's paintable attributes will be disabled given certain conditions in the scene, like for example a time constraint. For example, Fibers and Tendons are not supposed to be paintable on a frame that is not the initialization frame and will be disabled in the Paint Tool UI if on a simulated frame. Hovering over the disabled attribute can inform about the action to be taken to remedy the warning.

### Paint Tool on AdnSkin

In the specific case of an AdnSkin deformer, the tool will display the following attributes:

<figure markdown> 
  ![Paint Tool Skin Attributes example](../images/tools_paint_tool_skin_attributes.png) 
  <figcaption><b>Figure 6</b>: Paintable attributes listed in the UI for an AdnSkin deformer. </figcaption>
</figure>

  - **Compression Resistance** and **Stretching Resistance**
    - Compression resistance is set to 1.0 by default. With this value, the solver will apply the corrections to the edges needed to keep the lengths at rest. Set values lower than 1.0 to linearly reduce the amount of correction applied by the solver when the edges get compressed.
    - Stretching resistance is set to 1.0 by default. With this value, the solver will apply the corrections to the edges needed to keep the lengths at rest. Set values lower than 1.0 to linearly reduce the amount of correction applied by the solver when the edges get stretched.
  - **Global Damping**
    - By default, this map is set to 1.0.
    - This value is scaled by the *Global Damping Multiplier* during simulation to control the amount of damping the solver will apply at each vertex.
  - **Hard Constraints**
    - Hard constraints are set to 1.0 by default. With this value the solver will apply the corrections to the vertices needed to keep them at a constant transformation, local to the closest point on the closest target mesh at initialization.
    - This value is normalized alongside Soft Constraints and Slide Constraints.
  - **Masses**
    - Masses are set to 1.0 by default. This will mean that by default the solver will consider that the skin has a uniform mass.
  - **Shape Preservation**
    - Shape preservation weights are set to 0.0 by default in AdnSkin. Modify this value to allow the solver to apply corrections to the current vertex to maintain the initial state of the shape formed with the surrounding vertices.
  - **Slide Constraints**
    - Slide constraints are set to 0.0 by default. Modify this value to allow the solver to apply corrections to the vertices regarding the sliding of the simulated mesh along the target surface.
    - This value is normalized alongside Hard Constraints and Soft Constraints.
  - **Sliding Distance Multiplier**
    - Sliding distance Multiplier is set to 1.0 by default. With this value, every vertex of the geometry will be able to slide along every vertex of the target surface.
    - It is suggested to lower the value in those areas where slide constraints are less relevant or not present for better performance without losing quality.
  - **Soft Constraints**
    - Soft constraints are set to 0.0 by default. Modify this value to allow the solver to apply corrections to the vertices regarding the vertices keeping a constant distance to the closest point on the closest target mesh.
    - This value is normalized alongside Hard Constraints and Slide Constraints.