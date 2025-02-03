# Scripts

## Mirror

The mirroring script is a Python script that allows to transfer the AdonisFX muscle setup of an asset from one side to the other. For example, a user can complete the muscle rig for the left side of an asset and thanks to this script mirror the setup quickly and efficiently to the right side. 

Currently, the script allows to mirror:

- AdnMuscle (settings, paintable maps, geometry targets, connections to sensors)
- AdnLocators (position, distance, rotation)
- AdnSensors (position, distance, rotation).

Please, check this [section](#limitations) to know more about the current limitations.

### How To Use

The character rig to apply the mirroring onto needs to satisfy some requirements for this script to work:

- One completed side of the rig (i.e. left or right). This side will work as source, while the other will work as destination.
- Apply a naming convention to all the objects involved in the mirroring (geometries, muscle deformers, locators and sensors) to allow the script to differentiate between left and right side objects. For example, use a "l_" and "r_", or "L_" and "R_" prefix, or "\_l" and "\_r", or "\_L" and "\_R" suffix.
- The left and right muscles must be symmetric in topology. This means that both the number of vertices and the vertex IDs of a muscle (e.g. "L_biceps") must match those of its counterpart muscle (e.g. "R_biceps") to ensure the paintable maps are mirrored correctly.
- It is recommended to save the scene before executing the script.

<figure style="width:90%; margin-left:5%" markdown>
  ![Maya Scene Ready To Execute The Mirroring](images/mirror_script_00.png)
  <figcaption><b>Figure 1</b>: Starting point to execute the mirroring script onto a biped asset. The left side is fully configured with muscle deformers, locators and sensors following the prefix naming convention "L_*".</figcaption>
</figure>

Once the scene fulfills the requirements, then the procedure to follow is:

1. Select all geometries from the source side with an AdnMuscle applied that need to be mirrored.

2. Add to the selection all the AdonisFX Locators from the same source side that need to be mirrored. Note that sensors (as not being DAG objects) do not need to be added to the selection. The script will take care of mirroring them too.

<figure style="width:90%; margin-left:5%" markdown>
  ![Mirror Script Selection](images/mirror_script_01.png)
  <figcaption><b>Figure 2</b>: All geometry muscles and locators on the left side selected.</figcaption>
</figure>

3. Run the following command in a Python Script tab.

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.scripts.maya import mirror
mirror.apply_mirror(left_convention="L_*", right_convention="R_*")
</code></pre>

4. A confirmation dialog will be displayed, reminding the user that it is recommended to have a saved version of the scene, as the mirroring process cannot be undone.

<figure style="width:60%; margin-left:20%" markdown>
  ![Mirror Script Confirmation Dialog](images/mirror_script_02.png)
  <figcaption><b>Figure 3</b>: Question dialog displayed to ask for confirmation before executing.</figcaption>
</figure>

5. Click *Yes* in the question dialog to proceed with the mirroring.

Depending on the complexity of the rig, this process might take a few seconds to compute. If something goes wrong during the execution, an error dialog will be displayed informing about the problem to help with the troubleshooting.

<figure style="width:90%; margin-left:5%" markdown>
  ![Mirroring Execution Completed](images/mirror_script_03.png)
  <figcaption><b>Figure 4</b>: Result of the execution: all AdnMuscle from the left side are replicated on the right side. Also, all the locators and sensors from the left side are created and connected on the right side.</figcaption>
</figure>

### Limitations

- Node types that are not supported: AdnRibbonMuscle deformer, AdnActivation nodes.
- Settings in AdnMuscle that are not included in the mirroring: Attachments To Transform.
- The naming convention does not allow to place the side identifier at the middle of the name (e.g. biceps_L_muscle).
