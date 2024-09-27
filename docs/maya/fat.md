# AdnFat

AdnFat is a Maya deformer for realistic simulation of fat tissues. Thanks to the combination of volume preservation and internal and external shape preservation, the deformer can produce dynamics that allow the fat geometry to produce jiggle and folds over time.

### How To Use

The AdnFat deformer is easy to create and confgure in Maya. The deformer can be applied to a mesh that represents the outer surface fat tissue. The deformer requires of a base mesh which will work as the internal surface of the fat tissue. The AdonisFX fat solver will take care of creating the internla structure between the base and simulated meshes procedurally. Typically, the base mesh will be simulated fascia, so that the deformation of that mesh will drive the simulation of the fat volume over time.

To create an AdnFat deformer within a Maya scene, the following inputs must be provided:

  - **Base Mesh (B)**: Mesh to drive the simulation mesh (e.g. the simulated fascia geometry).
  - **Fat Mesh (F)**: Mesh to apply the deformer onto to simulate (e.g. the fat geometry).

The process to create an AdnFat deformer is:

1. Select the **Base Mesh**, then the **Fat Mesh**.
2. Press ![Fat button](images/adn_fat.png){style="width:4%"} in the AdonisFX shelf or *Fat* in the AdonisFX menu, under the *Create > Solvers* section. If the shelf button is double-clicked or the option box in the menu is selected a window will be displayed where a custom name and initial attribute values can be set.
3. A message in the console will notify you that AdnFat has been created properly, meaning that it is ready to simulate with default settings. If an error occurred, a dialog will prompted. Check the next section to customise their configuration.

## Attributes

### Solver Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Enable**               | Boolean    | True    | ✓ | Flag to enable or disable the deformer computation. |
| **Iterations**           | Integer    | 3       | ✓ | Number of iterations that the solver will execute per simulation step. Greater values mean greater computational cost. Has a range of \[1, 10\]. Upper limit is soft, higher values can be used. |
| **Substeps**             | Integer    | 1       | ✓ | Number of substeps that the solver will execute per simulation step. Greater values mean greater computational cost. Has a range of \[1, 10\]. Upper limit is soft, higher values can be used. |
| **Material**             | Enumerator | Fat     | ✓ | Solver stiffness presets per material. The materials are listed from lowest to highest stiffness. There are 7 different presets: Fat: 10<sup>3</sup>, Muscle: 5e<sup>3</sup>, Rubber: 10<sup>6</sup>, Tendon: 5e<sup>7</sup>, Leather: 10<sup>6</sup>, Wood: 6e<sup>9</sup>, Concrete: 2.5e<sup>10</sup>. |
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
| **Space Scale**      | Float      | 1.0             | ✓ | Sets the scaling factor applied to the masses and/or the forces (e.g. gravity). AdonisFX interprets the scene units in centimeters. If modeling your creature you apply a scaling factor for whatever reason (e.g. to avoid precision issues in Maya), you will have to adjust for this scaling factor using this attribute. If your character is supposed to be 170 units tall, but you preferred to model it to be 17 units tall, then you will need to set the space scale to a value of 10. This will ensure that your 17 units creature will simulate as if it was 170 units tall. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Space Scale Mode** | Enumerator | Masses + Forces | ✓ | Determines if the spatial scaling affects the masses, the forces, or both. The available options are: <ul><li>Masses: The *Space Scale* only affects masses.</li><li>Forces: The *Space Scale* only affects forces.</li><li>Masses + Forces: The *Space Scale* affects masses and forces.</li><ul> |

### Gravity
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Gravity**           | Float  | 0.0              | ✓ | Sets the magnitude of the gravity acceleration in m/s<sup>2</sup>. The value is internally converted to cm/s<sup>2</sup>. Has a range of \[0.0, 100.0\]. Upper limit is soft, higher values can be used. |
| **Gravity Direction** | Float3 | {0.0, -1.0, 0.0} | ✓ | Sets the direction of the gravity acceleration. Vectors introduced do not need to be normalised, but they will get normalised internally. |

### Advanced Settings

#### Stiffness Settings
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Use Custom Stiffness**                  | Boolean | False          | ✓ | Toggles the use of a custom stiffness value. If custom stiffness is used, *Material* and *Stiffness Multiplier* will be disabled and *Stiffness* will be used instead. |
| **Stiffness**                             | Float   | 10<sup>5</sup> | ✓ | Sets the custom stiffness value. Its value must be greater than 0.0. |

