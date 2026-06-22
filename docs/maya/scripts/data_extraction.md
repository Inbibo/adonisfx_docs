# Data Extraction

> [!IMPORTANT]
> An Adonis ML license is required to use this feature.

In the `adnml.scripts.maya.data_extraction` module, a Python function is provided to extract data for training AdonisML models from a processed Adonis simulation setup.

Data extraction gathers the input and output data used by the AdonisML training workflow. The extracted data is used to train ML models that can support AdnMLDeformer workflows and, when muscle paths are provided, AdnSmartTissue workflows.

The data extraction script allows users to:

- Extract joint transform input data from a Maya rig.
- Extract mesh displacement output data from a rest skin and a simulated skin.
- Optionally extract muscle activation data from Adonis muscle solvers.
- Record data over the full playback range or over specific frame windows.
- Skip frames to reduce redundant poses in the extracted dataset.
- Recook frames for stabilization before recording data.
- Export the resulting dataset files to a target directory.

The extraction script is the Python API equivalent of the workflow exposed through the [Data Extraction Tool](../tools/data_extraction_tool).

The extraction process writes the generated dataset into the target folder specified by `save_directory_path`. The main exported files are `inputs.csv`, `outputs.csv`, `joints.json`, and `extraction_config.json`.

## Requirements

To run data extraction, the following arguments must be provided:

- `rest_skin_path`: Path to the rest skin SOP node.
- `sim_skin_path`: Path to the processed simulated skin SOP node.
- `joint_names_list`: List of Houdini/KineFX joint names to extract.
- `skincluster_name`: Name of the skin cluster node connected to the animated skin.
- `save_directory_path`: Target folder where the extracted dataset will be saved.

The rest skin and simulated skin must have the same topology. They must have matching point counts and matching point order so the extraction process can compute displacement data correctly.

## Extract Data

To extract ML training data from Python, run this command in Maya Script Editor or from your batch script:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adnml.scripts.maya import data_extraction

data_extraction.extract(
    rest_skin_path="|hyena|Geometry|Body_lod200_GRP|restSkin_Geo",
    sim_skin_path="|hyena|adonisfx_GRP|skinRender_GRP|skinRender_Geo",
    joint_names_list=["|hyena|DeformationSystem|Root_M|L_Hip",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1|L_HipPart2",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1|L_HipPart2|L_Knee",
                      ...],
    skincluster_name="skinCluster128",
    save_directory_path="path/to/export/folder"
)
</code></pre>

The extraction process writes the dataset files to the folder specified by `save_directory_path`.

## Extract Data With Optional Settings

Additional extraction settings can be provided to control frame sampling, stabilization, muscle activation extraction, and overwrite behavior.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adnml.scripts.maya import data_extraction

data_extraction.extract(
    rest_skin_path="|hyena|Geometry|Body_lod200_GRP|restSkin_Geo",
    sim_skin_path="|hyena|adonisfx_GRP|skinRender_GRP|skinRender_Geo",
    joint_names_list=["|hyena|DeformationSystem|Root_M|L_Hip",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1|L_HipPart2",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1|L_HipPart2|L_Knee",
                      ...],
    skincluster_name="skinCluster128",
    save_directory_path="path/to/export/folder",
    muscles_paths="|hyena|adonisfx_GRP|muscles_GRP",
    skip_frames=2,
    stabilization_frames=5,
    frame_windows=[[970, 971], [1000, 1020]],
    force_overwrite=False
)
</code></pre>

The optional arguments are:

- `muscles_paths`: Muscle group path used to extract muscle activation data.
- `skip_frames`: Number of frames to skip between recorded poses. This helps reduce redundant pose data and extract more diverse samples.
- `stabilization_frames`: Number of times to recook a frame before recording displacement data. This parameter damps the motion inertia in the recorded poses.
- `frame_windows`: List of frame windows to record. If empty, the entire playback range is recorded.
- `force_overwrite`: If enabled, existing dataset files in the target folder can be overwritten.

## Frame Windows

By default, the extraction process uses the current Maya playback range.

To extract only specific parts of the animation, provide the `frame_windows` argument in the extraction call.

Each entry defines a frame range using the format `[start_frame, end_frame]`.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adnml.scripts.maya import data_extraction

data_extraction.extract(
    rest_skin_path="|hyena|Geometry|Body_lod200_GRP|restSkin_Geo",
    sim_skin_path="|hyena|adonisfx_GRP|skinRender_GRP|skinRender_Geo",
    joint_names_list=["|hyena|DeformationSystem|Root_M|L_Hip",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1|L_HipPart2",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1|L_HipPart2|L_Knee",
                      ...],
    skincluster_name="skinCluster128",
    save_directory_path="path/to/export/folder",
    frame_windows=[[1, 120], [220, 360], [500, 720]]
)
</code></pre>

