# AdnPush

AdnPush is a Houdini SOP designed to push a surface along the direction of its normals. This deformation can be applied outwards (i.e., the surface bulges and gains volume) or inwards (i.e., the surface shrinks and loses volume). Optional collider meshes can limit the displacement and prevent the pushed surface from passing through surrounding geometry. This deformer is useful for refining meshes by increasing or decreasing their volume, as well as for modeling purposes. For example, a common use case is generating internal fascia geometry from skin geometry. Check [this section](../simple_setup#adnpush) to see a simple setup of this.

## How To Use

The AdnPush SOP is easy to create and configure in Houdini. It requires a mesh connected to its input and can optionally receive one or more collider meshes through its parameter template. Following the example mentioned above, the input mesh would be the skin geometry at rest, while muscles or other internal tissues could be used as colliders.

1. Go to the geometry context of the rig containing the geometry to apply the deformer to.
2. Press TAB and navigate to the submenu Adonis > Deformers to find the AdnPush ![Push button](../../images/adn_push.png){style="width:4%"} SOP type.
3. Create it and connect the geometry to the input.
4. Modify the value of the *Push Length* parameter to see the result of the push deformation.
5. To add colliders, open the *Colliders* section, add entries to the *Colliders* multiparm, and set the object path of each collider mesh.
6. Enable *Use Colliders* to process the collider list. Check the [Attributes](push#attributes) section to customize the configuration.

When colliders are enabled, each point is displaced until its push path hits a collider. If the path hits multiple colliders, the displacement stops at the closest hit.

## Attributes

### Settings
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Push Length** | Float | 0.0 | ✓ | Length of the push to apply. A positive value pushes the vertices along the direction of the normal, while a negative value pushes them in the opposite direction. Has a range of \[-1.0, 1.0\]. The upper and lower limits are soft; higher or lower values can be used. |

### Colliders
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Use Colliders** | Boolean | False | ✓ | Toggles the use of colliders. If enabled, the provided colliders are processed; if disabled, they are ignored. |
| **Overlap Tolerance** | Float | 0.0 | ✓ | Distance used to offset the input geometry along its vertex normals before raycasting against the colliders. Use a small value to tolerate initial overlaps with the colliders; 0.0 otherwise. Has a range of \[0.0, 1.0\]. The upper limit is soft; higher values can be used. |

### Collider Targets
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Colliders** | List | 0 | ✗ | List of geometry targets used to stop the push displacement. Each entry provides the object path of one collider mesh. |
| **Collider World Mesh** | String |  | ✓ | Object path of the collider geometry. The path can be absolute or relative to the AdnPush SOP. |

### Deformer Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Envelope** | Float | 1.0 | ✓ | Specifies the deformation scale factor. Has a range of \[0.0, 1.0\]. The upper and lower limits are soft, values can be set in a range of \[-2.0, 2.0\] |

### Extra Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Update On Topology Change** | Boolean | True | ✓ | Toggles the update of the internal geometry connectivity data only when the topology of the input mesh changes. If enabled, the SOP runs faster by reusing that information at each frame. If disabled, the SOP runs slower because that information needs to be recomputed at each frame. |

### Maps

| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Push Multiplier Attribute** | float | 1.0 | ✗  | Specifies the name of the per-point attribute to read the multiplier of the push length. The expected attribute name is `adnPushMultiplier`. The expected range of the per-point values is \[0.0, 1.0\].  |
| **Weights Attribute**         | float | 1.0 | ✗  | Specifies the name of the per-point attribute to read the weight of the deformation. The expected attribute name is `adnWeights`. The expected range of the per-component per-point values is \[0.0, 1.0\]. |

> [!NOTE]
> - All maps parameters are disabled in the Maps tab because the attribute names are fixed to drive specific functionalities of the solver.
> - Fixed point attribute names also ensure compatibility with the API.
> - To copy the map names of the disabled attributes for painting (using an attribute paint node) right click on the disabled map attribute parameter, press "Copy Parameter", select the attribute paint node and on the attribute name entry right click and press "Paste Values". This allows to easily copy the attribute name for painting.
> - The *Make Paintable* utility provided in the Adonis menu > Utils, can be used to create the attribpaint node and automatically populate the entries with the map names of the AdnPush SOP.
> - If a point attribute on the geostream does not match the naming convention exposed in the node, use an "Attribute Rename" node to rename the attribute to match the expected naming convention.

## Parameter Template

<figure markdown>
  ![push parameter template solver tab](../images/push_parameter_template_00.png)
  <figcaption><b>Figure 1</b>: AdnPush Parameter Template (Part 1): Solver.</figcaption>
</figure>

<figure markdown>
  ![push parameter template colliders tab](../images/push_parameter_template_01.png)
  <figcaption><b>Figure 2</b>: AdnPush Parameter Template (Part 2): Colliders.</figcaption>
</figure>

<figure markdown>
  ![push parameter template maps tab](../images/push_parameter_template_02.png)
  <figcaption><b>Figure 3</b>: AdnPush Parameter Template (Part 3): Maps.</figcaption>
</figure>

## Colliders

Manage collider meshes from the *Colliders* multiparm in the AdnPush parameter template:

- **Add colliders**:
    1. Increment the number of entries in the *Colliders* multiparm.
    2. Enter the object path of a collider mesh in the new entry. The path can be absolute or relative to the AdnPush SOP.
- **Remove colliders**:
    1. Locate the collider to remove in the *Colliders* multiparm.
    2. Remove it using the **X** button for that entry.
    3. Alternatively, click **Clear** to remove all colliders.

Adding colliders does not enable collision processing automatically. Enable *Use Colliders* to make AdnPush stop point displacement at the closest collider hit.

## Paintable Weights

To provide more control, the AdnPush SOP includes two paintable attributes.

| Name | Default | Description |
| :--- | :------ | :---------- |
| **Push Multiplier** | 1.0 | Weight used to multiply the global Push Length to determine the amount of adjustment applied at each vertex. |
| **Weights**         | 1.0 | Global weights map used to control the influence of the deformer at each vertex. |

<figure markdown>
  ![push paintable maps](../images/push_weights.png)
  <figcaption><b>Figure 4</b>: Example of Push Multiplier map of AdnPush SOP applied to the skin layer of a biped to obtain the fascia geometry. Left: front view. Right: back view.</figcaption>
</figure>

> [!NOTE]
> To tweak the point attributes of an AdnPush SOP, an `attribpaint` is needed. To ease the creation and initial configuration of this node, select the AdnPush SOP and click on Adonis > Utils > Make Paintable. This utility will create an `attribcreate` node to define the required point attributes and assign their default values followed by an `attribpaint` node to allow these attributes to be modified. Both nodes are automatically named and properly connected to the AdnPush node.
