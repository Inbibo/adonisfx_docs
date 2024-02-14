# How To Use

**Simshape** is a Maya deformer to get facial simulation in the animation rig of an asset. Given a facial expression, the deformer is able to compute the activation of the vertices in order to emulate the changes in the rigidity of the skin. As result, the dynamics of the simulated skin mimic the behaviour of internal muscles contracting.

During the simulation, the solver reduces the inertias of the vertices with higher values of activation, while it computes standard simulation in the vertices that are not activated. One of the key features of Simshape is the ability to extract muscle information directly from the neutral geometry and the set of deformed geometries with the facial expressions using Machine Learning techniques.

## Requirements

The Simshape deformer requires the following inputs to be provided:

  - <b class="mesh_color"> Rest Mesh (R) </b> with no deformation or animation. (optional) 
  - <b class="mesh_color"> Deform Mesh (D)</b> with deformation driven by the facial expressions. (optional)
  - <b class="mesh_color"> Anim Mesh (A)</b> with deformation driven by the facial expressions and animation result of to the binding to the animation rig. (optional)
  - <b class="mesh_color"> Simulation Mesh (S)</b> to apply the deformer onto. This mesh can be the animation mesh or a separate mesh with no deformation nor animation.

!!! Notes
    - All input geometries must have the same number of vertices.
    - If <b class="mesh_color">R</b> is not provided, the system will use the initial state of <b class="mesh_color">S</b> as the rest mesh.
    - If <b class="mesh_color">D</b> is not provided, the simulation will not produce activations.
    - If <b class="mesh_color">A</b> is not provided, the system will use the input mesh to the deformer (<b class="mesh_color">S</b>) as animated mesh.
