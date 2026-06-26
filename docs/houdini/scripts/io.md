# Input & Output

In `adn.scripts.houdini.adnio` module, a set of Python functions are provided to allow users to:

- Gather the Adonis nodes setup from the scene.
- Clear the scene by removing all Adonis nodes and dependent nodes.
- Build the Adonis setup in the scene from a dictionary.
- Import Adonis setup from a JSON file.
- Export Adonis setup into a JSON file.

In the following sections, we provide a brief overview of how to use the utilities provided in this Python module.

## Gather Data

To gather all Adonis nodes from the scene and store their setup into a dictionary, run this command in Python:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.houdini import adnio
data = adnio.gather_from_scene(enabled_features, context)
</code></pre>

The argument `enabled_features` is optional and it is a dictionary where keys are feature names (i.e. Adonis solver nodes and other util nodes) and values are flags to determine if a feature has to be gathered or bypassed. If this is not provided, all features will be gathered.

The second argument `context` is optional and it is the path to the geometry node where the Adonis rig should be gathered from (i.e. */obj/geo1*). If the argument is not provided, the rig will be gathered from the first found active geometry node in */obj*.

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
}
context = "/obj/geo1"</code></pre>

## Clear All

To clear all Adonis related nodes from the scene, run the command below in Python. This is useful for when Adonis data has to be imported onto a clean version of the rig.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.houdini import adnio
adnio.clear_scene()
</code></pre>

> [!NOTE]
> In addition to removing all Adonis nodes, the clear utility will also remove the dependent nodes created between the null nodes *ADN_IN_* and *ADN_OUT_*, including them.

## Build

To build an Adonis setup in Python, it is required to provide the setup information in dictionary format. This dictionary data can be the value returned by the function `gather_from_scene` or the result of loading a JSON file exported previously with the function `export_data`. The code to build the Adonis setup is:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.houdini import adnio
adnio.build_from_data(data, enabled_features, context)
</code></pre>

The first argument `data` is required and it is the dictionary with the mapped data. The second argument `enabled_features` is optional and corresponds to a dictionary where keys are feature names and values are flags to determine if a feature has to be built or bypassed (same format used for gathering data). The third argument `context` is optional and corresponds to the path to the geometry node where the Adonis rig should be built. If it is not provided, the rig will be built into the first found active geometry node in */obj*.

## Import

To import an Adonis setup from a JSON file, run the command below:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.houdini import adnio
file_path = "path/to/source/file.json"
adnio.import_data(file_path, enabled_features)
</code></pre>

The first argument `file_path` is required and it is the full path to the JSON file containing a valid Adonis setup definition. The second argument `enabled_features` is optional and corresponds to a dictionary where keys are feature names and values are flags to determine if a feature has to be imported or bypassed (same format used for gathering data).

> [!NOTE]
> The rig will be imported into the first found geometry node with the visibility flag on. For that reason it is advisable to have one single geometry node in the */obj* context or at least only one active.

Find more information about the use of the import feature in the [Import](../tools/importer) page.

## Export

To export the Adonis setup in the current scene into a file, run this command:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.houdini import adnio
file_path = "path/to/destination/file.json"
adnio.export_data(file_path, enabled_features)
</code></pre>

The first argument `file_path` is required and it is the full path to the JSON file to export the data into. The second argument `enabled_features` is optional and corresponds to a dictionary where keys are feature names and values are flags to determine if a feature has to be exported or bypassed (same format used for gathering data).

> [!NOTE]
> The rig will be exported from the first found geometry node with the visibility flag on. For that reason it is advisable to have one single geometry node in the */obj* context or at least only one active.

Find more information about the use of the export feature in the [Export](../tools/exporter) page.

## Limitations

- The `adnio` scripts do not support subnetworks inside of the Geometry context. This means that all Adonis SOP nodes (and any other SOP nodes containing geometry required by the Adonis rig) must exist at the same level within the Geometry context (e.g., */obj/geo1*).
- Only one active geometry node (with the visibility/display flag enabled) in the */obj* context is allowed for the `adnio` scripts to work.
- Nodes used to drive attachment to transform or slide on segment constraints (e.g. null, joint or rivet nodes) must live in the */obj* context.
- KineFX joint transforms are not supported.
