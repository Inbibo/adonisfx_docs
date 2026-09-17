# Input & Output

In `adn.scripts.maya.adnio` module, a set of Python functions are provided to allow users to:

- Gather the Adonis nodes setup from the scene.
- Clear the scene by removing all Adonis nodes.
- Build the Adonis setup in the scene from a dictionary.
- Import Adonis setup from a JSON file.
- Export Adonis setup into a JSON file.

In the following sections, we provide a brief overview of how to use the utilities provided in this Python module.

## Gather Data

To gather all Adonis nodes from the scene and store their setup into a dictionary, run this command in Python:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import adnio
data = adnio.gather_from_scene(
    enabled_features=enabled_features,
    include_geometry_data=True,
    selection_only=False,
)
</code></pre>

The optional arguments are:

- `enabled_features`: Dictionary whose keys are feature names and whose Boolean values determine whether each feature is gathered. All features are gathered when this argument is `None`.
- `include_geometry_data`: Includes point positions and UV data for paintable solver meshes. This data enables Position and UV map import, but can significantly increase the JSON file size. Defaults to `True`.
- `selection_only`: Limits gathering to the Adonis nodes represented by the current selection and their enabled upstream dependencies. Defaults to `False`.

The feature keys are defined by the DCC-independent `IOFeaturesData` class in `adn.utils.constants`:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.utils.constants import IOFeaturesData
enabled_features = {
    IOFeaturesData.SENSOR: True,
    IOFeaturesData.ACTIVATION: True,
    IOFeaturesData.MUSCLE: True,
    IOFeaturesData.GLUE: True,
    IOFeaturesData.SKIN: True,
    IOFeaturesData.FAT: True,
    IOFeaturesData.RELAX: True,
    IOFeaturesData.SKIN_MERGE: True,
    IOFeaturesData.SIMSHAPE: True,
    IOFeaturesData.EDGE_EVALUATOR: True,
    IOFeaturesData.REMAP: True,
    IOFeaturesData.PUSH: True,
    IOFeaturesData.MUSH: True,
    IOFeaturesData.ML_DEFORMER: True,
    IOFeaturesData.SMART_TISSUE: True,
    IOFeaturesData.CLOSEST_FIT: True,
    IOFeaturesData.RIGID_WRAP: True,
    IOFeaturesData.SOFT_WRAP: True,
    IOFeaturesData.RADIAL_WRAP: True,
}</code></pre>

When `selection_only` is `True`, an empty selection preserves the full-scene behavior. A non-empty selection gathers the resolved Adonis nodes and their enabled upstream dependencies, while geometry data used for map transfer remains limited to the original selection. The function returns `None` if a selection-only export contains no enabled exportable Adonis nodes; otherwise, it returns the gathered rig dictionary.

## Clear All

To clear all Adonis related nodes from the scene, run the command below in Python. This is useful for when Adonis data has to be imported onto a clean version of the rig.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import adnio
adnio.clear_scene()
</code></pre>

## Build

To build an Adonis setup in Python, it is required to provide the setup information in dictionary format. This dictionary data can be the value returned by the function `gather_from_scene` or the result of loading a JSON file exported previously with the function `export_data`. The code to build the Adonis setup is:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import adnio
from adn.utils.constants import IOData
from adn.utils.maps import MapIOMode

enabled_data = {
    IOData.SETTINGS: True,
    IOData.MAPS: True,
}
success = adnio.build_from_data(
    data,
    enabled_features=enabled_features,
    map_io_mode=MapIOMode.COMPONENT_ID,
    enabled_data=enabled_data,
)
</code></pre>

The arguments are:

- `data`: Required dictionary containing the mapped Adonis rig data.
- `enabled_features`: Optional feature flags using the same format as `gather_from_scene`. All features are built when this argument is `None`.
- `map_io_mode`: Map correspondence mode from `MapIOMode`. Defaults to `MapIOMode.COMPONENT_ID`.
- `enabled_data`: Optional flags keyed by `IOData.SETTINGS` and `IOData.MAPS`. Settings include node parameters, input connections, and all other non-paintable attributes; maps include only paintable maps. Missing flags default to `True`, and `None` imports both categories. If both categories are disabled, the function returns `False` without changing the scene.

The function returns `True` when the data is successfully built and `False` otherwise. If a node selected through `enabled_features` does not exist, it is created for either enabled data category. When a paintable map depends on a target that is not connected, the function logs a warning and skips that map.

The `MapIOMode` class is available from `adn.utils.maps` and exposes the following modes:

- `MapIOMode.COMPONENT_ID` (`0`): Uses the existing component IDs. This is the default.
- `MapIOMode.POSITION` (`1`): Uses the closest exported point positions and falls back to Component ID when compatible.
- `MapIOMode.UV` (`2`): Uses UV correspondence first, then Position, and finally Component ID when compatible.

`MapIOMode.ALL` contains all three supported values. Position and UV modes require the input data to contain geometry data gathered with `include_geometry_data=True`; see *Export Geometry Data* in this [section](../tools/exporter#ui).

## Import

To import an Adonis setup from a JSON file, run the command below:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import adnio
from adn.utils.constants import IOData
from adn.utils.maps import MapIOMode

file_path = "path/to/source/file.json"
enabled_data = {
    IOData.SETTINGS: True,
    IOData.MAPS: True,
}
success = adnio.import_data(
    file_path,
    enabled_features=enabled_features,
    map_io_mode=MapIOMode.COMPONENT_ID,
    enabled_data=enabled_data,
)
</code></pre>

The required `file_path` argument is the full path to a JSON file containing a valid Adonis setup. The optional `enabled_features`, `map_io_mode`, and `enabled_data` arguments behave as described for `build_from_data`. The function returns `True` when the data is successfully imported and `False` otherwise.

Find more information about the import behavior in the [Import](../tools/importer) page.

## Export

To export the Adonis setup in the current scene into a file, run this command:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import adnio
file_path = "path/to/destination/file.json"
success = adnio.export_data(
    file_path,
    enabled_features=enabled_features,
    include_geometry_data=True,
    selection_only=False,
)
</code></pre>

The required `file_path` argument is the full destination path for the JSON file. The optional `enabled_features`, `include_geometry_data`, and `selection_only` arguments behave as described for `gather_from_scene`. The function returns `True` when the data is successfully exported and `False` otherwise.

Find more information about the export behavior in the [Export](../tools/exporter) page.

## Limitations

- The use of Maya namespaces is not supported by the `adnio` scripts.