Frame windows are useful when only specific animation ranges should contribute to the training dataset.

## Skip Frames

The `skip_frames` argument controls how many frames are skipped between recorded poses.

This can be used to reduce redundant pose data and extract more diverse samples.

Lower values are recommended for fast animations, while higher values can be used for slower animations. Typical suggested values for normal animation speeds are between `2` and `5`.

The skip frames will be computed from the start of each frame window, this ensures that the starting frame of each window is always recorded in the dataset.

## Stabilization Frames

The `stabilization_frames` argument controls how many times each recorded frame should be recooked before displacement data is computed and written.

This is used to stabilize the simulation dynamics before recording data. Higher values make each of the recorded poses lose more dynamics and converge toward a static silhouette. Well stabilized data is required for good ML deformation training.

Typical suggested values for normal animation speeds are between `5` and `10`. Faster animations may require more stabilization frames.

Increasing `stabilization_frames` will increase the total extraction time.

## Muscle Activation Data

To extract muscle activation data, provide the `muscles_paths` argument.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adnml.scripts.maya import data_extraction

data_extraction.extract(
    rest_skin_path="|hyena|Geometry|Body_lod200_GRP|restSkin_Geo",
    sim_skin_path="|hyena|adonisfx_GRP|skinRender_GRP|skinRender_Geo",
    joint_names_list=["|hyena|DeformationSystem|Root_M|L_Hip",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1|L_HipPart2",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1|L_HipPart2|L_Knee",
                      ...],
    skincluster_name="skinCluster128",
    save_directory_path="path/to/export/folder",
    muscles_paths="|hyena|adonisfx_GRP|muscles_GRP"
)
</code></pre>

When muscle paths are provided, the extracted data will support training the ML model on material properties prediction for AdnSmartTissue. If this input is not provided, the extracted data will support training models for AdnMLDeformer only.

## Force Overwrite

By default, the extraction process will not overwrite existing dataset files.

If `inputs.csv` or `outputs.csv` already exist in the target export folder, the extraction will raise an error unless `force_overwrite` is enabled.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adnml.scripts.maya import data_extraction

data_extraction.extract(
    rest_skin_path="|hyena|Geometry|Body_lod200_GRP|restSkin_Geo",
    sim_skin_path="|hyena|adonisfx_GRP|skinRender_GRP|skinRender_Geo",
    joint_names_list=["|hyena|DeformationSystem|Root_M|L_Hip",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1|L_HipPart2",
                      "|hyena|DeformationSystem|Root_M|L_Hip|L_HipPart1|L_HipPart2|L_Knee",
                      ...],
    skincluster_name="skinCluster128",
    save_directory_path="path/to/export/folder",
    force_overwrite=True
)
</code></pre>

> [!WARNING]
> Enabling `force_overwrite` will replace any existing extraction data in the target folder, use it with caution.

## Exported Files

After a successful extraction, the following files are written to the target export folder:

- `inputs.csv`: Input data containing the selected joint transforms.
- `outputs.csv`: Output data containing the extracted mesh displacement data and optional data required for AdnSmartTissue material properties prediction.
- `joints.json`: Joint hierarchy data exported in the same order used by `inputs.csv`.
- `extraction_config.json`: Configuration data describing the extraction settings used for the exported dataset.

The exported joint data uses Houdini/KineFX joint names internally. The `joints.json` file stores full hierarchy paths built from the KineFX primitive hierarchy, in the same order used for `inputs.csv`.

## Validation

The extraction script validates the provided data before extraction starts.

The script checks that:

- The rest skin path is valid.
- The simulation skin path is valid.
- The save directory path is valid.
- The rest skin and simulation skin are not the same object.
- The rest skin and simulation skin have matching topology.
- Every joint path exists and is valid.
- The skip frame value is a valid integer greater than or equal to `0`.
- The stabilization frame value is a valid integer greater than or equal to `0`.
- The frame windows are valid.
- Existing dataset files are not overwritten unless `force_overwrite` is enabled.

## Errors

The `extract` function may raise the following errors:

- `ValueError`: Raised when an input path, frame setting, geometry, or joint list is invalid.
- `FileExistsError`: Raised when dataset files already exist and `force_overwrite` is disabled.
- `InterruptedError`: Raised when the extraction process is interrupted by the user.
