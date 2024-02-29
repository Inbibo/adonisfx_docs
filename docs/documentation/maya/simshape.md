# AdnSimshape

AdnSimshape is a Maya deformer to produce facial simulation in the animation rig of an asset. Given a facial expression, the deformer is able to compute the activation of the vertices in order to emulate the changes in the rigidity of the skin. As result, the dynamics of the simulated skin mimic the behaviour of internal muscles contracting.

During simulation, the solver reduces the inertias of the vertices with higher values of activation, while it computes standard simulation in the vertices that are not activated. One of the key features of AdnSimshape is the ability to extract muscle information directly from the neutral geometry and the set of deformed geometries with the facial expressions using Machine Learning techniques.

## How to Use

The AdnSimshape deformer is of great simplicity to set up and apply to a mesh within a Maya scene. The combination of a rest mesh, deform mesh and animated mesh allow the system to compute activation values which would drive the behaviour and inertias of the output skin mesh (simulated mesh).

## Requirements

To create an AdnSimshape deformer within a Maya scene, the following inputs must be provided:

  - **Rest Mesh (R)**: Mesh with no deformation or animation (optional).
  - **Deform Mesh (D)**: Mesh with deformation driven by the facial expressions (optional).
  - **Animated Mesh (A)**: Mesh with deformation driven by the facial expressions and animation result of the binding to the animation rig (optional).
  - **Simulation Mesh (S)**: Mesh to apply the deformer to. This mesh can be the animation mesh or a separate mesh with no deformation nor animation.

> [!NOTE]
> - All input geometries must have the same number of vertices.
> - If **R** is not provided, the system will use the initial state of **S** as the rest mesh.
> - If **D** is not provided, the simulation will not produce activations.
> - If **A** is not provided, the system will use the input mesh to the deformer (**S**) as animated mesh.

## Create AdnSimshape

