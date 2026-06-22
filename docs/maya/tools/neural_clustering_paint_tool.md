# Neural Clustering Paint Tool

> [!IMPORTANT]
> An Adonis ML license is required to use this feature.

The **Neural Clustering Paint Tool** is used to paint neural clusters on a static mesh. These clusters provide additional locality information for the machine learning training process, helping the model better isolate local deformations and activations.

The tool exports the painted cluster data to a `.json` file. This file is later used during neural training and can be provided when launching the training process with the [AdnNeuralTrainingTool](../tools/neural_training_tool).

Neural clusters define local regions on the training mesh. These regions help the training process understand which parts of the mesh should be treated as related deformation areas, which can improve the posability of the trained rig.

The number and size of the clusters should be adjusted depending on the amount of extracted training data available. Larger datasets can support more granular clusters, while smaller datasets should usually use broader cluster regions.

If multiple clusters overlap, the cluster values can be normalized. Normalizing overlapping clusters helps keep the cluster data consistent and can improve the resulting training quality.

> [!TIP]
> The **Neural Clustering Paint Tool** is intended to be used as an optional data preparation step for machine learning workflows. It provides neural clustering information that can complement the data extracted through the **AdnMLDataExtraction TOP HDA**.

## UI

<figure style="width:50%;" markdown>
  ![Adonis Data Extraction Tool](../images/data_extraction_tool.png)
  <figcaption><b>Figure 1</b>: Adonis Data Extraction UI.</figcaption>
</figure>

The Data Extraction Tool (see Figure 1) provides an intuitive interface to configure the data extraction process according to specific requirements. Below is a breakdown of the available UI elements:

### Skin information

- **Rest skin scene path**: Specifies the Maya scene path to the rest skin. The *Get From Selection* button allows users to select the rest skin geometry in the scene and automatically populate the field with its path.

- **Sim skin scene path**: Specifies the Maya scene path to the simulated skin. The *Get From Selection* button allows users to select the simulated skin geometry in the scene and automatically populate the field with its path.

- **SkinCluster name**: Specifies the name of the skinCluster node associated with the animated skin. This will be used to extract the animation joint data. The animated skin must have the same topology as the rest and simulated skins.

### Joints

- **Load Joint List From File**: This button allows users to load the list of joint paths from a `joints.json` file from previous data extractions. This can be useful for ensuring consistency across multiple data extractions or when working with complex rigs.

- **Set Joint List From Selection**: This button allows users to select the joints in the Maya scene that will be included in the data extraction. The selected joint paths will be displayed in the *Joint List* field.

- **Joint List**: This field displays the list of joint paths that will be included in the data extraction. Users can manually edit this list or use the buttons mentioned above to populate it.

- **Select Joints in Scene**: This button allows users to select the joints in the Maya scene based on the paths specified in the *Joint List* field. This can be useful for quickly verifying that the correct joints are included in the data extraction.

### Muscles

- **Extract muscle activation data**: When enabled, the data extraction process will include muscle activation data, which can be used for training AdonisML models that predict dynamic material behavior for AdnSmartTissue.

- **Muscle group scene path**: If muscle activation data extraction is enabled, this field specifies the Maya scene path to the muscle group. The muscle group should contain the AdnMuscle and AdnRibbonMuscle nodes that will be included in the data extraction. The *Get From Selection* button allows users to select the muscle group in the scene and automatically populate the field with its path.

### Frame Settings

- **Record frame windows**: When enabled, the data extraction process will record the input and output data for the specified frame windows. If disabled, the data extraction will record data for the full animation playback range.

- **Frame windows**: This field specifies the frame windows for recording the data. Frame windows must be defined as separate frame ranges (for example: `[[1, 5], [220, 600], [1023, 1500]]`) where each range indicates the start and end frames for recording.

- **Skip frames**: This field specifies the number of frames to skip between each recorded frame. For example, if set to `2`, the data extraction will record every third frame. This can be useful for reducing the redundancy of poses in the data recorded, especially for slow animations.

- **Stabilization frames**: This field specifies the number of times a frame should be stabilized before being recorded. This parameter damps the motion inertia in the recorded poses. Higher values make each of the recorded poses lose more dynamics and converge toward a static silhouette. Well stabilized data is required for good ML deformation training. Faster animations usually require more stabilization frames. Typical suggested values for normal animation speeds are between `5` and `10`. Increasing this value will increase the export time.

### Output

