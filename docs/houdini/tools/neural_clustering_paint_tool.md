# AdnNeuralClusteringPaintTool

The **AdnNeuralClusteringPaintTool** is used to paint neural clusters on a static mesh. These clusters provide additional locality information for the machine learning training process, helping the model better isolate local deformations and activations.

The tool exports the painted cluster data to a `.json` file. This file is later used during neural training and can be provided when launching the training process with the [AdnNeuralTrainingTool](../tools/neural_training_tool).

Neural clusters define local regions on the training mesh. These regions help the training process understand which parts of the mesh should be treated as related deformation areas, which can improve the poseability of the trained rig.

The number and size of the clusters should be adjusted depending on the amount of extracted training data available. Larger datasets can support more granular clusters, while smaller datasets should usually use broader cluster regions.

If multiple clusters overlap, the cluster values can be normalized. Normalizing overlapping clusters helps keep the cluster data consistent and can improve the resulting training quality.

> [!NOTE]
> The **AdnNeuralClusteringPaintTool** is intended to be used as an optional data preparation step for machine learning workflows. It provides neural clustering information that can complement the data extracted through the [AdnMLDataExtraction TOP HDA](../tools/data_extraction_tool).

## Requirements

To use the AdnNeuralClusteringPaintTool, the following inputs must be provided:

- *Geometry*: Static mesh where neural clusters will be painted.
- *Joints*: ML joints used to associate each cluster with the relevant joint data.

The static mesh connected to *Geometry* must match the topology of the mesh that will be used for training. This means both meshes must have matching point counts and matching point order so the exported cluster weights correspond to the expected training mesh data.

The ML joints connected to *Joints* should represent the joint set used as machine learning input data. In many cases, this can be the animated joints. The joint geometry must contain a valid *name* point attribute, because joint selections are resolved using the joint names.

The joint entries assigned to each cluster must use explicit `@name=...` selections, for example `@name=R_Scapula`. Do not use wildcards or broad patterns.

> [!NOTE]
> The painted mesh must match the topology of the mesh that will be trained. If the topology does not match, the exported cluster weights may not correspond to the expected training mesh data.

## How To Use

1. Create an **AdnNeuralClusteringPaintTool** node.

<figure style="width:90%; margin-left:5%" markdown>
  ![AdnNeuralClusteringPaintTool parameter template](../images/neural_clustering_paint_tool_parameter_template.png)
  <figcaption><b>Figure 1</b>: AdnNeuralClusteringPaintTool parameter template.</figcaption>
</figure>

2. Connect the geometry and joints.

    Connect the static mesh to paint into the *Geometry* input.

    Connect the ML joints into the *Joints* input. These can be the animated joints, as long as they represent the joint set that will be used for the machine learning input data.

    The ML joint geometry must contain a valid *name* point attribute.

<figure style="width:90%; margin-left:5%" markdown>
  ![AdnNeuralClusteringPaintTool node setup](../images/neural_clustering_paint_tool_node.png)
  <figcaption><b>Figure 2</b>: Example node setup for the AdnNeuralClusteringPaintTool, with the static mesh connected to the <i>Geometry</i> input and the ML joints connected to the <i>Joints</i> input.</figcaption>
</figure>

3. Set the *Mesh* parameter.

    Use *Mesh* to define the source mesh name stored in the exported `.json` file.

    The *Mesh* parameter is only used as a naming field for export, import, and cross-DCC compatibility. It does not define the actual geometry being painted. The geometry being painted comes from the *Geometry* input.

    For cross-DCC compatibility, the *Mesh* value should match the equivalent mesh name used in other DCCs. Avoid relying on full Houdini paths when possible.

    The mesh name can be assigned manually by typing it, or by using *Pick Mesh From Selection* to fill the *Mesh* parameter from the currently selected Houdini node name. This only updates the *Mesh* text field and does not change node connections or geometry.

    Use *Clear Mesh* to clear the *Mesh* parameter. This does not remove clusters, weights, imported data, or painted attributes.

4. Import an existing cluster map if needed.

    Use *Import JSON* to import neural cluster entry data from a `.json` file. This replaces the current entries in the tool with the entries from the file.

    Importing restores the cluster entries, the cluster names, the joint associations, and the painted weights stored for each cluster. The imported weights are stored per cluster and the corresponding attributes are stashed internally on the node.

    Use *Clear Imported Data* to clear imported and mirrored weight values from the internal stash. Cluster entries and painted weights remain unchanged.

    *Clear Imported Data* is also used to clear mirrored data because the same internal stash is used for import and mirror operations.

5. Configure the mirror naming convention.

    Use *Mirror by* to define how the left and right text is matched in cluster names and joint names.

    Use *Prefix* when the left and right text appears at the start of the name, for example `L_forearm` and `R_forearm`.

    Use *Suffix* when the left and right text appears at the end of the name, for example `forearm_L` and `forearm_R`.

    Use *Token* when the left and right text can appear anywhere in the name, for example `front_L_forearm` and `front_R_forearm`.

    Use *Left* and *Right* to define the side-specific naming convention. For example, use `L_` and `R_` for prefix names, `_L` and `_R` for suffix names, or `_L_` and `_R_` for token-based names.

    The mirror naming convention is used for both the cluster entry name and the joint names.