#### Override Constraint Stiffness
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Solver Stiffness**     | Float |  0.0 | ✗ | Shows the global stiffness value currently used by the solver. |
| **Internal Shape Preservation**   | Float | -1.0 | ✓ | Sets the stiffness override value for the internal shape preservation constraints. If the value is less than 0.0, the global stiffness will be used. Otherwise, this custom stiffness will override the global stiffness. Has a range of \[0.0, 10<sup>12</sup>\]. Upper limit is soft, higher values can be used. |
| **External Shape Preservation**   | Float | -1.0 | ✓ | Sets the stiffness override value for the external shape preservation constraints. If the value is less than 0.0, the global stiffness will be used. Otherwise, this custom stiffness will override the global stiffness. Has a range of \[0.0, 10<sup>12</sup>\]. Upper limit is soft, higher values can be used. |


> [!NOTE]
> Providing a stiffness override value of 0.0 will disable the computation of that constraint.

#### Mass Properties

| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Point Mass Mode**        | Enumerator | By Density       | ✓ | Defines how masses should be used in the solver.<ul><li>*By Density* allows to estimate the mass value by multiplying Density * Area.</li><li>*By Uniform Value* allows to set a uniform mass value.</li></ul> |
| **Density**                | Float      | 900.0            | ✓ | Sets the density value in kg/m<sup>3</sup> to be able to estime mass values with *By Density* mode. The value is internally converted to g/cm<sup>3</sup>. Has a range of \[0.001, 10<sup>6</sup>\]. Lower and upper limits are soft, lower and higher values can be used. |
| **Global Mass Multiplier** | Float      | 1.0              | ✓ | Sets the scaling factor applied to the mass of every point. Has a range of \[0.001, 10.0\]. Lower and upper limits are soft, lower and higher values can be used. |

#### Dynamic Properties
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Global Damping Multiplier**   | Float      | 0.75  | ✓ | Sets the scaling factor applied to the global damping of every point. Has a range of \[0.0, 1.0\]. Upper limit is soft, higher values can be used. |
| **Inertia Damper**              | Float      | 0.0   | ✓ | Sets the linear damping applied to the dynamics of every point. Has a range of \[0.0, 1.0\]. Upper limit is soft, higher values can be used. |
| **Attenuation Velocity Factor** | Float      | 1.0   | ✓ | Sets the weight of the attenuation applied to the velocities of the simulated vertices driven by the *Attenuation Matrix*. Has a range of \[0.0, 1.0\]. Upper limit is soft, higher values can be used. |

#### Volume Structure
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Divisions**   | Integer      | 1  | ✗ | Sets the number of internal divisions to create during the internal structure procedural generation. Has a range of \[1, 10\]. Upper limit is soft, higher values can be used. |

### Debug Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Debug**       | Boolean      | False            | ✓ | Enable or Disable the debug functionalities in the viewport for the AdnFat deformer. |
| **Feature**     | Enumerator   | Volume Structure | ✓ | A list of debuggable features for this deformer.<ul><li>Volume Structure: Draw the *Internal Structure* generated procedurally.</li><li>External Shape Preservation: Draw *Shape Preservation* connections between the vertices adjacent to the vertices with this constraint.</li></ul> |
| **Width Scale** | Float        | 3.0              | ✓ | Modifies the width of all lines. |
| **Color**       | Color Picker |                  | ✓ | Selects the line colour from a colour wheel. Its saturation can be modified using the slider. |

### Deformer Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Envelope** | Float | 1.0 | ✓ | Specifies the deformation scale factor. Has a range of \[0.0, 1.0\]. Upper and lower limits are soft, values can be set in a range of \[-2.0, 2.0\]|

### Connectable Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Attenuation Matrix**  | Matrix | Identity | ✓ | Transformation matrix to drive the attenuation. |
| **Base Mesh**      | Mesh   |          | ✓ | Mesh taken as base to create the fat volume and drive the simulation. |
| **Base Matrix**    | Matrix | Identity | ✓ | World matrix of the base mesh. |

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

In order to provide more artistic control, some key parameters of the AdnFat solver are exposed as paintable attributes in the deformer. The Maya paint tool must be used to paint those parameters to ensure that the values satisfy the solver requirements.