- **Export folder path**: Specifies the folder path where the extracted data will be saved. Use the **Browse** button to select the desired export folder.

- **Force overwrite**: When enabled, the data extraction process will overwrite any existing files in the export folder with the same names as the newly extracted data. Use this option with caution to avoid unintentional loss of previous data.

## Requirements

To use the Neural Clustering Paint Tool, the following inputs must be provided:

- *Geometry*: Static mesh where neural clusters will be painted.
- *Joints*: ML joints used to associate each cluster with the relevant joint data.

The static mesh connected to *Geometry* must match the topology of the mesh that will be used for training. This means both meshes must have matching point counts and matching point order so the exported cluster weights correspond to the expected training mesh data.

The ML joints connected to *Joints* should represent the joint set used as machine learning input data. In many cases, this can be the animated joints. The joint geometry must contain a valid *name* point attribute, because joint selections are resolved using the joint names.

The joint entries assigned to each cluster must use explicit `@name=...` selections, for example `@name=R_Scapula`. Do not use wildcards or broad patterns.

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

    Use *Clear* to clear all of the current multiparameter entries.

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

    For more information about Houdini's Attribute Paint node, refer to the [Houdini Attribute Paint documentation](https://www.sidefx.com/docs/houdini/nodes/sop/attribpaint).

<figure style="width:90%; margin-left:5%" markdown>
  ![AdnNeuralClusteringPaintTool painted cluster](../images/neural_clustering_paint_tool_cluster.png)
  <figcaption><b>Figure 4</b>: Example of a painted neural cluster on a training mesh. Painted values closer to <code>1</code> are displayed toward red and represent higher influence, while values closer to <code>0</code> are displayed toward blue and represent lower influence. Smooth transitions between these values define the cluster falloff.</figcaption>
</figure>

10. Mirror the cluster if needed.

    Press *Mirror* to create or update a mirrored neural cluster entry by copying joints and weights across the X axis.

    Mirroring is useful when one side of the character has already been configured and the opposite side should use corresponding joints and mirrored weight values.

    The entry name and joints are mirrored using the selected *Mirror by* mode and the *Left* and *Right* naming tokens. The same naming convention is used for both the cluster entry name and the joint names.

    The painted weights are mirrored across the X axis of the geometry. This means the tool transfers the painted region from one side of the mesh to the corresponding opposite-side region.

    If the selected convention does not match, the tool will try to fall back to a simple `L`/`R` token swap. A warning will be logged in case of failure.

    If the mirrored entry already exists, the tool asks for confirmation. Depending on which data is already present, it may update only the mirrored joints, the weights, or both.

11. Normalize overlapping clusters if needed.

    Enable *Normalize Clusters* when cluster regions overlap and the painted values should be normalized.

    Normalizing clusters adjusts the weights between `0` and `1` across all clusters. This helps keep overlapping cluster data consistent and can improve the quality of the model predictions at the interface between clusters.

12. Export the cluster map.

    Use *Export JSON* to export the current neural cluster entry data to a `.json` file.

    Export requires a valid *Mesh*, valid cluster *Name* values, and valid *Joints* fields.

    The exported `.json` file can then be used during neural training with the [AdnNeuralTrainingTool](../tools/neural_training_tool).

## Result

After configuring and painting clusters with the AdnNeuralClusteringPaintTool, the painted neural clustering data can be exported to a `.json` file.

This `.json` file is used during neural training and can be provided when launching the training process with the [AdnNeuralTrainingTool](../tools/neural_training_tool).

The generated clusters describe regions of locality on the mesh. These regions help the training process isolate local deformation and activation behavior, which can improve the posability of the trained rig.

## Recommendations

- Use broader cluster regions when the extracted training dataset contains fewer samples.
- Use more granular clusters only when enough training samples are available to support them.
- Paint clusters around regions where local deformation behavior should be isolated.
- Normalize clusters when painted regions overlap.
- Use clear cluster names that describe the body region or deformation area they represent.
- Associate each cluster with the joints that are expected to cause deformations in that region. For example, for a humanoid character, movements of the elbow, or forearm, joint are expected to cause bulging of the bicep and tricep muscles, therefore the cluster should cover that skin region.
- Keep mesh and cluster names aligned with other DCCs when the cluster data needs to be reused across applications.
- Use explicit `@name=...` joint selections and avoid wildcards.
- Remember that painted values closer to `1` represent higher influence and are displayed toward red, while values closer to `0` represent lower influence and are displayed toward blue.
