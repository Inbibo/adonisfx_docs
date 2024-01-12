# How To Use

Volumetric Muscle is a Maya deformer for fast, robust and easy-to-configure volumetric muscle simulation for digital assets. Thanks to the combination of internal (structural) and external (attachments) constraints, this deformer can produce dynamics that allow the mesh to acquire the simulated characteristics of a muscle with realistic volume preservation, fibers activations to modulate the rigidity and attachments properties to external objects to follow the global kinematics of the character.

## Requirements

The Volumetric Muscle deformer requires the following inputs to be provided:

  - <b class="mesh_color"> Attachments </b> to which the simulated muscle will be attached to. Any transform node can be used (e.g. bones, locators, meshes, etc). This input is optional and unlimited.
  - <b class="mesh_color"> Muscle Geometry </b> that the volumetric muscle deformer will be applied onto.

!!! Notes
    - It is not mandatory to select the attachments on creation of the volumetric muscle deformer. We can add and remove attachments after creating the deformer, check this [advanced section](advanced.md#how-to-add-and-remove-attachments) for further details.

## Create Volumetric Muscle

1. Select the attachments (if any) and the geometry in the following order:
    ``` mermaid
    graph LR
      A["N Attachments\n"] --> B;
      B["Muscle\n"];
    ```
2. Press the ![Volumetric Muscle button](../img/adn_muscle_sim.png) button in the AdonisFX shelf or press Volumetric Muscle in the AdonisFX menu. 
3. Volumetric muscle is ready to simulate with default settings. Check [this page](attributes.md#attributes) to customize the configuration.

## Paintable Weights

In order to provide more artistic control, some key parameters of the volumetric muscle solver are exposed as paintable attributes in the deformer. The [AdonisFX Paint Tool](how_to_use.md#adonisfx-paint-tool) must be used to paint those parameters to ensure that the values satisfy the solver requirements.

- *Tendons*: floating values to indicate the source of the muscle fibers. The solver will use that information to make an estimation of the fiber direction at each vertex. We recommend to set a value of 1.0 wherever the tendinous tissue would be in an anatomically realistic muscle and a value of 0.0 in the rest of the mesh.
- *Attachment Constraints*: weight to indicate the influence of each attachment at each vertex of the muscle.
- *Fibers*: the deformer estimates the fiber directions at each vertex based on the tendon weights. In case that the estimated fibers do not fit well to the desired directions, we can use the paint tool to comb the fibers manually. The fibers can be displayed using the [Draw Fibers](attributes.md#debug) option in the deformer 
- *Compression Resistance*: force to correct the edge lengths if the current length is smaller than the rest length. A higher value represents higher correction.
- *Stretching Resistance*: force to correct the edge lengths if the current length is greater than the rest length. A higher value represents higher correction.

<figure>
  <img src="../img/volumetric_paint_example.png"> 
  <figcaption>Figure 1: Example of painted weights on a biceps. From left to right: Tendons weights, Attachment weight for the attachment at the top, Attachment weight for the attachment at the bottom; and Fibers directions at each vertex.</figcaption>
</figure>

!!! Note
    - The attachment weights are normalised at each vertex. This normalisation is applied when a stroke is finished. The use of the AdonisFX painting tool is mandatory for that. The basics of the paint tool are explained in [this section](how_to_use.md#adonisfx-paint-tool).
    - We recommend to paint the values for the most influent attractors at the end in order to avoid the internal normalisation override them in further strokes.

### AdonisFX Paint Tool

To configure the paintable attributes in the Volumetric Muscle deformer, the AdonisFX paint tool must be used. Apart from the standard functionalities that the Maya default paint context provides, this tool also processes the painted weights to guarantee that the requirements of solver are satisfied.

<figure>
  <img src="../img/paint_tool_volumetric.png"> 
  <figcaption>Figure 2: AdonisFX Paint Tool</figcaption>
</figure>

Do the following to open the tool:

  1. Select the mesh with the Volumetric Muscle deformer applied to.
  2. Press the paint tool ![paint tool](../img/adn_paint_tool.png) shelf button or go to AdonisFX menu > Paint Tool.

The selected attribute in the combo box exposed at the top of the UI is the active attribute in the paint context. Now you can use the tool as it was the Artisan's tool from Maya, the behaviour of the different widgets/fields is the same.

<figure style="margin-left:30%;" markdown> 
  ![Pain Tool Skin Attributes example](../img/paint_tool_volumetric_attributes.png) 
  <figcaption style="margin-right:30%"> Figure 3: AdonisFX paint tool displaying the paintable attributes of the deformer. </figcaption> 
</figure>

Following, we present the key aspects to keep in mind while painting each attribute:

  1. Attachment Constraints
    1. If this attribute type is selected, then a list widget is shown with the names of the attachments connected to the Volumetric Muscle deformer.
    2. Select the desired attachment you want to paint from the list widget and paint the weight values.
    3. If more than one attachment was added to the system, then the paint tool will normalise the weights automatically after a stroke has been completed.
    4. If any attachment is removed or added to the system, then the paint tool will refresh the list on mouse hover over the UI.
  2. Tendons
    1. We recommend to paint values of 1.0 wherever the tendon tissue is and values of 0.0 in the rest of the mesh. This painting will internally trigger an automatic estimation of fibers directions.
  3. Fibers
    1. To visualise the fibers, enable the [Draw Fibers](attributes.md#debug) attribute in the deformer or go to the Adonis menu > Edit Muscle > Draw Fibers.
    2. From the deformer Attribute Editor, it is also possible to scale the fibers vectors for debugging purposes.
    3. Comb the fibers towards the desired direction.
  4. Stretching and Compression Resistance
    1. Stretching resistance is set to 1.0 by default. With this value, the solver will apply the corrections to the edges needed to keep the lengths at rest. Set values lower than 1.0 to linearly reduce the amount of correction applied by the solver when the edges get stretched.
    2. Compression resistance is set to 1.0 by default. With this value, the solver will apply the corrections to the edges needed to keep the lengths at rest. Set values lower than 1.0 to linearly reduce the amount of correction applied by the solver when the edges get compressed.