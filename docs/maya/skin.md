# AdnSkin

AdnSkin is a Maya deformer for fast, robust and easy-to-configure skin simulation for digital assets. Thanks to the combination of internal and external constraints, the deformer can produce dynamics that allow the skin mesh to realistically react to the deformations of internal tissues (e.g. muscles, fascia) over time.

The influence these constraints have on the simulated mesh can be freely modified by painting them via the [AdonisFX Paint Tool](tools#paint-tool) or by uniformly regulating their influence via multipliers in the Attribute Editor. Besides the maps and multipliers there are many other parameters to regulate the skin's dynamics and behaviour to a wide array of options.

### How To Use

The AdnSkin deformer is of great simplicity to set up and apply to a mesh within a Maya scene. The way this deformer works is by applying simulation on top of the skin mesh (simulated mesh) which will be directly coupled to its reference mesh (with deformation over time).

To create an AdnSkin deformer within a Maya scene, the following inputs must be provided:

  - **Reference Mesh (R)**: Mesh to drive the simulation skin (e.g. fascia or combined muscles).
  - **Skin Mesh (S)**: Mesh to apply the deformer onto.

The process to create an AdnSkin deformer is:

1. Select the **Reference Mesh**, then the **Skin Mesh**.
2. Press ![Skin button](images/adn_skin.png){style="width:4%"} in the AdonisFX shelf or *Skin* in the AdonisFX menu, under the *Create* section. If the shelf button is double-clicked or the option box in the menu is selected a window will be displayed where a custom name and initial attribute values can be set.
3. A message box will notify you that AdnSkin has been created properly, meaning that it is ready to simulate with default settings. Check the next section to customise their configuration.

## Attributes

### Solver Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Enable**               | Boolean    | True    | ✓ | Flag to enable or disable the deformer computation. |
| **Iterations**           | Integer    | 3       | ✓ | Number of iterations that the solver will execute per simulation step. Greater values mean greater computational cost. Has a range of \[1, 10\]. Upper limit is soft, higher values can be used. |
| **Material**             | Enumerator | Leather | ✓ | Solver stiffness presets per material. The materials are listed from lowest to highest stiffness. There are 7 different presets: Fat: 10<sup>3</sup>, Muscle: 5e<sup>3</sup>, Rubber: 10<sup>6</sup>, Tendon: 5e<sup>7</sup>, Leather: 10<sup>6</sup>, Wood: 6e<sup>9</sup>, Concrete: 2.5e<sup>10</sup>. |
| **Stiffness Multiplier** | Float      | 1.0     | ✓ | Multiplier factor to scale up or down the material stiffness. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |

### Time Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Preroll Start Time** | Time | *Current frame* | ✗ | Sets the frame at which the preroll begins. The preroll ends at *Start Time*. |
| **Start Time**         | Time | *Current frame* | ✗ | Determines the frame at which the simulation starts. |
| **Current Time**       | Time | *Current frame* | ✓ | Current playback frame. |

### Scale Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Time Scale**       | Float      | 1.0             | ✓ | Sets the scaling factor applied to the simulation time step. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Space Scale**      | Float      | 1.0             | ✓ | Sets the scaling factor applied to the masses and/or the forces. AdonisFX interprets the scene units in meters. Because of that, to simulate external forces in the right scale, the *Space Scale* may need to be adjusted. For example, to apply *Gravity* with a value of 9.8 m/s^2^, the *Space Scale* should be set to 0.01. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Space Scale Mode** | Enumerator | Masses + Forces | ✓ | Determines if the spatial scaling affects the masses, the forces, or both. The available options are: <ul><li>Masses: The *Space Scale* only affects masses.</li><li>Forces: The *Space Scale* only affects forces.</li><li>Masses + Forces: The *Space Scale* affects masses and forces.</li><ul> |

### Gravity
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Gravity**           | Float  | 0.0              | ✓ | Sets the magnitude of the gravity acceleration. Has a range of \[0.0, 100.0\]. Upper limit is soft, higher values can be used. |
| **Gravity Direction** | Float3 | {0.0, -1.0, 0.0} | ✓ | Sets the direction of the gravity acceleration. Vectors introduced do not need to be normalised, but they will get normalised internally. |

### Advanced Settings

#### Stiffness Settings
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Use Custom Stiffness**                  | Boolean | False          | ✓ | Toggles the use of a custom stiffness value. If custom stiffness is used, *Material* and *Stiffness Multiplier* will be disabled and *Stiffness* will be used instead. |
| **Stiffness**                             | Float   | 10<sup>5</sup> | ✓ | Sets the custom stiffness value. Its value must be greater than 0.0. |
| **Override Shape Preserve Stiffness** | Boolean | False          | ✓ | Override the shape preservation stiffness with a custom value. If disabled it will use either the material stiffness or the custom stiffness value. |
| **Shape Preserve Stiffness**              | Float   | 1000.0         | ✓ | Sets the stiffness shape preservation override value. Its value must be greater than 0.0. |

#### Mass Properties

| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Point Mass Mode**        | Enumerator | By Uniform Value | ✓ | Defines how masses should be used in the solver.<ul><li>*By Density* allows to estimate the mass value by multiplying Density * Area.</li><li>*By Uniform Value* allows to set a uniform mass value.</li></ul> |
| **Density**                | Float      | 1100.0           | ✓ | Sets the density value in kg/m<sup>3</sup> to be able to estime mass values with *By Density* mode. Has a range of \[0.001, 10<sup>6</sup>\]. Lower and upper limits are soft, lower and higher values can be used. |
| **Global Mass Multiplier** | Float      | 1.0              | ✓ | Sets the scaling factor applied to the mass of every point. Has a range of \[0.001, 10.0\]. Lower and upper limits are soft, lower and higher values can be used. |

#### Dynamic Properties
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Global Damping Multiplier**   | Float      | 0.75 | ✓ | Sets the scaling factor applied to the global damping of every point. Has a range of \[0.0, 1.0\]. Upper limit is soft, higher values can be used. |
| **Inertia Damper**              | Float      | 0.0  | ✓ | Sets the linear damping applied to the dynamics of every point. Has a range of \[0.0, 1.0\]. Upper limit is soft, higher values can be used. |
| **Rest Length Multiplier**      | Float      | 1.0  | ✓ | Sets the scaling factor applied to the edge lengths at rest. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Max Sliding Distance**        | Float      | 0.0  | ✗ | Determines the size of the sliding area. It corresponds to the maximum distance to the closest point on the reference mesh computed on initialisation. The higher this value is, the higher quality and the lower performance. If the value provided is considered too high for a given reference mesh, a warning will be displayed to the user. Has a range of \[0.0, 10.0\]. Upper limit is soft, higher values can be used.
| **Compression Multiplier**      | Float      | 1.0  | ✓ | Sets the scaling factor applied to the compression resistance of every point. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Stretching Multiplier**       | Float      | 1.0  | ✓ | Sets the scaling factor applied to the stretching resistance of every point. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Attenuation Velocity Factor** | Float      | 1.0  | ✓ | Sets the weight of the attenuation applied to the velocities of the simulated vertices driven by the *Attenuation Matrix*. Has a range of \[0.0, 1.0\]. Upper limit is soft, higher values can be used. |
| **Sliding Constraints Mode**    | Enumerator | Fast | ✓ | Defines the mode of execution for the sliding constraints.<ul><li>*Quality* is more accurate, recommended for final results.</li><li>*Fast* provides higher performance, recommended for preview.</li></ul> |

### Debug Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Debug**       | Boolean      | False            | ✓ | Enable or Disable the debug functionalities in the viewport for the AdnSkin deformer. |
| **Feature**     | Enumerator   | Hard Constraints | ✓ | A list of debuggable features for this deformer.<ul><li>Hard Constraints: Draw *Hard Constraints* connections from the simulated mesh to the reference mesh.</li><li>Shape Preservation: Draw *Shape Preservation* connections between the vertices adjacent to the vertices with this constraint.</li><li>Slide Constraints: Draw *Slide Constraints* connections from the simulated mesh to the reference mesh.</li><li>Sliding Surface On Target: Draw outline of triangles covered by the *Max Sliding Distance* of each vertex.</li><li>Soft Constraints: Draw *Soft Constraints* connections from the simulated mesh to the reference mesh.</li></ul> |
| **Width Scale** | Float        | 3.0              | ✓ | Modifies the width of all lines. |
| **Color**       | Color Picker |                  | ✓ | Selects the line colour from a colour wheel. Its saturation can be modified using the slider. |

### Connectable Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Attenuation Matrix** | Matrix | Identity | ✓ | Transformation matrix to drive the attenuation. |
| **Reference Matrix**   | Mesh   |          | ✓ | Mesh taken as reference to evaluate external constraints. | 

## Attribute Editor Template

<figure markdown>
  ![skin editor first part](images/attribute_editor_part_one_skin.png) 
  <figcaption><b>Figure 1</b>: AdnSkin Attribute Editor.</figcaption>
</figure>

<figure markdown>
  ![skin editor second part](images/attribute_editor_part_two_skin.png)
  <figcaption><b>Figure 2</b>: AdnSkin Attribute Editor (Advanced Settings).</figcaption>
</figure>

<figure markdown>
  ![skin editor debug menu](images/attribute_editor_skin_debug.png)
  <figcaption><b>Figure 3</b>: AdnSkin Attribute Editor (Debug menu).</figcaption>
</figure>

## Paintable Weights

In order to provide more artistic control, some key parameters of the AdnSkin solver are exposed as paintable attributes in the deformer. The [AdonisFX Paint Tool](tools#paint-tool) must be used to paint those parameters to ensure that the values satisfy the solver requirements.

| Name | Default | Description |
| :--- | :------ | :---------- |
| **Compression Resistance**      | 1.0 | Force to correct the edge lengths if the current length is smaller than the rest length. A higher value represents higher correction.<ul><li>*Tip*: To optimise the painting of the weight, flood it to 1.0 as a starting point and tweak some areas later on.</li><li>*Tip*: Reducing the value of the weight in some areas will contribute to reduce wrinkling effect.</li></ul> |
| **Global Damping**              | 1.0 | Set global damping per vertex in the simulated mesh. The greater the value per vertex is the more damping of velocities. |
| **Hard Constraints**            | 1.0 | Weight to modulate the correction applied to the vertices to keep them at a constant transformation, local to the closest point on the reference mesh at initialisation. Hard Constraint maps will force the geometry points to keep the original position. A low value of *Hard Constraints* may be desired to allow the skin to create wrinkles and sliding effect.<ul><li>*Tip*: In the example of a biped or quadruped creature, it is recommended to flood the geometry with a very low value 0.1, and then set a value of 1.0 to the edges of the skin to guarantee that it is properly attached to the target geometry.</li><li>*Tip*: Smooth the borders by using the Smooth and Flood combination to make sure that there are no discontinuities in the weights map. This will help the simulation to not produce sharp differences in the dynamics of every vertex compared to its connected vertices.</li></ul> |
| **Masses**                      | 1.0 | Set individual mass values per vertex in the simulated mesh. |
| **Shape Preservation**          | 0.0 | Amount of correction to apply to the current vertex to maintain the initial state of the shape formed with the surrounding vertices. |
| **Slide Constraints**           | 0.0 | Weight to modulate the correction applied to the vertices to keep them at a constant distance to the reference mesh sliding along the reference surface.<ul><li>*Tip*: In the example of a biped or quadruped creature, it is recommended to set a value of 1.0 on the scapulas, shoulders, elbows and knees and an overall value of 0 on the rest of the body.</li><li>*Tip*: Smooth the borders by using the Smooth and Flood combination to make sure that there are no discontinuities in the weights map. This will help the simulation to not produce sharp differences in the dynamics of every vertex compared to its connected vertices.</li></ul> |
| **Sliding Distance Multiplier** | 1.0 | Determines the size of the sliding area per vertex. It corresponds to the maximum distance to the closest point on the reference mesh computed on initialisation. Greater values will allow for larger sliding areas but will also increase the computational cost.<ul><li>*Tip*: For areas where sliding is not required paint to 0. Use values closer to 1 in areas where more sliding freedom should be prioritised.</li></ul> |
| **Soft Constraints**            | 0.0 | Weight to modulate the correction applied to the vertices to keep them at a constant distance to the closest point on the reference mesh at initialisation. Painting these constraint weights would allow the deformer to create a wrinkle effect when combined with hard and slide weights.<ul><li>*Tip*: In the example of a biped or quadruped creature, it is recommended to flood the geometry with a low value 0.2.</li></ul> |
| **Stretching Resistance**       | 1.0 | Force to correct the edge lengths if the current length is greater than the rest length. A higher value represents higher correction.<ul><li>*Tip*: To optimise the painting of the weight, flood it to 1.0 as a starting point and tweak some areas later on.</li><li>*Tip*: Smooth the borders by using the Smooth and Flood combination to make sure that there are no discontinuities in the weights map. This will help the simulation to not produce sharp differences in the dynamics of every vertex compared to its connected vertices.</li></ul> |

<figure>
  <img src="images/skin_weights.png" caption="AdonisFX Paint Tool"> 
  <figcaption><b>Figure 4</b>: Example of painted weights on the skin of a bear character, labeled as:<br/><b>a)</b> Compression Resistance, <b>b)</b> Global Damping, <b>c)</b> Hard Constraints, <b>d)</b> Mass,<br/><b>e)</b> Shape Preservation, <b>f)</b> Slide Constraints, <b>g)</b> Sliding Distance Multiplier, <b>h)</b> Soft Constraints, and <b>i)</b> Stretching Resistance.</figcaption>