When initially creating an AdnSimshape deformer, it is possible to add both a **Simulated Mesh** and a **Rest Mesh**, or only add a **Simulated Mesh**. The process to create an AdnSimshape deformer is the following:

  1. Select the **Rest Mesh** (optional), then the **Simulated Mesh**.
    - The deformer can also be applied to the **Animated Mesh** and use it directly as the **Simulated Mesh**.
  2. Press the ![Simshape button](images/adn_simshape.png) in the AdonisFX shelf or press *Simshape* in AdonisFX menu under the *Create* section. If the shelf button is double-clicked or the option box in the menu is selected a window will be displayed where a custom name and initial attribute values can be set.
  3. A message box will notify that AdnSimshape has been created properly, meaning that it is ready to simulate with default settings. Check the [attributes section](#attributes) to customize the configuration.

In order to add or remove any of the optional meshes, a set of menu items are exposed in AdonisFX menu > Edit Simshape. In that submenu, the options to manage each mesh type can be found. See Figure 1.

<figure style="width:45%" markdown>
  ![Edit Simshape submenu](images/simshape_menu.png)
  <figcaption><b>Figure 1:</b> Edit Simshape submenu.</figcaption>
</figure>

To add any of these meshes to AdnSimshape, follow a similar procedure to when first creating the deformer:

  1. First, select the **Additional Mesh**. then the **Simulated Mesh**.
  2. Press the corresponding menu element in AdonisFX menu > Edit Simshape.
  3. A message box will notify that the action has been successful.

To remove any of these meshes from AdnSimshape follow this procedure:

  1. Select only the mesh with AdnSimshape applied.
  2. Press the corresponding menu element in AdonisFX menu > Edit Simshape.
  3. A message box will notify that the action has been successful.

## Paintable Weights

In order to provide more artistic control, some key parameters of the AdnSimshape solver are exposed as paintable attributes in the deformer. The Maya paint tool must be used to paint those parameters to ensure that the values satisfy the solver requirements.

 - **Attract Force**: Weight to control the amount of influence of the animated mesh. The higher the value is, the more influence and the less dynamics will appear.
    - It's initialized to a flooded value of 1.0
 - **Collision Threshold Multiplier**: Factor to scale the distance vertex-to-collider at rest. It is used to modulate the minimum distance to the collider allowed for each vertex.
    - It's initialized to a flooded value of 1.0
- **Compression Resistance**: Force to correct the edge lengths if the current length is smaller than the rest length. A higher value represents higher correction.
    - It's initialized to a flooded value of 0.0
 - **Global Damping**: Set global damping per vertex in the simulated mesh. The greater the value per vertex the more it will attempt to retain its previous position.
    - It's initialized to a flooded value of 1.0
 - **Mass**: Set individual mass values per vertex in the simulated mesh.
    - It's initialized to a flooded value of 1.0
 - **Slide Collision Constraints**: Represents for which areas collisions should be computed against the collider.
    - It's initialized to a flooded value of 0.0
    - A value of 0.0 does not apply correction at all, while a value of 1.0 does apply the correction to fix intersections. 
- **Stretching Resistance**: Force to correct the edge lengths if the current length is greater than the rest length. A higher value represents higher correction.
    - It's initialized to a flooded value of 1.0

# Attributes

#### Solver Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Enable**               | Boolean    | True    | ✓ | Flag to enable or disable the deformer computation. |
| **Iterations**           | Integer    | 3       | ✓ | Number of iterations that the solver will execute per simulation step. Greater values mean greater computational cost. Has a range of \[1, 10\]. Upper limit is soft, higher values can be used. |
| **Material**             | Enumerator | Leather | ✓ | Solver stiffness presets per material. The materials are listed from lowest to highest stiffness. There are 7 different presets: Fat: 10<sup>3</sup>, Muscle: 5e<sup>3</sup>, Rubber: 10<sup>6</sup>, Tendon: 5e<sup>7</sup>, Leather: 10<sup>6</sup>, Wood: 6e<sup>9</sup>, Concrete: 2.5e<sup>10</sup>. |
| **Stiffness Multiplier** | Float      | 1.0     | ✓ | Multiplier factor to scale up or down the material stiffness. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |

#### Muscles Activation Settings
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Activation Mode**          | Enumerator | No activation | ✗ | Mode to drive the muscle activations. There are 3 different modes: <ul><li>Muscle Patches (Disabled by default): An Adonis Muscle Patches file ([.amp](#generate-muscle-patches)) has to be provided to enable this option.</li><li>Plug Values (Disabled by default): The attribute values ActivationList.Activation should be populated to enable this option. The activation data will be read from the plug values.</li><li>No Activation (Enabled by default): No activation is read.</li></ul> |
| **Muscle Patches File**      | String     |               | ✗ | Path to the Adonis Muscle Patches file ([.amp](#generate-muscle-patches)). |
| **Activation Smoothing**     | Integer    | 1             | ✗ | Number of iterations for the activation smoothing algorithm. The greater the number, the smoother the activations per patch will be. Has a range of \[1, 20\]. Upper limit is soft, higher values can be used. |
| **Bidirectional Activation** | Boolean    | False         | ✗ | Flag to enable muscle activations in the positive and negative directions of the muscle patches fibers. |
| **Write Out Activation**     | Boolean    | False         | ✗ | Flag to toggle the writing of activations into an output plug. |

#### Time Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Preroll Start Time** | Time | *Current frame* | ✗ | Sets the frame at which the pre-roll begins. The pre-roll ends at *Start Time*. |
| **Start Time**         | Time | *Current frame* | ✗ | Determines the frame at which the simulation starts. |
| **Current Time**       | Time | *Current frame* | ✗ | Current playback frame. |

#### Scale Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Time Scale**       | Float      | 1.0             | ✓ | Sets the scaling factor applied to the simulation time step. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Space Scale**      | Float      | 1.0             | ✓ | Sets the scaling factor applied to the masses and/or the forces. Adonis interprets the scene units in meters. Because of that, to simulate external forces in the right scale, the *Space Scale* may need to be adjusted. For example, to apply *Gravity* with a value of 9.8 m/s^2^, the *Space Scale* should be set to 0.01. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Space Scale Mode** | Enumerator | Masses + Forces | ✓ | Determines if the spatial scaling affects the masses, the forces, or both. The available options are: <ul><li>Masses: The *Space Scale* only affects masses.</li><li>Forces: The *Space Scale* only affects forces.</li><li>Masses + Forces: The *Space Scale* only affects masses and forces.</li><ul> |

#### Gravity
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Gravity**           | Float  | 0.0              | ✓ | Sets the magnitude of the gravity acceleration. Has a range of \[0.0, 100.0\]. Upper limit is soft, higher values can be used. |
| **Gravity Direction** | Float3 | {0.0, -1.0, 0.0} | ✓ | Sets the direction of the gravity acceleration. Vectors introduced do not need to be normalized, but they will get normalized internally. |

### Advanced Settings

#### Stiffness Settings
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Use Custom Stiffness** | Boolean | False          | ✓ | Toggles the use of a custom stiffness value. If custom stiffness is used, *Material* and *Stiffness Multiplier* will be disabled and *Stiffness* will be used instead. |
| **Stiffness**            | Float   | 10<sup>5</sup> | ✓ | Sets the custom stiffness value. Its value must be greater than 0.0. |

#### Dynamic Properties
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Global Mass Multiplier**      | Float | 1.0  | ✓ | Sets the scaling factor applied to the mass of every point. Has a range of \[0.0, 10.0\]. Upper limit is soft, higher values can be used. |
| **Global Damping Multiplier**   | Float | 0.75 | ✓ | Sets the scaling factor applied to the global damping of every point. Has a range of \[0.0, 1.0\]. Upper limit is soft, higher values can be used. |
| **Inertia Damper**              | Float | 0.0  | ✓ | Sets the linear damping applied to the dynamics of every point. Has a range of \[0.0, 1.0\]. Upper limit is soft, higher values can be used. |
| **Rest Length Multiplier**      | Float | 1.0  | ✓ | Sets the scaling factor applied to the edge lengths at rest. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Compression Multiplier**      | Float | 1.0  | ✓ | Sets the scaling factor applied to the compression resistance of every point. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Stretching Multiplier**       | Float | 1.0  | ✓ | Sets the scaling factor applied to the stretching resistance of every point. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Attenuation Velocity Factor** | Float | 1.0  | ✓ | Sets the weight of the attenuation applied to the velocities of the simulated vertices driven by the *Attenuation Matrix*. Has a range of \[0.0, 10.0\]. Upper limit is soft, higher values can be used. |

#### Collision Settings
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Compute Collisions**   | Boolean | True | ✗ | Flag to enable collisions correction in the deformer. If disabled, the deformer will ignore colliders when deforming the mesh. |
| **Keep Orientation**     | Boolean | True | ✗ | Flag to preserve the initial orientation of the vertices relative to the collider when handling collisions. If disabled, the mesh will suffer no changes if the orientation of the collider varies. |
| **Max Sliding Distance** | Float   | 1.0  | ✗ | Maximum distance (in world units) the simulated vertex is allowed to slide relative to the collider. Has a range of \[0.0, 10.0\]. Upper limit is soft, higher values can be used. |

#### Attraction Settings
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Attraction Multiplier** | Float      | 1.0       | ✓ | Sets the scaling factor applied to the Attraction. Has a range of \[0.0, 2.0\]. Upper limit is soft, higher values can be used. |
| **Attraction Remap Mode** | Enumerator | Cube Root | ✓ | Remap mode used to compute the definitive attraction values. There are 4 different modes that folow different remap methods: Linear, Logarithmic, Square Root, Cube Root. |

#### Initialization Settings
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Animatable Rest Mesh**    | Boolean | False | ✗ | Flag that enables reading animated rest mesh data. |
| **Initialize to Anim Mesh** | Boolean | False | ✗ | Flag to instantiate points at animated mesh instead of rest mesh on initialization. |

#### Activation Remap
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Activation Remap** | Ramp Attribute |  | ✗ | Curve to remap the activation values. |

### Debug attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Debug**       | Boolean      | False                 | ✗ | Enable or Disable the debug functionalities in the viewport for the AdnSimshape deformer. |
| **Feature**     | Enumerator   | Collision Constraints | ✗ | A list of debuggable features for this deformer.<ul><li>Collision Constraints: Draw *Collision Constraints* connections from the simulated mesh to the collider mesh.</li><li>Muscle Fibers: Draw *Muscle Fibers* on the simulated mesh.</li><ul> |
| **Width Scale** | Float        | 3.0                   | ✗ | Modifies the width of all lines. |
| **Color**       | Color Picker |                       | ✗ | Selects the line color from a color wheel. Its saturation can be modified using the slider. |
| **Fiber Scale** | Float        | 3.0                   | ✗ | The scale can be modified to set a custom fiber length. |

### Connectable attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Anim Mesh**                  | Mesh   |          | ✗ | Animated mesh on which to apply the simulation. |
| **Attenuation Matrix**         | Matrix | Identity | ✗ | Transformation matrix to drive the attenuation. |
| **Collision Mesh**             | Mesh   |          | ✗ | Collision mesh used to drive the the collision logic. |
| **Collision Mesh Matrix**      | Matrix | Identity | ✗ | Collision matrix used to drive the collision logic. |
| **Collision Rest Mesh**        | Mesh   |          | ✗ | Collision rest mesh used to drive the initialization of the collision logic. |
| **Collision Rest Mesh Matrix** | Matrix | Identity | ✗ | Collision rest matrix at rest used for initializing. |
| **Deform Mesh**                | Mesh   |          | ✗ | Deform mesh used to estimate the muscle patches activation. |
| **Rest Mesh**                  | Mesh   |          | ✗ | Rest mesh used for initializing the system and to compute the activations against the deform mesh. |

## Attribute Editor Template

<figure markdown>
  ![simshape editor first part](images/attribute_editor_part_one_simshape.png) 
  <figcaption><b>Figure 2:</b> AdnSimshape Attribute Editor</figcaption>
</figure>

<figure markdown>
  ![simshape editor second part](images/attribute_editor_part_two_simshape.png)
  <figcaption><b>Figure 3:</b> AdnSimshape Attribute Editor (Advanced Settings)</figcaption>
</figure>

<figure markdown>
![skin editor debug menu](images/attribute_editor_simshape_debug.png)
<figcaption><b>Figure 4:</b> AdnSimshape Attribute Editor (Debug menu)</figcaption>
</figure>

## Debugger

To better visualize deformer constraints and attributes in the Maya viewport there is the option to enable the debugger, found in the dropdown menu labeled *Debug* in the Attribute Editor.

To enable the debugger the *Debug* checkbox must be marked. To select the specific feature to visualize, choose it from the list provided in *Features*.

### Debug features

The features that can be visualized with the debugger in the AdnSimshape deformer are:

 - **Collision Constraints**: For each vertex, a line will be drawn from the mesh to the closest point of a collider.
    - The debug lines will only be displayed in case collisions are enabled and colliders have been set up.
 - **Muscle Fibers**: For each vertex, a line will be drawn showing the direction of the muscle fibers.
    - The debug lines will only be displayed in case muscle activations have been enabled with an Adonis Muscle Patches file.

Enabling the debugger and selecting one of these constraints will draw lines from the influenced vertices in the simulated mesh to their corresponding reference vertices. 

<figure markdown>
![skin editor debug menu](images/simshape_debug.png)
<figcaption><b>Figure 5:</b> AdnSimshape Muscle Fibers and Collision Constraints debugging</figcaption>
</figure>

# Advanced

## Muscle Activations
AdnSimshape can emulate the behaviour of facial muscles by computing the muscle activation directly on the vertices of the skin geometry. The activation of the vertices is an advanced and optional feature that can work in two modes: from **muscle patches data** or from **plug values**.

<figure markdown>
  ![Activation modes from attribute editor](images/activation_modes.png)
  <figcaption><b>Figure 6:</b> Activation Modes switch exposed in the Attribute Editor</figcaption>
</figure>

!!! abstract "Activations Modes"
    === "Muscle Patches"
        The data in the Adonis Muscle Patches (AMP) file in combination with the deformation status of the Deform Mesh are used to calculate the amount of activation at each vertex. The AMP file is the result of a Machine Learning process and can be generated following [generate muscle patches section](#generate-muscle-patches).

        <h5>Requirements</h5>

        - **Adonis Muscle Patches**.
        - **Deform mesh**.

    === "Plug Values"
        The plug values from the Activation List array attribute are used to drive the level of activation at each vertex.

        > [!NOTE]
        > - The values must be provided in the range 0 to 1, where 0.0 is no activation and 1.0 is maximum activation.
        > - The values outside of the valid range will be clamped.

    === "No Activation"
        Activations are not computed. This option is selected by default.

### Generate Muscle Patches

##### Requirements

  - **Neutral mesh**: Rest mesh with a neutral facial expression.
  - **Target meshes**: Set of deformed meshes representing facial expressions.
    - The number of vertices in the neutral and the target meshes must match with the number of vertices of the simulated mesh that will be used for the simulation.


The AMP file is generated from the Learn Muscle Patches tool:

<figure style="float: right; width: 40%; padding-left: 5px;">
  <img src="images/simshape_ml_window.png" caption="Learn Muscle Patches UI"> 
  <figcaption><b>Figure 7:</b> Learn Muscle Patches UI</figcaption>
</figure>

1. Open the **Learn Muscle Patches UI**. Using the shelf button ![Learn Muscle Patches icon](images/adn_learn_muscle_patches.png) or go to the Edit Simshape submenu from the AdonisFX menu and press *Learn Muscle Patches UI*.
2. Add the neutral mesh.
3. Add the target meshes.
4. Select the vertices on the neutral mesh that will be involved in the training for the muscle patches generation. If *Add Selected* is pressed with no selection, the tool will display a pop-up and inform that all vertices will be used for the learning process. This button has to necessarily be pressed to enable the execution of the learning process.
5. Browse or specify the destination AMP file.
6. Configure custom settings for the learning algorithm.
7. Press **Execute**.

<br>
<figure style="width: 25%;" markdown>
  ![Simshape draw muscle patches example](images/nassim_draw_muscle_patches.png)
  <figcaption><b>Figure 8:</b> Example of muscle patches generated with the Learn Muscle Patches UI</figcaption>
</figure>

Additional custom settings for the learning algorithm:

| Name | Type | Default | Description |
| :--- | :--- | :------ | :---------- |
| **Limit Iterations**         | Boolean | False | If enabled, the *Number of Iterations* will be taken into consideration. |
| **Number of Iterations**     | Integer | 20    | Maximum number of iterations allowed in the training process. The higher this value is, the more accurate the muscle patches estimation will be and the longer the execution will take. This parameter is ignored if *Limit Iterations* attribute is disabled. In that case, the training process will run until it achieves the most accurate solution. Has a range of \[1, 1e<sup>6</sup>\] |
| **Number of Muscle Patches** | Integer | 79    | Maximum number of muscle patches expected in the results. Has a range of \[1, 1e<sup>6</sup>\] |
| **Draw Muscle Patches**      | Boolean | True  | If enabled, the vertices of the neutral mesh will be colored according to the muscle patches resulting from the training. |

### Debug Activations

AdnSimshape integrates a debug mode to visualize the activations during the simulation. If this mode is enabled, then AdnSimshape will display a map of vertex colors from black to red on the simulation mesh where the black color is mapped to no activation and the red color is mapped to maximum activation.

<figure style="width: 30%" markdown>
  ![Learn Muscle Patches UI window](images/nassim_debug.png)
  <figcaption><b>Figure 9:</b> Example of AdnSimshape running in Debug mode</figcaption>
</figure>


In order to toggle and untoggle the debug mode, follow these steps:

1. Stop the simulation.
2. Move to pre-roll time or start time.
3. Press ![Simshape debug icon](images/adn_simshape_debugger.png) or go to the Edit Simshape submenu from the AdonisFX menu and press *Activations Debugger*.

## Colliders

AdnSimshape supports an internal collider that has to be bound to the rig and combined into a single object in order to mimic the internal structures. Colliders can represent structures like the skull or the teeth.

### Add Collider

1. Select the collider object.
2. Select the mesh with the AdnSimshape deformer.
3. Press the AdonisFX Shelf > *Add Collider* Shelf Button ![Add collider icon](images/adn_add_collider.png) or go to the Edit Simshape submenu from the AdonisFX menu and press *Add Collider*. 

> [!NOTE]
> - Avoid intersections between the collider and the rest/simulated mesh.
> - Colliders with high Level Of Detail will affect the simulation performance.

### Remove Collider

1. Select the collider object.
2. Select the mesh with the AdnSimshape deformer.
3. Press the AdonisFX Shelf > *Remove Collider* Shelf Button ![Remove collider icon](images/adn_remove_collider.png) or go to the Edit Simshape submenu from the AdonisFX menu and press *Remove Collider*.

### Add Rest Collider

The use of rest collider is recommended when the pre-roll simulation is not computed and the [initialization to the animated mesh](#initialization-settings) is enabled. In order to allow the solver to build consistent collision data in those cases, it is necessary to provide both the [rest mesh](#requirements) and the rest collider.

1. Select the rest collider object.
2. Select the mesh with the AdnSimshape deformer.
3. Go to the Edit Simshape submenu from the AdonisFX menu and press *Add Rest Collider*.

> [!NOTE]
> - Avoid intersections between the collider and the rest mesh.
> - Colliders with high Level Of Detail will affect the simulation performance.
> - Collider meshes must have the same number of vertices although it can be different from the number of vertices of the rest, deformed, animated and simulated meshes.

### Remove Rest Collider

1. Select the rest collider object.
2. Select the mesh with the AdnSimshape deformer.
3. Go to the Edit Simshape submenu from the AdonisFX menu and press *Remove Rest Collider*.

### Collider Configuration

Apart from [*Compute Collisions*](#collision-settings), [*Keep Orientation*](#collision-settings) and [*Max Sliding Distance*](#collision-settings) parameters, it is possible to tweak the collision computation by painting the following attributes, also explained in more detail in the [*Paintable Weights*](#paintable-weights) section:

 - [**Slide Collision Constraints**](#paintable-weights) to scale the distance vertex-to-collider at rest.
 - [**Collision Threshold Multiplier**](#paintable-weights) to represent which areas the collisions should be computed against the collider.

<figure style="width:45%" markdown> 
  ![Slide collision paint example](images/slide_collision_paint_example.png) 
  <figcaption><b>Figure 10:</b> Slide Collision Constraints painted values.</figcaption> 
</figure>

<figure style="width:45%;" markdown> 
  ![Collision threshold paint example](images/collision_threshold_paint_example.png) 
  <figcaption><b>Figure 11:</b> Collision Threshold Multiplier painted values to 0.2 for the whole mesh.</figcaption> 
</figure>
