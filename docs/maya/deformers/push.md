# AdnPush

AdnPush is a Maya deformer designed to push a surface along the direction of its normals. This deformation can be applied outwards (i.e., the surface bulges and gains volume) or inwards (i.e., the surface shrinks and loses volume). This deformer is useful for refining meshes by increasing or decreasing their volume, as well as for modeling purposes. For example, a common use case is generating internal fascia geometry from skin geometry. Check [this section](../simple_setup.md#AdnPush) to see a simple setup of this.

## How to use

The AdnPush deformer is easy to create and configure in Maya. It only requires a mesh to apply the node to. Following the example mentioned above, this mesh would be the skin geometry at rest.

1. Select the mesh on which to apply the deformer.
2. Press ![Push button](../images/adn_push.png){style="width:4%"} in the AdonisFX shelf or *Push* in the AdonisFX menu, under the Create Deformers section.
3. A message in the terminal will notify that AdnPush has been created properly.
4. Modify the value of the *Push Length* parameter to see the result of the push deformation. Check the [Attributes](push#attributes) section to customize their configuration.

## Attributes

### Settings
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Push Length** | Float | 0.0 | ✓ | Length of the push to apply. A positive value pushes the vertices along the direction of the normal, while a negative value pushes them in the opposite direction. Has a range of \[-1.0, 1.0\]. The upper and lower limits are soft; higher or lower values can be used. |

### Deformer Attributes
| Name | Type | Default | Animatable | Description |
| :--- | :--- | :------ | :--------- | :---------- |
| **Envelope** | Float | 1.0 | ✓ | Specifies the deformation scale factor. Has a range of \[0.0, 1.0\]. The upper and lower limits are soft, values can be set in a range of \[-2.0, 2.0\]|

## Attribute Editor Template

<figure markdown>
  ![push attribute editor](../images/push_attribute_editor.png)
  <figcaption><b>Figure 1</b>: AdnPush Attribute Editor.</figcaption>
</figure>

## Paintable Weights

To provide more control, the AdnPush deformer includes two paintable attributes. The Maya paint tool must be used to paint those parameters to ensure that the values satisfy the deformation needs.

| Name | Default | Description |
| :--- | :------ | :---------- |
| **Push Multiplier** | 1.0 | Weight used to multiply the global Push Length to determine the amount of adjustment applied at each vertex. |
| **Weights**         | 1.0 | Maya standard weights map used to control the influence of the deformer at each vertex. |

<figure markdown>
  ![push paintable maps](../images/push_weights.png)
  <figcaption><b>Figure 2</b>: Example of Push Multiplier map of AdnPush deformer applied to the skin layer of a biped to obtain the fascia geometry. Left: front view. Right: back view.</figcaption>
</figure>