</figure>

> [!NOTE]
> *Hard*, *Soft* and *Slide* values are normalised for each vertex. Make sure to paint the values that you want to give priority to at the end in order to avoid the internal normalisation override them in further strokes.

## Debugger

In order to better visualise deformer constraints and attributes in the Maya viewport there is the option to enable the debugger, found in the dropdown menu labeled *Debug* in the Attribute Editor.

To enable the debugger the *Debug* checkbox must be marked. To select the specific feature you would like to visualise, choose it from the list provided in *Features*. The features that can be visualised with the debugger in the AdnSkin deformer are:

 - **Hard Constraints**: For each vertex, a line will be drawn from the simulated mesh vertex to the corresponding point on the reference mesh if its *Hard Constraints* weight is greater than 0.0.
 - **Shape Preservation**: For each vertex with a shape preservation weight greater than 0.0, a line will be drawn from each adjacent vertex to the opposite adjacent vertex.
 - **Slide Constraints**: For each vertex, a line will be drawn from the simulated mesh vertex to the corresponding point on the reference mesh if its *Slide Constraints* weight is greater than 0.0.s
 - **Sliding Surface On Target**: For each vertex, lines will outline the target triangles within the reach of its *Max Sliding Distance*.
 - **Soft Constraints**: For each vertex, a line will be drawn from the simulated mesh vertex to the corresponding point on the reference mesh if its *Soft Constraints* weight is greater than 0.0.

<figure markdown>
  ![skin editor debug example](images/skin_debug.png)
  <figcaption><b>Figure 5</b>: In gray the reference mesh, in orange the simulated skin. Debugger enabled displaying a test example with <i>Soft Constraints</i> coloured in green.</figcaption>
</figure>

<figure markdown>
  ![skin editor sliding surface debug](images/skin_debug_slide_surface.png)
  <figcaption><b>Figure 6</b>: In gray the reference mesh, in red the simulated skin. Debugger enabled displaying the <i>Sliding Surface</i> coloured in green.</figcaption>
</figure>