| Name | Default | Description |
| :--- | :------ | :---------- |
| **Global Damping**              | 1.0 | Set global damping per vertex in the simulated mesh. The greater the value per vertex is the more damping of velocities. |
| **Masses**                      | 1.0 | Set individual mass values per vertex in the simulated mesh. |
| **External Shape Preservation** | 0.0 | Amount of correction to apply to the a vertex to maintain the initial state of the shape formed with the surrounding vertices. |
| **Internal Shape Preservation** | 0.0 | Amount of correction to apply to the internal volume to preserve the initial volumetric shape and prevent from distorsion. |

<figure>
  <img src="images/skin_weights.png" caption="AdonisFX Paint Tool"> 
  <figcaption><b>Figure 4</b>: Example of painted weights on the skin of a bear character, labeled as:<br/><b>a)</b> Compression Resistance, <b>b)</b> Global Damping, <b>c)</b> Hard Constraints, <b>d)</b> Mass,<br/><b>e)</b> Shape Preservation, <b>f)</b> Slide Constraints, <b>g)</b> Sliding Distance Multiplier, <b>h)</b> Soft Constraints, and <b>i)</b> Stretching Resistance.</figcaption>
</figure>


## Debugger

In order to better visualise deformer constraints and attributes in the Maya viewport there is the option to enable the debugger, found in the dropdown menu labeled *Debug* in the Attribute Editor.

To enable the debugger the *Debug* checkbox must be marked. To select the specific feature you would like to visualise, choose it from the list provided in *Features*. The features that can be visualised with the debugger in the AdnFat deformer are:

 - **External Shape Preservation**: For each vertex with a external shape preservation weight greater than 0.0, a line will be drawn from each adjacent vertex to the opposite adjacent vertex.
 - **Volume Structure**: A line will be drawn for every connection between two points in the volume. A point can be either a vertex on the base mesh, a vertex on the simulated fat mesh or a virtual point that belongs to an internal layer generated by the procedural construction based on the *Divisions* attribute.

<figure markdown>
  ![skin editor debug example](images/skin_debug.png)
  <figcaption><b>Figure 5</b>: In gray the target mesh, in orange the simulated skin. Debugger enabled displaying a test example with <i>Soft Constraints</i> coloured in green.</figcaption>
</figure>

<figure markdown>
  ![skin editor sliding surface debug](images/skin_debug_slide_surface.png)
  <figcaption><b>Figure 6</b>: In gray the target mesh, in red the simulated skin. Debugger enabled displaying the <i>Sliding Surface</i> coloured in green.</figcaption>
</figure>

<figure markdown>
  ![skin editor distance constraint debug](images/skin_dist_constr_debug.png)
  <figcaption><b>Figure 7</b>: In red the simulated skin. Debugger enabled displaying the <i>Distance Constraints</i> coloured in blue with <i>Triangulate Mesh</i> option disabled (Left) and enabled (Right).</figcaption>
</figure>

<figure markdown>
  ![skin editor shape preservation constraint debug](images/skin_shape_preserve_constr_debug.png)
  <figcaption><b>Figure 8</b>: In red the simulated skin. Debugger enabled displaying the <i>Shape Preservation Constraints</i> coloured in blue with <i>Triangulate Mesh</i> option disabled (Left) and enabled (Right).</figcaption>
</figure>

## Advanced

### Base Mesh

Once the AdnFat deformer is created, it is possible to add and remove the base mesh thanks to some utilities available in the AdonisFX menu.

- **Add Base Mesh**:
    1. Select the geometry to be assigned as base mesh to the AdnFat.
    2. Select the geometry that has the AdnFat deformer applied.
    3. Press the *Add Base Mesh* item in the AdonisFX menu from the Edit Fat submenu.
- **Remove Base Mesh**:
    1. Select the geometry currently assigned as base mesh to the AdnFat. This step is optional.
    2. Select the geometry that has the AdnFat deformer applied.
    3. Press the *Remove Base Mesh* item in the AdonisFX menu from the Edit Fat submenu.

<figure markdown>
  ![skin adding multiple targets](images/skin_add_multiple_targets.png)
  <figcaption><b>Figure 9</b>: Addition of multiple targets (e.g. Adding multiple muscle targets to a fascia/fat/skin simulation).</figcaption>
</figure>
