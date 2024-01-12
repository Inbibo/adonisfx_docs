# How To Use

Skin is a Maya deformer for fast, robust and easy-to-configure skin simulation for digital assets. Thanks to the combination of internal and external constraints, the deformer can produce dynamics that allow the skin mesh to realistically react to the deformations of the internal tissues (e.g. muscles, fascia) over time.

## Requirements

The Skin deformer requires the following inputs to be provided:

  - <b class="mesh_color"> Reference Mesh (R) </b> to drive the simulation skin (e.g. fascia or combined muscles).
  - <b class="mesh_color"> Skin Mesh (S) </b> where the skin deformer will be applied to.

## Create Skin

1. Select the meshes in the following order:
    ``` mermaid
    graph LR
      A["Reference Mesh\n"] --> B;
      B["Skin Mesh\n"];
    ```
2. Press ![Skin button](../img/adn_skin_sim.png) in the AdonisFX shelf or Skin in the AdonisFX menu.
3. Skin is ready to simulate with default settings. Check [this page](attributes.md#attributes) to customize the configuration.

## Paintable Weights

In order to provide more artistic control, some key parameters of the skin solver are exposed as paintable attributes in the deformer. The [AdonisFX Paint Tool](how_to_use.md#adonisfx-paint-tool) must be used to paint those parameters to ensure that the values satisfy the solver requirements.

- *Hard Constraints*: weight to modulate the correction applied to the vertices to keep them at a constant transformation local to the closest point on the reference mesh at initialization. The recommendation for a biped or quadruped creature is to use a maximum value of 1.0 on the wrists, ankles and hips and a value of 0.2 on the rest of the body.
- *Slide Constraints*: weight to modulate the correction applied to the vertices to keep them at a constant distance to the reference mesh sliding along the reference surface. In the example of a biped or quadruped, we recommend a value of 1.0 on the scapulas, shoulders, elbows and knees and a value of 0.2 on the rest of the body.
- *Soft Constraints*: weight to modulate the correction applied to the vertices to keep them at a constant distance to the closest point on the reference mesh at initialization. An intermediate value of 0.5 on the whole geometry is recommended.
- *Compression Resistance*: force to correct the edge lengths if the current length is smaller than the rest length. A higher value represents higher correction.
- *Stretching Resistance*: force to correct the edge lengths if the current length is greater than the rest length. A higher value represents higher correction.

<figure>
  <img src="../img/skin_paint_example.png" caption="AdonisFX Paint Tool"> 
  <figcaption>Figure 1: Example of painted weights on the skin of a bear character. From left to right: Hard Constraints, Slide Constraints and Soft Constraints.</figcaption>
</figure>

!!! Note
    - *Hard*, *Soft* and *Slide* values are normalized for each vertex. Make sure to paint the values that you want to give priority to at the end in order to avoid the internal normalization override them in further strokes.

### AdonisFX Paint Tool

To configure the paintable attributes in the skin deformer, the AdonisFX paint tool must be used. Apart from the standard functionalities that the Maya default paint context provides, this tool also processes the painted weights to guarantee that the requirements of solver are satisfied.

<figure>
  <img src="../img/paint_tool.png" caption="AdonisFX Paint Tool"> 
  <figcaption>Figure 2: AdonisFX Paint Tool</figcaption>
</figure>

Do the following to open the tool:

  1. Select the mesh with the Skin deformer applied to.
  2. Press the paint tool ![paint tool](../img/adn_paint_tool.png) shelf button or go to AdonisFX menu > Paint Tool.

You can select the attribute to paint from the combo box exposed in the UI:

<figure style="margin-left:30%;" markdown> 
  ![Pain Tool Skin Attributes example](../img/paint_tool_skin_attributes.png) 
  <figcaption> Figure 3: Paintable attributes listed in the UI. </figcaption>
</figure>
