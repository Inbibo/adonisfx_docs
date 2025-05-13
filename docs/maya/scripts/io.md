# I/O

In `adn.scripts.maya.adnio` module, a set of useful python functions are provided to allow users to:

- Gather the AdonisFX nodes setup from the scene.
- Clear the scene by removing all AdonisFX nodes.
- Build the AdonisFX setup in the scene from a dictionary.
- Import AdonisFX setup from a JSON file.
- Export AdonisFX setup into a JSON file.

In the following sections, we provide a brief overview of how to use the utilities provided in this Python module.

## Gather data

To gather all AdonisFX nodes from the scene and store their setup into a dictionary, run this command in Python:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import adnio
adnio.gather_from_scene(enabled_features)
</code></pre>

The argument `enabled_features` is optional and it is a dictionary where keys are feature names (i.e. AdonisFX solver nodes and other util nodes) and values are flags to determine if a feature has to be gathered or bypassed. If this is not provided, all features will be gathered.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.utils.maya.constants import IOFeaturesData
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
    IOFeaturesData.REMAP: True
}</code></pre>


## Clear all

To clear all AdonisFX related nodes from the scene, run the command below in Python. This is useful for when AdonisFX data has to be imported onto a clean version of the rig.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import adnio
adnio.clear_scene()
</code></pre>

## Build

To build an AdonisFX setup in Python, it is required to provide the setup information in dictionary format. This dictionary data can be the value returned by the function `gather_from_scene` or the result of loading a JSON file exported perviously with the function `export_data`. The code to build the AdonisFX setup is:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import adnio
adnio.build_from_data(in_data, enabled_features)
</code></pre>

The first argument `in_data` is required and it is the dictionary with the mapped data. The second argument `enabled_features` is optional and corresponds to a dictionary where keys are feature names and values are flags to determine if a feature has to be built or bypassed (same format used for gathering data).

## Import

To import an AdonisFX setup from a JSON file, run the command below:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import adnio
adnio.import_data(file_path, enabled_features)
</code></pre>

The first argument `file_path` is required and it is the full path to the JSON file containing a valid AdonisFX setup definition. The second argument `enabled_features` is optional and corresponds to a dictionary where keys are feature names and values are flags to determine if a feature has to be imported or bypassed (same format used for gathering data).

Find more information about the use of the import feature in the [Import](tools/importer) page.

## Export

To export the AdonisFX setup in the current scene into a file, run this command:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import adnio
adnio.export_data(file_path, enabled_features=None)
</code></pre>

The first argument `file_path` is required and it is the full path to the JSON file to export the data into. The second argument `enabled_features` is optional and corresponds to a dictionary where keys are feature names and values are flags to determine if a feature has to be exported or bypassed (same format used for gathering data).

Find more information about the use of the export feature in the [Export](tools/exporter) page.