## Create Simshape

  1. Select the meshes in the following order:
    ``` mermaid
    graph LR
      A["Rest Mesh\n <i style='font-size:12px;'>Optional</i>"]:::opt --> B;
      B["Simulation Mesh\n <i style='font-size:12px;'>Required</i>"];
      classDef opt fill:#413E63,stroke-dasharray: 5 5
    ```
  2. Press the ![Simshape button](images/adn_simshape_sim.png) in the AdonisFX shelf or press Simshape in AdonisFX menu.
  3. Simshape is ready to simulate with default settings. Check [this page](#attributes) to customize the configuration.

In order to add or remove any of those optional meshes, a set of menu items are exposed in AdonisFX menu > Edit Simshape. In that submenu, we can find the options to manage each mesh type as we present in the Figure 1.

<figure style="width:45%" markdown>
  ![Edit Simshape submenu](images/simshape_menu.png)
  <figcaption>Figure 1: Edit Simshape submenu.</figcaption>
</figure>

# Attributes

[^1]:
  Soft range: higher values can be used.

<style>
table th:first-of-type {
    width: 20%;
}
table th:nth-of-type(2) {
    width: 10%;
}
table th:nth-of-type(3) {
    width: 15%;
}
table th:nth-of-type(4) {
    width: 10%;
}
table th:nth-of-type(5) {
    width: 45%;
}
</style>

#### Solver Attributes
| Attribute            | Type  | Value     | Range/Options     | Description                  |
| :------------        | :---  | :----     | :------------     | :--------------------------- |
| Enable               | Bool  | True      | \[False, True\]   | Flag to enable or disable the deformer computation. |
| Iterations           | Long  | 3         | \[1, 10\] [^1]    | Number of iterations that the solver will execute per simulation step. |
| Material             | Enum  | Leather   | <ul><li>Fat</li><li>Muscle</li><li>Rubber</li><li>Tendon</li><li>Leather</li><li>Wood</li><li>Concrete</li></ul> | Solver stiffness. The materials are listed from lowest to highest stiffness |
| Stiffness Multiplier | Float | 1.0       | \[0.0, 2.0\] [^1] | Multiplier factor to scale up or down the material stiffness. |

#### Muscles Activation Settings
| Attribute                | Type   | Value           | Range/Options   | Description                  |
| :------------            | :---   | :----           | :------------   | :--------------------------- |
| Activation Mode          | Enum   | No Activation   | <ul><li>Muscle Patches</li><li>Plug Values</li><li>No Activation</li></ul> | Mode to drive the muscle activations:<ul><li> **Muscle Patches** (Disabled by default): An Adonis Muscle Patches file (.amp) has to be provided to enable this option.</li><li> **Plug Values**. (Disabled by default): The attribute values **ActivationList.Activation** should be populated to enable this option. The activation data will be read from the plug values. </li><li> **No Activation**. No activation is read. </li></ul> |
| Muscle Patches File      | String |                 || Path to the Adonis Muscle Patches file (.amp). |
| Activation Smoothing     | Long   | 1               | \[1, 20\] [^1]  | Number of iterations for the activation smoothing algorithm. |
| Bidirectional Activation | Bool   | False           | \[False, True\] | Flag to enable muscle activations in the positive and negative directions of the muscle patches fibers. |
| Activation List          | Float  | 0.0             || Array attribute to connect the activation values for each vertex. Used in Plug Values activation mode |

#### Time Attributes
| Attribute          | Type | Value         | Range/Options | Description                  |
| :---------------   | :--- | :----         | :----------   | :--------- |
| Preroll Start Time | Time | Current frame || Frame to start the preroll. |
| Start Time         | Time | Current frame || Frame to end the preroll and start the simulation. |
| Current Time       | Time | Current frame || Current playback frame. |

#### Scale Attributes
| Attribute   | Type  | Value | Range/Options          | Description                  |
| :---------- | :---  | :---- | :------------          | :--------------------------- |
| Time Scale  | Float | 1.0   | \[1e^-3^, 10.0\] [^1]  | Scale to control the time step relative to the Dependency Graph time. |
| Space Scale | Float | 1.0   | \[1e^-3^, 100.0\] [^1] | Scale to control the space relative to the scene units. |

#### Gravity
| Attribute         | Type   | Value            | Range/Options       | Description               |
| :------------     | :---   | :----            | :------------       | :------------------------ |
| Gravity           | Float  | 0.0              | \[0.0, 100.0\] [^1] | Magnitude of the gravity. |
| Gravity Direction | Float3 | (0.0, -1.0, 0.0) |                     | Direction of the gravity. |

### Advanced Settings

#### Stiffness Settings
| Attribute            | Type  | Value    | Range/Options   | Description                  |
| :------------        | :---  | :----    | :------------   | :--------------------------- |
| Use Custom Stiffness | Bool  | False    | \[False, True\] | Flag that enables the custom stiffness. If we use custom stiffness, **Material** and **Stiffness Multiplier** will be disabled and **Stiffness** will be used instead. |
| Stiffness            | Float | 10^5^    | \[0.0, inf\]    | Custom stiffness value. |

#### Dynamic Properties
| Attribute              | Type  | Value | Range/Options     | Description                  |
| :------------          | :---  | :---- | :------------     | :--------------------------- |
| Global Damping         | Float | 0.75  | \[0.0, 1.0\] [^1] | Global damping introduced to the system. |
| Inertia Damping        | Float | 0.0   | \[0.0, 1.0\]      | Damping affecting only the inertias in the system. |
| Rest Length Multiplier | Float | 1.0   | \[0.0, 2.0\] [^1] | Scaling factor of the edge rest lengths. |
| Stretching Resistance  | Float | 1.0   | \[0.0, 1.0\]      | Force to correct the edge lengths if the current length is greater than the rest length. This attribute is paintable. | 
| Compression Resistance | Float | 0.0   | \[0.0, 1.0\]      | Force to correct the edge lengths if the current length is smaller than the rest length. This attribute is paintable. |

#### Collision Settings
| Attribute            | Type  | Value | Range/Options      | Description                  |
| :------------        | :---  | :---- | :------------      | :--------------------------- |
| Compute Collisions   | Bool  | True  | \[False, True\]    | Flag to enable collisions correction. |
| Keep Orientation     | Bool  | True  | \[False, True\]    | Preserves the initial orientation of the vertices relative to the collider when handling collisions.|
| Max Sliding Distance | Float | 1.0   | \[0.0, 10.0\] [^1] | Maximum distance the simulated vertex is allowed to slide on top of the collider in world units. |

#### Attraction Settings
| Attribute             | Type | Value     | Range/Options  | Description           |
| :------------         | :--- | :----     | :------------  | :----------           |
| Attraction Remap Mode | Enum | Cube Root | <ul><li>Linear</li><li>Logarithmic</li><li>Square Root</li><li>Cube Root</li></ul> | Remap mode used to compute the definitive attraction values. |

#### Initialization Settings
| Attribute               | Type | Value | Range/Options   | Description           |
| :------------           | :--- | :---- | :------------   | :----------           |
| Animatable Rest Mesh    | Bool | False | \[False, True\] | Flag that enables reading animated rest mesh data. |
| Initialize to Anim Mesh | Bool | False | \[False, True\] | Flag to instantiate points at animated mesh instead of rest mesh on initialization. |

#### Activation Remap
| Attribute        | Type           | Value  | Range/Options  | Description           |
| :------------    | :---           | :----  | :------------  | :----------           |
| Activation Remap | Ramp Attribute | Linear || Curve to remap the activation values. |

#### Additional Properties
| Attribute     | Type  | Value | Range/Options  | Description                  |
| :------------ | :---  | :---- | :------------  | :--------------------------- |
| Attract Force | Float | 1.0   | \[0.0, 1.0\]   | Attibute to control the amount of influence of the animated mesh. The higher the value is, the more influence and the less dynamics will appear. This attribute is paintable. |

## Attribute Editor Template

<figure markdown>
  ![simshape editor first part](images/attribute_editor_part_one_simshape.png) 
  <figcaption>Figure 1: Simshape Attribute Editor</figcaption>
</figure>

<figure markdown>
  ![simshape editor second part](images/attribute_editor_part_two_simshape.png)
  <figcaption>Figure 2: Simshape Attribute Editor (Advanced Settings)</figcaption>
</figure>

# Advanced

## Muscle Activations
Simshape can emulate the behaviour of facial muscles by computing the muscle activation directly on the vertices of the skin geometry. The activation of the vertices is an advanced and optional feature that can work in two modes: from muscle patches data or from plug values.

<figure markdown>
  ![Activation modes from attribute editor](images/activation_modes.png)
  <figcaption>Figure 1: Activation Modes switch exposed in the Attribute Editor</figcaption>
</figure>

!!! abstract "Activations Modes"
    === "Muscle Patches"
        The data in the Adonis Muscle Patches (AMP) file in combination with the deformation status of the Deform Mesh are used to calculate the amount of activation at each vertex. The AMP file is the result of a Machine Learning process and can be generated following [this section](#generate-muscle-patches).

        <h5>Requirements</h5>

        - **Adonis Muscle Patches**.
        - **Deform mesh**.

    === "Plug Values"
        The plug values from the Activation List array attribute are used to drive the level of activation at each vertex.

        !!! Note
            - The values must be provided in the range 0 to 1, where 0.0 is no activation and 1.0 is maximum activation.
            - The values outside of the valid range will be clamped.

    === "No Activation"
        Activations are not computed. This option is selected by default.

### Generate Muscle Patches
##### Requirements

  - **Neutral mesh**: rest mesh with a neutral facial expression.
  - **Target meshes**: set of deformed meshes representing facial expresions.
  - The number of vertices in the neutral and the target meshes must match with the number of vertices of the Simulated mesh that will be used for the simulation.


The AMP file is generated from the Learn Muscle Patches tool:

<figure style="float: right; width: 40%; padding-left: 5px;">
  <img src="images/simshape_ml_window.png" caption="Learn Muscle Patches UI"> 
  <figcaption>Figure 3: Learn Muscle Patches UI</figcaption>
</figure>

1. Open the **Learn Muscle Patches UI**. Using the shelf button ![Learn Muscle Patches icon](images/adn_simshape_learn.png) or go to the Edit Simshape submenu from the AdonisFX menu and press **Learn Muscle Patches UI**.
2. Add the neutral mesh.
3. Add the target meshes.
4. Select the vertices on the neutral mesh that will be involved in the training for the muscle patches generation.
5. Browse or specify the destination AMP file.
6. Configure custom settings for the learning algorithm.
7. Press **Execute**.

<br>
<figure style="width: 25%;" markdown>
  ![Simshape draw muscle patches example](images/nassim_draw_muscle_patches.png)
  <figcaption>Figure 2: Example of muscle patches generated with the Learn Muscle Patches UI</figcaption>
</figure>

Additional custom settings for the learning algorithm:

| Settings                   | Type  | Value     |  Range/Options | Description                  |
| :------------              | :---  | :----     |  :------------ | :--------------------------- |
| Limit Iterations           | Bool  | False     |                | If enabled, the "Number of iterations" will be taken into consideration. |
| Number of Iterations       | Int   | 20        | \[1, 1e^6^\]   | Maximum number of iterations allowed in the training process. The higher this value is, the more accurate the muscle patches estimation will be and the longer the execution will take. This parameter is ignored if "Limit iterations" attribute is disabled. In that case, the training process will run until it achieves the most accurate solution. |
| Number of Muscle Patches   | Int   | 79        | \[1, 1e^6^\]   | Maximum number of muscle patches expected in the results. |
| Draw Muscle Patches        | Bool  | True      |                | If enabled, the vertices of the neutral mesh will be colored according to the muscle patches resulting from the training. |

### Debug Activations
Simshape integrates a debug mode to visualize the activations during the simulation. If this mode is enabled, then Simshape will display a map of vertex colors from black to red on the simulation mesh where the black color is mapped to no activation and the red color is mapped to maximum activation.

<figure style="width: 30%" markdown>
  ![Learn Muscle Patches UI window](images/nassim_debug.png)
  <figcaption>Figure 4: Example of Simshape running in Debug mode</figcaption>
</figure>


In order to toggle and untoggle the debug mode, follow these steps:

1. Stop the simulation.
2. Move to pre-roll frame or start frame.
3. Press ![Simshape debug icon](images/adn_simshape_debug.png) or go to the Edit Simshape submenu from the AdonisFX menu and press **Activations Debugger**.

## Colliders

Simshape supports an internal collider that has to be bound to the rig and combined into a single object in order to mimic the internal structures like the skull or the teeth.

### Add Collider

1. Select the collider object.
2. Select the mesh with the Simshape deformer.
3. Press the AdonisFX Shelf > Add Collider Shelf Button ![Add collider icon](images/adn_add_collider.png) or go to the Edit Simshape submenu from the AdonisFX menu and press **Add Collider**. 

!!! Note
    - Avoid intersections between the collider and the rest/simulated mesh.
    - Colliders with high Level Of Detail will affect the simulation performance.

### Remove Collider

1. Select the collider object.
2. Select the mesh with the Simshape deformer.
3. Press the AdonisFX Shelf > Remove Collider Shelf Button ![Remove collider icon](images/adn_remove_collider.png) or go to the Edit Simshape submenu from the AdonisFX menu and press **Remove Collider**.

### Add Rest Collider

The use of rest collider is recommended when the preroll simulation is not computed and the [initialization to the animated mesh](#initialization-settings) is enabled. In order to allow the solver to build consistent collision data in those cases, we should provide both the [rest mesh](#requirements) and the rest collider.

1. Select the rest collider object.
2. Select the mesh with the Simshape deformer.
3. Go to the Edit Simshape submenu from the AdonisFX menu and press **Add Rest Collider**.

!!! Note
    - Avoid intersections between the collider and the rest mesh.
    - Colliders with high Level Of Detail will affect the simulation performance.

### Remove Rest Collider

1. Select the rest collider object.
2. Select the mesh with the Simshape deformer.
3. Go to the Edit Simshape submenu from the AdonisFX menu and press **Remove Rest Collider**.

### Collider Configuration

Apart from [*Compute Collisions*](#collision-settings), [*Keep Orientation*](#collision-settings) and [*Max Sliding Distance*](#collision-settings) parameters, it is possible to tweak the collision computation by painting the following attributes:

| Paintable Attribute            | Type  | Value | Range        | Description |
| :------------                  | :---  | :---- | :----        | :---------- |
| Slide Collision Constraints    | Float | 0.0   | \[0.0, 1.0\] | Represents for which areas collisions should be computed against the collider.  <br><br> A value of 0.0 does not apply correction at all, while a value of 1.0 does apply the correction to fix intersections. |
| Collision Threshold Multiplier | Float | 1.0   | \[0.0, 1.0\] | Factor to scale the distance vertex-to-collider at rest. It is used to modulate the minimum distance to the collider allowed for each vertex. |

<figure style="width:45%" markdown> 
  ![Slide collision paint example](images/slide_collision_paint_example.png) 
  <figcaption>Figure 5: Slide Collision Constraints painted values.</figcaption> 
</figure>

<figure style="width:45%;" markdown> 
  ![Collision threshold paint example](images/collision_threshold_paint_example.png) 
  <figcaption>Figure 6: Collision Threshold Multiplier painted values to 0.2 for the whole mesh.</figcaption> 
</figure>