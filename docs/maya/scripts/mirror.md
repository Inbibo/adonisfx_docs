# Mirror

The mirroring script is a Python script that allows the transfer of the AdonisFX muscle setup of an asset from one side to the other. For example, a user can complete the muscle rig for the left side of an asset and thanks to this script mirror the setup quickly and efficiently to the right side. 

Currently, the script allows to mirror:

- **AdnMuscle deformers**, including their configurations, paintable maps, geometry targets, and connections to locators.​
- The three types of **AdonisFX locators** (i.e. AdnLocatorPosition, AdnLocatorDistance, and AdnLocatorRotation).
- The three types of **AdonisFX sensors** (i.e. AdnSensorPosition, AdnSensorDistance, and AdnSensorRotation).
- **AdnActivation nodes**, including their input and output connections.

Please, check this [section](#limitations) to know more about the current limitations.

## Requirements

In order to use the mirroring script, the rig must meet the following requirements to ensure a successful transfer of the muscle setup:

- **A completed setup on one side**: One side of the rig (either left or right) must be fully configured. This completed side will serve as the **source**, while the opposite side will be the **destination** for the mirrored setup.

- **Consistent naming convention**: All objects involved in the mirroring process (including geometries, muscle deformers, locators, sensors, activation nodes and any other attachment nodes like rig joints) must follow a naming convention based on prefixes or suffixes (see Figure 1). This allows the tool to differentiate between left and right-side entities. Naming conventions can use:
    - **Prefixes**: e.g., "L_" and "R_" or "l_" and "r_".
    - **Suffixes**: e.g., "_L" and "_R" or "_l" and "_r".

- **Symmetric muscle topology**: The left and right muscles must have identical topology. This means that:
    - The **vertex count** must be the same on both sides.
    - The **vertex IDs** of a muscle (e.g., "L_biceps") must match those of its counterpart (e.g., "R_biceps").

    This ensures that paintable maps and deformer weights are transferred accurately during the mirroring process.

<figure style="width:90%; margin-left:5%" markdown>
  ![Example of naming convention](images/mirror_tool_00.png)
  <figcaption><b>Figure 1</b>: Example of the naming convention (using "L_" prefix) applied to muscles, joints, sensors, locators and activation nodes.</figcaption>
</figure>

## How To Use

1. Open a scene that fulfills the requirements listed previously.

<figure style="width:90%; margin-left:5%" markdown>
  ![Maya Scene Ready To Execute The Mirroring](images/mirror_tool_01.png)
  <figcaption><b>Figure 2</b>: Starting point to execute the mirroring onto a biped asset. The left side is fully configured with muscle deformers, locators, sensors and activation nodes following the prefix naming convention "L_".</figcaption>
</figure>

2. Select all geometries from the source side that have an AdnMuscle deformer applied and need to be mirrored.

3. Add to the selection all the AdonisFX locators from the same source side that need to be mirrored. Note that sensors and activation nodes (as not being DAG objects) do not need to be added to the selection. The Mirror Tool will automatically handle their mirroring.

<figure style="width:90%; margin-left:5%" markdown>
  ![Mirror Script Selection](images/mirror_tool_02.png)
  <figcaption><b>Figure 3</b>: All geometry muscles and locators on the left side selected.</figcaption>
</figure>

4. Run the following command in a Python Script tab.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import mirror
report_data = {"errors": [], "warnings": []}
result = mirror.apply_mirror(left_convention="L_*", right_convention="R_*", report_data=report_data)
</code></pre>

5. Depending on the complexity of the rig, this process might take a few seconds to compute. The `result` returned by the function will be `True` if there were any muscles or locators properly mirrored, and `False` if nothing was mirrored (e.g. if the selection was empty).

<figure style="width:90%; margin-left:5%" markdown>
  ![Mirroring Execution Completed](images/mirror_tool_08.png)
  <figcaption><b>Figure 5</b>: Result of the execution: all AdnMuscle from the left side are replicated on the right side. Additionally, all the locators, sensors and activation nodes from the left side are created and connected on the right side.</figcaption>
</figure>

6. If something goes wrong during the execution, error and warning messages will be added to the `report_data` dictionary. Execute the following code to log all the information in the terminal for troubleshooting.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">import logging
for err in report_data["errors"]:
    logging.error(err)
for warn in report_data["warnings"]:
    logging.warning(warn)
</code></pre>

> [!NOTE]
> - Depending on the need, the script can mirror only the muscles (selection from step 2), only the locators and sensors (selection from step 3), or everything at once (including both selections from step 2 and 3).
> - The mirroring process can also be executed with the **Mirror Tool**. For more details, please refer to the [Mirror Tool page](tools/mirror_tool).

## Limitations

- The naming convention does not allow placing the side identifier at the middle of the name (e.g. biceps_L_muscle).
- The mirroring logic does not allow to mirror intermediate nodes between the AdnActivation and the AdnMuscle deformer.