6. Create or select a cluster entry.

    Use *Entry* to select the cluster entry to edit. Each entry represents a neural cluster definition.

    Use the plus and minus icons next to *Entry* to add or remove cluster entries.

    Use *Clear* to clear the current multiparameter entry.

7. Name the cluster entry.

    Use *Name* to assign a valid neural cluster name to the selected cluster entry.

    The cluster name becomes the Houdini point attribute used for painting, import, export, mirroring, and normalization. Use a valid attribute name with no spaces or special characters.

8. Assign joints to the cluster entry.

    Use *Joints* to define the joint selection for the selected cluster entry.

    The joint selection should be created using the cogwheel picker next to the *Joints* parameter, as shown in Figure 3.

    The joint geometry must contain a valid *name* point attribute. The entries in *Joints* must follow the `@name=...` convention, for example `@name=R_Scapula`. Do not use wildcards or broad patterns, because the export process expects explicit joint name selections.

    When the clustering data is exported, these selections are resolved to full joint paths using separators.

    The selected joints help describe which rig controls are related to the painted cluster region.

<figure style="width:90%; margin-left:5%" markdown>
  ![AdnNeuralClusteringPaintTool joint selection](../images/neural_clustering_paint_tool_joint_selection.png)
  <figcaption><b>Figure 3</b>: Joint picker used to populate the <i>Joints</i> parameter for a cluster entry. The selected joints are written as explicit <code>@name=...</code> entries.</figcaption>
</figure>

9. Paint the cluster.

    Press *Paint Cluster* to make the selected cluster the active paint target and enter the paint workflow for its mask attribute.

    The paint workflow exposes the same painting parameters as Houdini's Attribute Paint node. These parameters control the brush behavior, stroke behavior, symmetry, and painted values.

    The painted values represent the influence of the current neural cluster over the mesh. High values define the main area of influence for the cluster, while lower values can be used to create a smooth falloff into nearby regions, as shown in Figure 4.

    To exit the paint viewer state, press **Esc** while the cursor is over the viewport.

<figure style="width:90%; margin-left:5%" markdown>
  ![AdnNeuralClusteringPaintTool painted cluster](../images/neural_clustering_paint_tool_cluster.png)
  <figcaption><b>Figure 4</b>: Example of a painted neural cluster on a training mesh. Painted values closer to <code>1</code> are displayed toward red and represent higher influence, while values closer to <code>0</code> are displayed toward blue and represent lower influence. Smooth transitions between these values define the cluster falloff.</figcaption>
</figure>

10. Mirror the cluster if needed.

    Press *Mirror* to create or update a mirrored neural cluster entry by copying joints and weights across the X axis.

    Mirroring is useful when one side of the character has already been configured and the opposite side should use corresponding joints and mirrored weight values.

    The entry name and joints are mirrored using the selected *Mirror by* mode and the *Left* and *Right* naming tokens. The same naming convention is used for both the cluster entry name and the joint names.

    The painted weights are mirrored across the X axis of the geometry. This means the tool transfers the painted region from one side of the mesh to the corresponding opposite-side region.

    If the selected convention does not match, the tool may fall back to a simple `L`/`R` token swap.

    If the mirrored entry already exists, the tool asks for confirmation. Depending on which data is already present, it may mirror only the joints, only the weights, or both.

11. Normalize overlapping clusters if needed.

    Enable *Normalize Clusters* when cluster regions overlap and the painted values should be normalized.

    Normalizing clusters adjusts the weights between `0` and `1` across all clusters. This helps keep overlapping cluster data consistent and can improve the quality of the resulting training data.

12. Export the cluster map.

    Use *Export JSON* to export the current neural cluster entry data to a `.json` file.

    Export requires a valid *Mesh*, valid cluster *Name* values, and valid *Joints* fields.

    The exported `.json` file can then be used during neural training with the [AdnNeuralTrainingTool](../tools/neural_training_tool).

## Parameters

### Mesh

| Name | Type | Default | Description |
| :--- | :--- | :------ | :---------- |
| *Mesh* | String |  | Source mesh name stored in the exported `.json` file. This is only used as a naming field for export, import, and cross-DCC compatibility. It does not define the actual geometry being painted. |
| *Pick Mesh From Selection* | Button |  | Fills the *Mesh* parameter from the currently selected Houdini node name. This only updates the *Mesh* text field and does not change node connections or geometry. |
| *Clear Mesh* | Button |  | Clears the *Mesh* parameter. This does not remove clusters, weights, imported data, or painted attributes. |

### Import and Export

| Name | Type | Default | Description |
| :--- | :--- | :------ | :---------- |
| *Export JSON* | Button |  | Exports the current neural cluster entry data to a `.json` file. Requires a valid *Mesh*, valid cluster *Name* values, and valid *Joints* fields. |
| *Import JSON* | Button |  | Imports neural cluster entry data from a `.json` file. This replaces the current entries in the tool with the entries from the file and stashes the imported cluster attributes internally on the node. |
| *Clear Imported Data* | Button |  | Clears imported and mirrored weight values from the internal stash. Cluster entries and painted weights remain unchanged. |

