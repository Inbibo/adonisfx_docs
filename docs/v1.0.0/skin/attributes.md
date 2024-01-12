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
| Material             | Enum  | Leather   | <ul><li>Fat</li><li>Muscle</li><li>Rubber</li><li>Tendon</li><li>Leather</li><li>Wood</li><li>Concrete</li></ul> | Solver stiffness. The materials are listed from lowest to highest stiffness |
| Stiffness Multiplier | Float | 1.0       | \[0.0, 2.0\] [^1] | Multiplier factor to scale up or down the material stiffness. |

#### Time Attributes
| Attribute          | Type | Value         | Range/Options    | Description                  |
| :---------------   | :--- | :----         | :----------      | :--------- |
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
| Attribute            | Type  | Value    | Range/Options | Description                  |
| :------------        | :---  | :----    | :------------ | :--------------------------- |
| Use Custom Stiffness | Bool  | False    || Flag that enables the custom stiffness. If we use custom stiffness, **Material** and **Stiffness Multiplier** will be disabled and **Stiffness** will be used instead. |
| Stiffness            | Float | 10^5^    | \[0.0, inf\]  | Custom stiffness value. |

#### Dynamic Properties
| Attribute              | Type  | Value | Range/Options      | Description                  |
| :------------          | :---  | :---- | :------------      | :--------------------------- |
| Global Damping         | Float | 0.75  | \[0.0, 2.0\] [^1]  | Global damping introduced to the system. |
| Inertia Damping        | Float | 0.0   | \[0.0, 1.0\]       | Damping affecting only the inertias in the system. |
| Rest Length Multiplier | Float | 1.0   | \[0.0, 2.0\] [^1]  | Scaling factor of the edge rest lengths. |
| Stretching Resistance  | Float | 1.0   | \[0.0, 1.0\]       | Force to correct the edge lengths if the current length is greater than the rest length. This attribute is paintable. | 
| Compression Resistance | Float | 1.0   | \[0.0, 1.0\]       | Force to correct the edge lengths if the current length is smaller than the rest length. This attribute is paintable. |
| Max Sliding Distance   | Float | 0.0   | \[0.0, 10.0\] [^1] | Maximum distance along the reference mesh that one vertex can slide on. |

#### Additional Properties
| Attribute         | Type  | Value | Range/Options | Description                  |
| :------------     | :---  | :---- | :------------ | :--------------------------- |
| Hard constraints  | Float | 1.0   | \[0.0, 1.0\]  | Weight to modulate the correction applied to the vertices to keep them at a constant transformation, local to the closest point on the reference mesh at initialization. <br> This attribute is paintable and normalized together with *Slide Constraints* and *Soft Constraints*. |
| Slide Constraints | Float | 0.0   | \[0.0, 1.0\]  | Weight to modulate the correction applied to the vertices to keep them at a constant distance to the reference mesh sliding along the reference surface. <br> This attribute is paintable and normalized together with *Hard Constraints* and *Soft Constraints*. |
| Soft constraints  | Float | 0.0   | \[0.0, 1.0\]  | Weight to modulate the correction applied to the vertices to keep them at a constant distance to the closest point on the reference mesh at initialization. <br> This attribute is paintable and normalized together with *Slide Constraints* and *Hard Constraints*. |

## Attribute Editor Template

<figure markdown>
  ![skin editor first part](../img/attribute_editor_part_one_skin.png) 
  <figcaption>Figure 1: Skin Attribute Editor</figcaption>
</figure>

<figure markdown>
  ![skin editor second part](../img/attribute_editor_part_two_skin.png)
  <figcaption>Figure 2: Skin Attribute Editor (Advanced Settings)</figcaption>
</figure>
