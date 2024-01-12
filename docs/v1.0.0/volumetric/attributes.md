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
| Iterations           | Long  | 3         | \[1, 10\] [^1]    | Number of iterations that the solver will execute per simulation step. |
| Material             | Enum  | Leather   | <ul><li>Fat</li><li>Muscle</li><li>Rubber</li><li>Tendon</li><li>Leather</li><li>Wood</li><li>Concrete</li></ul> | Solver stiffness. The materials are listed from lowest to highest stiffness. |
| Stiffness Multiplier | Float | 1.0       | \[0.0, 2.0\] [^1] | Multiplier factor to scale up or down the material stiffness. |
| Activation           | Float | 0.0       | \[0.0, 1.0\]      | Current activation of the deformed volumetric muscle. The activation modifies the stiffness of the muscle depending on the fibers direction of the muscle. |
| Rest Activation      | Float | 0.0       | \[0.0, 1.0\]      | Rest activation of the deformed volumetric muscle. The rest activation modifies the stiffness of the muscle depending on the fibers direction of the muscle at rest. |
| Volume Preservation  | Float | 1.0       | \[0.0, 1.0\]      | Ratio of volume preservation during deformation of the muscle. A higher value indicated a higher muscle volume preservation during deformation. |
| Volume Ratio         | Float | 1.0       | \[0.0, 2.0\] [^1] | Ratio of volume preservation during deformation of the muscle. A higher value indicated a higher muscle volume preservation during deformation. |

#### Time Attributes
| Attribute          | Type | Value         | Range/Options    | Description                  |
| :---------------   | :--- | :----         | :----------       | :--------- |
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
| Use Custom Stiffness | Bool  | False    || Flag that enables the custom stiffness. If we use custom stiffness, **Material** and **Stiffness Multiplier** will be disabled and **Stiffness** will be used instead. |
| Stiffness            | Float | 10^5^    | \[0.0, inf\]    | Custom stiffness value. |

#### Dynamic Properties
| Attribute              | Type  | Value | Range/Options     | Description                  |
| :------------          | :---  | :---- | :------------     | :--------------------------- |
| Global Damping         | Float | 0.0   | \[0.0, 2.0\] [^1] | Global damping introduced to the system. |
| Inertia Damping        | Float | 0.0   | \[0.0, 1.0\]      | Damping affecting only the inertias in the system. |
| Rest Length Multiplier | Float | 1.0   | \[0.0, 2.0\] [^1] | Scaling factor of the edge rest lengths. |
| Stretching Resistance  | Float | 1.0   | \[0.0, 1.0\]      | Force to correct the edge lengths if the current length is greater than the rest length. This attribute is paintable. | 
| Compression Resistance | Float | 1.0   | \[0.0, 1.0\]      | Force to correct the edge lengths if the current length is smaller than the rest length. This attribute is paintable. |
| Hard Attachments       | Bool  | False | \[False, True\]   | If enabled, attachment constraints will force the vertices to stick to target transformation completely. |

#### Debug
| Attribute    | Type  | Value | Range/Options      | Description                  |
| :----------- | :---  | :---- | :------------      | :--------------------------- |
| Draw Fibers  | Bool  | False | \[False, True\]    | Draw the debug fibers in the viewport. |
| Fibers Scale | Float | 1.0   | \[0.0, 10.0\] [^1] | Scale the fibers drawn in the viewport to increase their size. |

## Attribute Editor Template

<figure markdown>
  ![Volumetric Muscle editor first part](../img/attribute_editor_part_one_volumetric.png) 
  <figcaption>Figure 1: Volumetric Muscle Attribute Editor</figcaption>
</figure>

<figure markdown>
  ![Volumetric Muscle editor second part](../img/attribute_editor_part_two_volumetric.png)
  <figcaption>Figure 2: Volumetric Muscle Attribute Editor (Advanced Settings)</figcaption>
</figure>
