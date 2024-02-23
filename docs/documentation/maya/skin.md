# AdnSkin

AdnSkin is a Maya deformer for fast, robust and easy-to-configure skin simulation for digital assets. Thanks to the combination of internal and external constraints, the deformer can produce dynamics that allow the skin mesh to realistically react to the deformations of internal tissues (e.g. muscles, fascia) over time.

The influence these constraints have on the simulated mesh can be freely modified by painting them via the [AdonisFX Paint Tool](tools.md#adonisfx-paint-tool) or by uniformly regulating their influence via multipliers in the Attribute Editor. Besides the maps and multipliers there are many other parameters to regulate the skin's dynamics and behaviour to a wide array of options.

# How to Use

The AdnSkin deformer is of great simplicity to set up and apply to a mesh within a Maya scene. The way this deformer works, a reference mesh (with deformation over time) is set in the scene, over which the skin mesh (simulated mesh) is applied with the deformer.

## Requirements

To create an AdnSkin deformer within a Maya scene, the following inputs must be provided:

  - **Reference Mesh (R)**: Mesh to drive the simulation skin (e.g. fascia or combined muscles).
  - **Skin Mesh (S)**: Mesh to apply the deformer onto.

## Create AdnSkin

The process to create an AdnSkin deformer is the following:

1. Select the reference mesh, then the geometry to simulate.
2. Press ![Skin button](images/adn_skin.png) in the AdonisFX shelf or *Skin* in the AdonisFX menu, under the *Create* section. If the shelf button is double-clicked or the option box in the menu is selected a window will be displayed where a custom name and initial attribute values can be set.
3. AdnSkin is ready to simulate with default settings. Check [this section](#attributes) to customize the configuration.

## Paintable Weights

In order to provide more artistic control, some key parameters of the AdnSkin solver are exposed as paintable attributes in the deformer. The [AdonisFX Paint Tool](tools.md#adonisfx-paint-tool) must be used to paint those parameters to ensure that the values satisfy the solver requirements.

- **Hard Constraints**: Weight to modulate the correction applied to the vertices to keep them at a constant transformation, local to the closest point on the reference mesh at initialization. Hard Constraint maps will force the geometry points to keep the original position. A low value of *Hard Constraints* may be desired to allow the skin to create wrinkles and sliding effect.

    - *Tip*: Flood the geometry with a very low value 0.1 - 0.2. Give a value of 1.0 to the edges of the skin to guarantee that is properly attached to the target geometry.

    - *Tip*: Smooth the borders by using the Smooth and Flood combination to make sure that there are no discontinuities in the weights map. This will help the simulation to not produce sharp differences in the dynamics of every vertex compared to its connected vertices.

- **Soft Constraints**: Weight to modulate the correction applied to the vertices to keep them at a constant distance to the closest point on the reference mesh at initialization. Painting these constraint weights would allow the deformer to create a wrinkle effect when combined with hard and slide weights.

    - *Tip*: Flood the geometry with a very low value 0.1 - 0.2.

    - *Tip*: To optimize the painting of the weight, flood it to 1.0 as a starting point and tweak some areas later on as the results of the skin simulation are seen.

- **Slide Constraints**: Weight to modulate the correction applied to the vertices to keep them at a constant distance to the reference mesh sliding along the reference surface. In the example of a biped or quadruped creature, it is recommended to set a value of 1.0 on the scapulas, shoulders, elbows and knees and an overall value of 0 on the rest of the body.

    - *Tip*: Smooth the borders by using the Smooth and Flood combination to make sure that there are no discontinuities in the weights map. This will help the simulation to not produce sharp differences in the dynamics of every vertex compared to its connected vertices.

- **Compression Resistance**: Force to correct the edge lengths if the current length is smaller than the rest length. A higher value represents higher correction. At value 1 the points in the geometry will try to stay as close as possible to their original position.

    - *Tip*: To optimize the painting of the weight, flood it to 1.0 as a starting point and tweak some areas later on as the results of the skin simulation are seen.
    
    - *Tip*: Reducing the value of the weight in some areas will contribute to getting rid of unwanted wrinkles or possible artifacts in the skin.

- **Stretching Resistance**: Force to correct the edge lengths if the current length is greater than the rest length. A higher value represents higher correction.

    - *Tip*: To optimize the painting of the weight, flood it to 1.0 as a starting point and tweak some areas later on as the results of the skin simulation are seen.

    - *Tip*: Smooth the borders by using the Smooth and Flood combination to make sure that there are no discontinuities in the weights map. This will help the simulation to not produce sharp differences in the dynamics of every vertex compared to its connected vertices.

- **Global Damping**: Set global damping per vertex in the simulated mesh. The greater the value per vertex is the more it will attempt to retain its previous position.

- **Max Sliding Multiplier**: Determines the size of the sliding area per vertex. It corresponds to the maximum distance to the closest point on the reference mesh computed on initialization. Greater values will allow for greater sliding but will have a greater computational cost.
    
    - *Tip*: For areas where sliding is not required paint to 0. Use values closer to 1 in areas where more sliding freedom should be prioritized.

- **Mass**: Set individual mass values per vertex in the simulated mesh.

<figure>
  <img src="images/skin_paint_example.png" caption="AdonisFX Paint Tool"> 
  <figcaption><b>Figure 1</b>: Example of painted weights on the skin of a bear character. From left to right: *Hard Constraints*, *Slide Constraints* and *Soft Constraints*.</figcaption>
</figure>

> [!NOTE]
> - *Hard*, *Soft* and *Slide* values are normalized for each vertex. Make sure to paint the values that you want to give priority to at the end in order to avoid the internal normalization override them in further strokes.

# Attributes

#### Solver Attributes
 - **Enable** (Boolean, True): Flag to enable or disable the deformer computation.
 - **Iterations** (Integer, 3): Number of iterations that the solver will execute per simulation step. Greater values mean greater computational cost.
     - Has a range of \[1, 10\]. Upper limit is soft, higher values can be used.
 - **Material** (Enumerator, "Leather"): Solver stiffness presets per material. The materials are listed from lowest to highest stiffness. There are 7 different presets:
    <ul><li>Fat: 10^7^</li><li>Muscle: 5e^3^</li><li>Rubber: 10^6^</li><li>Tendon: 5e^7^</li><li>Leather: 10^8^</li><li>Wood: 6e^9^</li><li>Concrete: 2.5e^10^</li></ul>
 - **Stiffness Multiplier** (Float, 1.0): Multiplier factor to scale up or down the material stiffness.
     - Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used.

#### Time Attributes
 - **Preroll Start Time** (Time, *Current frame*): Sets the frame at which the preroll begins. The preroll ends at *Start Time*.
 - **Start Time** (Time, *Current frame*): Determines the frame at which the simulation starts.
 - **Current Time** (Time, *Current frame*): Current playback frame.

#### Scale Attributes
 - **Time Scale** (Float, 1.0): Sets the scaling factor applied to the simulation time step.
    - Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used.
 - **Space Scale** (Float, 1.0): Sets the scaling factor applied to the masses and/or the forces.
    - Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used.
 - **Space Scale Mode** (Enumerator, "Masses + Forces"): Determines if the spatial scaling affects the masses, the forces, or both. The available options are:
    - Masses: The *Space Scale* only affects masses.
    - Forces: The *Space Scale* only affects forces.
    - Masses + Forces: The *Space Scale* only affects masses and forces.

#### Gravity
 - **Gravity** (Float, 0.0): Sets the magnitude of the gravity acceleration.
    - Has a range of \[0.0, 100.0\]. Upper limit is soft, higher values can be used.
 - **Gravity Direction** (Float3, {0.0. -1.0, 0.0}): Sets the direction of the gravity acceleration.
    - Vectors introduced do not need to be normalized, but they will get normalized internally.

### Advanced Settings

#### Stiffness Settings
 - **Use Custom Stiffness** (Boolean, False): Toggles the use of a custom stiffness value.
    - If we use a custom stiffness, *Material* and *Stiffness Multiplier* will be disabled and *Stiffness* will be used instead.
 - **Stiffness** (Float, 10^5^): Sets the custom stiffness value.
    - Its value must be greater than 0.0.

#### Dynamic Properties
 - **Global Mass Multiplier** (Float, 1.0): Sets the scaling factor applied to the mass of every point.
    - Has a range of \[0.0, 10.0\]. Upper limit is soft, higher values can be used.
 - **Global Damping** (Float, 0.75): Sets the scaling factor applied to the global damping of every point.
    - Has a range of \[0.0, 1.0\]. Upper limit is soft, higher values can be used.
 - **Inertia Damper** (Float, 0.0): Sets the linear damping applied to the dynamics of every point.
    - Has a range of \[0.0, 1.0\].
 - **Rest Length Multiplier** (Float, 1.0): Sets the scaling factor applied to the edge lengths at rest.
    - Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used.
 - **Max Sliding Distance** (Float, 0.5): Determines the size of the sliding area. It corresponds to the maximum distance to the closest point on the reference mesh computed on initialization.
    - The higher this value is, the higher quality and the lower performance.
    - Has a range of \[0.0, 10.0\]. Upper limit is soft, higher values can be used.
 - **Compression Multiplier** (Float, 1.0): Sets the scaling factor applied to the compression resistance of every point.
    - Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used.
 - **Stretching Multiplier** (Float, 1.0): Sets the scaling factor applied to the stretching resistance of every point.
    - Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used.
 - **Attenuation Velocity Factor** (Float, 1.0): Sets the weight of the attenuation applied to the whole simulation driven by the *Attenuation Matrix*.
    - Has a range of \[0.0, 1.0\].
 - **Sliding Constraints Mode** (Enumerator, "Fast"): Defines the mode of execution for the sliding constraints.
    - *Quality* is more accurate, recommended for final results.
    - *Fast* provides higher performance, recommended for preview.

### Debug attributes

 - **Debug** (Boolean, False): Enable or Disable the debug functionalities in the viewport for the AdnSkin deformer.
 - **Feature** (Enumerator, "Hard Constraints"): A list of debuggable features for this deformer.
     - Hard Constraints: Draw *Hard Constraints* connections from the simulated mesh to the reference mesh.
     - Soft Constraints: Draw *Soft Constraints* connections from the simulated mesh to the reference mesh.
     - Slide Constraints: Draw *Slide Constraints* connections from the simulated mesh to the reference mesh.
 - **Width Scale** (Float, 3.0): Modifies the width of all lines.
 - **Color** (Color picker): Selects the line color from a color wheel. Its saturation can be modified using the slider.

### Connectable attributes
 - **Attenuation Matrix** (Matrix, Identity): Transformation matrix to drive the attenuation.
 - **Reference Mesh** (Mesh): Mesh taken as reference to evaluate external constraints.

## Attribute Editor Template

<figure markdown>
  ![skin editor first part](images/attribute_editor_part_one_skin.png) 
  <figcaption><b>Figure 2</b>: AdnSkin Attribute Editor.</figcaption>
</figure>

<figure markdown>
  ![skin editor second part](images/attribute_editor_part_two_skin.png)
  <figcaption><b>Figure 3</b>: AdnSkin Attribute Editor (Advanced Settings).</figcaption>
</figure>

<figure markdown>
  ![skin editor debug menu](images/attribute_editor_skin_debug.png)
  <figcaption><b>Figure 5</b>: AdnSkin Attribute Editor (Debug menu)</figcaption>
</figure>

## Debugger

In order to better visualize deformer constraints and attributes in the Maya viewport there is the option to enable the debugger, found in the dropdown menu labeled *Debug* in the Attribute Editor.

To enable the debugger the *Debug* checkbox must be marked. To select the specific feature you would like to visualize, choose it from the list provided in *Features*. 

### Debug features

The features that can be visualized with the debugger in the AdnSkin deformer are:

 - **Hard Constraints**: For each vertex, a line will be drawn from the simulated mesh to its corresponding reference point on those vertices where its *Hard Constraints* weight is greater than 0.0.
 - **Soft Constraints**: For each vertex, a line will be drawn from the simulated mesh to its corresponding reference point on those vertices where its *Soft Constraints* weight is greater than 0.0.
 - **Slide Constraints**: For each vertex, a line will be drawn from the simulated mesh to its corresponding reference point on those vertices where its *Slide Constraints* weight is greater than 0.0.

Enabling the debugger and selecting one of these constraints will draw lines from the influenced vertices in the simulated mesh to their corresponding reference vertices. 

<figure markdown>
  ![skin editor debug example](images/skin_debug.png)
  <figcaption><b>Figure 4</b>: Debugger enabled displaying *Hard Constraints*, slide constraints and soft constraints with different configurations. </figcaption>
</figure>
