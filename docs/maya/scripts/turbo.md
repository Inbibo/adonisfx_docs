# Turbo

The Turbo script is a Python script that automates the setup of an AdonisFX rig on a clean asset. It configures the following simulation layers in sequence:

- **Muscle layer**  
- **Glue layer**  
- **Fascia layer**  
- **Fat layer**  
- **Skin layer** 

Please, check this [section](#limitations) to know more about the current limitations.

The main function to run turbo is `apply_turbo`, which is defined as follows:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya.turbo import apply_turbo

def apply_turbo(
    mummy,                    # str: name or path of the skeletal mesh
    muscles,                  # str or list: muscle geometry names
    fascia=None,              # str: fascia geometry name
    fat=None,                 # str: fat geometry name
    skin=None,                # str: skin geometry name
    glue=False,               # bool: enable glue layer
    glue_group=None,          # str: group name for glue output geometry
    create_glue_group=True,   # bool: auto-create glue_group if it does not exist
    space_scale=1.0,          # float: simulation scale factor
    force=False,              # bool: remove existing AdonisFX nodes
    report_data=None          # dict: collects errors and warnings
)
</code></pre>

## Requirements

Each layer builds upon the previous one, this means that a specific layer cannot be created unless all the previous layer inputs have been provided.

To configure at least the muscle layer, the following inputs are required:

- **mummy**: the skeletal mesh that drives the muscle simulation.
- **muscles**: one or more meshes representing muscles.

When these two inputs are provided, the muscle layer will be completely configured including AdonisFX locators and sensors.

To configure the downstream layers, the following inputs have to be provided:

- **glue**: flag indicating if the glue layer has to be built.
- **fascia**: the fascia mesh to which AdnSkin is applied. The **glue** input must be `True` for the fascia layer to be built.
- **fat**: the fat mesh to which AdnFat is applied. The **fascia** input must be provided for the fat layer to be built.
- **skin**: the skin mesh to which AdnSkin is applied. The **fat** input must be provided for the skin layer to be built.

## Arguments

In this section we provide a brief overview of the arguments of the `apply_turbo` function.

| Argument | Required | Type | Default | Description |
| :------- | :------- | :--- | :------ | :---------- |
| **mummy**             | Yes      | string         |       | Skeletal mesh that drives the muscle simulation. It can be: 1) the name of the geometry (short name or full path); 2) a group containing the geometry. |
| **muscles**           | Yes      | string or list |       | Geometries to apply a muscle deformer to. It can be: 1) name of one single geometry; 2) a transform group containing multiple geometries; 3) a list of geometry names; 4) a list of groups containing multiple geometries. |
| **fascia**            | Optional | string         | None  | Geometry to apply the skin deformer to. It can be: 1) name of the fascia geometry; 2) group containing the fascia geometry. Requires `glue=True`. |
| **fat**               | Optional | string         | None  | Geometry to apply the fat deformer to. It can be: 1) name of the fat geometry; 2) group containing the fat geometry. Requires fascia to be provided first. |
| **skin**              | Optional | string         | None  | Geometry to apply the skin deformer to. It can be: 1) name of the skin geometry; 2) group containing the skin geometry. Requires fat to be provided first. |
| **glue**              | Optional | bool           | False | If True, creates an AdnGlue node using all muscles as inputs. |
| **glue_group**        | Optional | string         | None  | Name of the group where the glue geometry will be placed. |
| **create_glue_group** | Optional | bool           | True  | If True and `glue_group` is provided, the group is created if it does not exist. |
| **space_scale**       | Optional | float          | 1.0   | Factor to scale simulation space. It will be set to the space scale attribute of all the solvers created. |
| **force**             | Optional | bool           | False | If True, deletes all existing AdonisFX nodes before executing to create the new nodes from a clean scene. Note that auxiliary nodes (e.g. rivets) or meshes created by an existing AdnGlue node will not be deleted. |
| **report_data**       | Optional | dictionary     | None  | A dictionary (`{"errors": [], "warnings": []}`) to capture any issues during execution. |

## How to use

1. Open a scene containing the geometries for all the layers to be built.