### Mirror

| Name | Type | Default | Description |
| :--- | :--- | :------ | :---------- |
| *Mirror by* | Menu | Prefix | Defines how the left and right text is matched in cluster names and joint names. Use *Prefix* when the text is at the start, *Suffix* when it is at the end, or *Token* when it can appear anywhere in the name. |
| *Left* | String | L_ | Left-side naming convention used for mirrored cluster names and joints. For example, use `L_` for prefix, `_L` for suffix, or `_L_` for token. |
| *Right* | String | R_ | Right-side naming convention used for mirrored cluster names and joints. For example, use `R_` for prefix, `_R` for suffix, or `_R_` for token. |

### Cluster Entry

| Name | Type | Default | Description |
| :--- | :--- | :------ | :---------- |
| *Entry* | Integer | 1 | Current cluster entry being edited. Use the plus and minus icons to add or remove entries, and use *Clear* to clear the current multiparameter entry. |
| *Name* | String | Entry1 | Neural cluster name. This becomes the Houdini point attribute used for painting, import, export, mirroring, and normalization. Use a valid attribute name with no spaces or special characters. |
| *Joints* | String |  | Explicit joint selection for the current cluster entry, stored as Houdini group patterns using the `@name=...` convention. The joint geometry must contain a valid *name* point attribute. Do not use wildcards or broad patterns. On export, these selections are resolved to full joint paths using separators. |
| *Paint Cluster* | Button |  | Makes this cluster the active paint target and enters the paint workflow for its mask attribute. |
| *Mirror* | Button |  | Creates or updates a mirrored neural cluster entry by copying joints and weights across the X axis. The entry name and joints are mirrored using the selected *Mirror by* mode and the *Left* and *Right* naming tokens. If the selected convention does not match, the tool may fall back to a simple `L`/`R` token swap. |
| *Normalize Clusters* | Boolean | False | Normalizes the weights between `0` and `1` across all clusters. This helps keep overlapping cluster weights consistent. |

### Paint Settings

The *Paint Settings* section exposes the same painting parameters available in Houdini's Attribute Paint node. These parameters control the brush behavior, stroke behavior, symmetry, and paint values used while painting cluster regions.

For more information about these parameters, refer to the [Houdini Attribute Paint documentation](https://www.sidefx.com/docs/houdini/nodes/sop/attribpaint.html).

## Cluster JSON Overview

The exported JSON file stores the mesh name and the list of neural cluster entries.

At the top level, the file contains:

- `mesh`: Source mesh name used for painting, export, import, and cross-DCC compatibility.
- `entries`: List of neural cluster entries.

Each entry contains:

- `name`: Cluster entry name. This corresponds to the neural cluster attribute used by the tool.
- `joints`: Full joint paths associated with the cluster.
- `vertex_indices`: Stored vertex index data for the entry.
- `color_set`: Name of the color set used to store the painted values.
- `weights`: Painted cluster weight values, stored by mesh component index.

For example, a cluster file may contain entries such as `R_frontLeg`, `L_frontLeg`, `R_rearLeg`, `L_rearLeg`, and `C_tailSpineNeck`. Each entry stores the joints associated with that region and the painted weight values for the mesh.

> [!NOTE]
> The exported cluster data is intended to be reusable across DCCs. For this reason, the mesh name, cluster names, and joint naming conventions should be kept consistent with the equivalent setup in other DCCs.

## Result

After configuring and painting clusters with the AdnNeuralClusteringPaintTool, the painted neural clustering data can be exported to a `.json` file.

This `.json` file is used during neural training and can be provided when launching the training process with the [AdnNeuralTrainingTool](../tools/neural_training_tool).

The generated clusters describe regions of locality on the mesh. These regions help the training process isolate local deformation and activation behavior, which can improve the poseability of the trained rig.

## Recommendations

- Use broader cluster regions when the extracted training dataset contains fewer samples.
- Use more granular clusters only when enough training samples are available to support them.
- Paint clusters around regions where local deformation behavior should be isolated.
- Normalize clusters when painted regions overlap.
- Use clear cluster names that describe the body region or deformation area they represent.
- Associate each cluster with the joints that most directly affect the painted region.
- Keep mesh and cluster names aligned with other DCCs when the cluster data needs to be reused across applications.
- Use explicit `@name=...` joint selections and avoid wildcards.
- Remember that painted values closer to `1` represent higher influence and are displayed toward red, while values closer to `0` represent lower influence and are displayed toward blue.

## Limitations

- Neural clustering quality depends on the quality and amount of extracted training data.
- Very granular clusters may require a larger dataset to train reliably.
- Broad clusters may be more suitable for smaller datasets, but they provide less localized deformation separation.
- Overlapping clusters should usually be normalized to avoid inconsistent cluster values.
- The painted mesh connected to *Geometry* must match the topology of the mesh used for training.
- The ML joint geometry connected to *Joints* must contain a valid *name* point attribute.
- The *Joints* entries must use explicit `@name=...` selections and should not use wildcards.
