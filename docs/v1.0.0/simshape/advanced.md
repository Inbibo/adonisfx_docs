# Advanced

## Muscle Activations
Simshape can emulate the behaviour of facial muscles by computing the muscle activation directly on the vertices of the skin geometry. The activation of the vertices is an advanced and optional feature that can work in two modes: from muscle patches data or from plug values.

<figure markdown>
  ![Activation modes from attribute editor](../img/activation_modes.png)
  <figcaption>Figure 1: Activation Modes switch exposed in the Attribute Editor</figcaption>
</figure>

!!! abstract "Activations Modes"
    === "Muscle Patches"
        The data in the Adonis Muscle Patches (AMP) file in combination with the deformation status of the Deform Mesh are used to calculate the amount of activation at each vertex. The AMP file is the result of a Machine Learning process and can be generated following [this section](advanced.md#generate-muscle-patches).

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
  <img src="../img/simshape_ml_window.png" caption="Learn Muscle Patches UI"> 
  <figcaption>Figure 3: Learn Muscle Patches UI</figcaption>
</figure>

1. Open the **Learn Muscle Patches UI**. Using the shelf button ![Learn Muscle Patches icon](../img/adn_simshape_learn.png) or go to the Edit Simshape submenu from the AdonisFX menu and press **Learn Muscle Patches UI**.
2. Add the neutral mesh.
3. Add the target meshes.
4. Select the vertices on the neutral mesh that will be involved in the training for the muscle patches generation.
5. Browse or specify the destination AMP file.
6. Configure custom settings for the learning algorithm.
7. Press **Execute**.

<br>
<figure style="width: 25%;" markdown>
  ![Simshape draw muscle patches example](../img/nassim_draw_muscle_patches.png)
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
  ![Learn Muscle Patches UI window](../img/nassim_debug.png)
  <figcaption>Figure 4: Example of Simshape running in Debug mode</figcaption>
</figure>


In order to toggle and untoggle the debug mode, follow these steps:

1. Stop the simulation.
2. Move to pre-roll frame or start frame.
3. Press ![Simshape debug icon](../img/adn_simshape_debug.png) or go to the Edit Simshape submenu from the AdonisFX menu and press **Activations Debugger**.

## Colliders

Simshape supports an internal collider that has to be bound to the rig and combined into a single object in order to mimic the internal structures like the skull or the teeth.

### Add Collider

1. Select the collider object.
2. Select the mesh with the Simshape deformer.
3. Press the AdonisFX Shelf > Add Collider Shelf Button ![Add collider icon](../img/adn_add_collider.png) or go to the Edit Simshape submenu from the AdonisFX menu and press **Add Collider**. 

!!! Note
    - Avoid intersections between the collider and the rest/simulated mesh.
    - Colliders with high Level Of Detail will affect the simulation performance.

### Remove Collider

1. Select the collider object.
2. Select the mesh with the Simshape deformer.
3. Press the AdonisFX Shelf > Remove Collider Shelf Button ![Remove collider icon](../img/adn_remove_collider.png) or go to the Edit Simshape submenu from the AdonisFX menu and press **Remove Collider**.

### Add Rest Collider

The use of rest collider is recommended when the preroll simulation is not computed and the [initialization to the animated mesh](attributes.md#initialization-settings) is enabled. In order to allow the solver to build consistent collision data in those cases, we should provide both the [rest mesh](how_to_use.md#requirements) and the rest collider.

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

Apart from [*Compute Collisions*](attributes.md#collision-settings), [*Keep Orientation*](attributes.md#collision-settings) and [*Max Sliding Distance*](attributes.md#collision-settings) parameters, it is possible to tweak the collision computation by painting the following attributes:

| Paintable Attribute            | Type  | Value | Range        | Description |
| :------------                  | :---  | :---- | :----        | :---------- |
| Slide Collision Constraints    | Float | 0.0   | \[0.0, 1.0\] | Represents for which areas collisions should be computed against the collider.  <br><br> A value of 0.0 does not apply correction at all, while a value of 1.0 does apply the correction to fix intersections. |
| Collision Threshold Multiplier | Float | 1.0   | \[0.0, 1.0\] | Factor to scale the distance vertex-to-collider at rest. It is used to modulate the minimum distance to the collider allowed for each vertex. |

<figure style="width:45%" markdown> 
  ![Slide collision paint example](../img/slide_collision_paint_example.png) 
  <figcaption>Figure 5: Slide Collision Constraints painted values.</figcaption> 
</figure>

<figure style="width:45%;" markdown> 
  ![Collision threshold paint example](../img/collision_threshold_paint_example.png) 
  <figcaption>Figure 6: Collision Threshold Multiplier painted values to 0.2 for the whole mesh.</figcaption> 
</figure>