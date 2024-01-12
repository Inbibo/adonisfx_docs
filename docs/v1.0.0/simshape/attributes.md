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
  ![simshape editor first part](../img/attribute_editor_part_one_simshape.png) 
  <figcaption>Figure 1: Simshape Attribute Editor</figcaption>
</figure>

<figure markdown>
  ![simshape editor second part](../img/attribute_editor_part_two_simshape.png)
  <figcaption>Figure 2: Simshape Attribute Editor (Advanced Settings)</figcaption>
</figure>