<figure style="width:90%; margin-left:5%" markdown>
  ![Maya Scene Ready To Execute The Turbo Script](../images/turbo_script_01.png)
  <figcaption><b>Figure 1</b>: Starting point to execute the turbo script onto an arm asset. The scene contains the geometries for: mummy, muscles, fascia, fat and skin.</figcaption>
</figure>

2. Create the arguments for the `apply_turbo` function.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">mummy       = "mummy_GEO"
muscles     = ["L_deltoid_GEO", "L_bicepsBrachii_GEO", "L_brachialis_GEO", "L_triceps_GEO", ...]
glue        = True
fascia      = "fascia_GEO"
fat         = "fat_GEO"
skin        = "simSkin_GEO"
report_data = {"errors": [], "warnings": []}
</code></pre>

3. Run the following command in a Python Script tab by providing the previous arguments.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya.turbo import apply_turbo
apply_turbo(
    mummy,
    muscles,
    fascia=fascia,
    fat=fat,
    skin=skin,
    glue=glue,
    report_data=report_data
)
</code></pre>

4. Additionally, to place the output glue geometry in a specific group, the group name can be provided via the `glue_group` argument. If the specified group does not exist, setting `create_glue_group` to `True` will make the turbo script to create it automatically.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya.turbo import apply_turbo

mummy             = "mummy_GEO"
muscles           = ["L_deltoid_GEO", "L_bicepsBrachii_GEO", "L_brachialis_GEO", "L_triceps_GEO", ...]
glue              = True
glue_group        = "glue_GRP"
create_glue_group = True
fascia            = "fascia_GEO"
fat               = "fat_GEO"
skin              = "simSkin_GEO"
report_data       = {"errors": [], "warnings": []}

apply_turbo(
    mummy,
    muscles,
    fascia=fascia,
    fat=fat,
    skin=skin,
    glue=glue,
    glue_group=glue_group,
    create_glue_group=create_glue_group,
    report_data=report_data
)
</code></pre>

<figure style="width:90%; margin-left:5%" markdown>
  ![Turbo Execution Completed](../images/turbo_script_02.png)
  <figcaption><b>Figure 2</b>: All simulation layers configured after the execution: muscles, glue, fascia, fat and skin.</figcaption>
</figure>

5. If something goes wrong during the execution, error and warning messages will be added to the `report_data` dictionary. Execute the following code to log all the information in the terminal for troubleshooting.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">import logging
for err in report_data["errors"]:
    logging.error(err)
for warn in report_data["warnings"]:
    logging.warning(warn)
</code></pre>

> [!NOTE]
> - If multiple geometries or groups share the same name in different groups (e.g. group1|geo and group2|geo, group1|group3 and group2|group3), providing the full DAG path will be required.
> - If there are AdonisFX nodes in the scene and the `force` argument is set to `False` the turbo script will generate an error in `report_data` indicating to clear the scene or to run the script again with `force=True` to automatically delete all the AdonisFX nodes.
> - The turbo process can also be executed with the **AdnTurbo tool**. For more details, please refer to the [Turbo Tool page](../tools/turbo_tool).

## Result

As a result of executing the script by providing the geometries for all the layers, the following nodes will be created:

- An AdnMuscle for each muscle geometry with the mummy geometry as target.
- An AdonisFX locator and sensor for each AdnMuscle to drive the muscle activation.
- An AdnGlue node (including its glue output geometry) with all the muscles as inputs.
- An AdnSkin node for the fascia geometry with the mummy and glue geometries as targets.
- An AdnRelax node applied on top of the fascia AdnSkin.
- An AdnFat node for the fat geometry with the fascia geometry as base mesh.
- An AdnRelax node applied on top of the AdnFat.
- An AdnSkin node for the skin geometry.

## Limitations

- The glue layer cannot be bypassed. This means that if the `fascia` argument is provided, the `glue` flag must be `True` for the script to complete successfully.
- If the `force` flag is set to `True` the script will automatically remove all the AdonisFX nodes from the scene (if any). However, other auxiliary nodes created in previous executions of the script will not be removed (i.e. glue output geometry, rivet nodes).
- The default values that the turbo script will use to configure each deformer cannot be customized.
