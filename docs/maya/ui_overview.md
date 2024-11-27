# UI Overview

The AdonisFX UI for Maya can be separated into two main elements presented in this page: the **AdonisFX Shelf** and the **AdonisFX Menu**.

## AdonisFX Shelf

The AdonisFX Shelf can be found in the Maya shelf tab under the label *AdonisFX*. It allows for quick access to the main AdonisFX functionalities.

<figure style="width: 100%;" markdown>
  ![AdnLocatorPosition within a scene](images/adonis_shelf.png)
  <figcaption><b>Figure 1</b>: AdonisFX shelf.</figcaption>
</figure>

| Icon | Description | Menu Shortcut |
| :--- | :---------- | :------------ |
| ![AdnLocator](images/adn_adonis_locator.png) | Creates an AdnLocator at the origin. This object is a standard Maya locator with a custom shape for better visualisation in the viewport. | |
| ![AdnLocatorPosition](images/adn_point_locator.png) | Creates an AdnLocatorPosition from the selected transform node. The locator shape represents the position change of the element provided. Double click will launch a simple UI to provide a custom name for the node. | AdonisFX Menu > Create Locators > *Position* |
| ![AdnLocatorDistance](images/adn_distance_locator.png) | Creates an AdnLocatorDistance from the two selected transform nodes. The locator shape represents the distance between the two elements provided. Double click will launch a simple UI to provide a custom name for the node. | AdonisFX Menu > Create Locators > *Distance* |
| ![AdnLocatorRotation](images/adn_angle_locator.png) | Creates an AdnLocatorRotation from the three selected transform nodes. The locator shape corresponds to the angle between the two segments represented by the three nodes. Double click will launch a simple UI to provide a custom name for the node. | AdonisFX Menu > Create Locators > *Rotation* |
|||
| ![AdnSensorPosition](images/adn_point_sensor.png) | Creates an AdnSensorPosition from the transform object and the AdnLocatorPosition selected. If only the transform node is provided, then both the locator and the sensor are created. Double click will launch a simple UI to provide a custom name for the node. | AdonisFX Menu > Create Sensors > *Position* |
| ![AdnSensorDistance](images/adn_distance_sensor.png) | Creates an AdnSensorDistance from the two transform nodes and the AdnLocatorDistance selected. If only the transform nodes are provided, then both the locator and the sensor are created. Double click will launch a simple UI to provide a custom name for the node. | AdonisFX Menu > Create Sensors > *Distance* |
| ![AdnSensorRotation](images/adn_angle_locator.png) | Creates an AdnSensorRotation from the three transform nodes and the AdnLocatorRotation selected. If only the transform nodes are provided, then both the locator and the sensor are created. Double click will launch a simple UI to provide a custom name for the node. | AdonisFX Menu > Create Sensors > *Rotation* |
|||
| ![Create AdnSimshape](images/adn_simshape.png) | Applies an AdnSimshape deformer to the selected mesh. Double click will launch a simple UI to assign a custom name and configure generic solver parameters. | AdonisFX Menu > Create Solvers > *Simshape* |
| ![Add AdnSimshape Collider](images/adn_add_collider.png) | Adds a collider to AdnSimshape selecting the collider and the mesh with AdnSimshape applied. | AdonisFX Menu > Edit Simshape > *Add Collider* |
| ![Remove AdnSimshape Collider](images/adn_remove_collider.png) | Removes a collider from AdnSimshape selecting the collider and the mesh with AdnSimshape applied. | AdonisFX Menu > Edit Simshape > *Remove Collider* |
| ![AdnSimshape Learn Muscle Patches Tool](images/adn_learn_muscle_patches.png) | Launches the Learn Muscle Patches UI used to generate the *AdonisFX Muscle Patches* file (.amp) file. | AdonisFX Menu > Edit Simshape > *Learn Muscle Patches UI* |
| ![AdnSimshape Activations Debugger](images/adn_simshape_debugger.png) | Toggles the AdnSimshape activations debug mode. Current frame has to match the preroll or start frame in the AdnSimshape deformer for this toggle to work. | AdonisFX Menu > Edit Simshape > *Activations Debugger* |
|||
| ![Create AdnSkin](images/adn_skin.png) | Creates AdnSkin deformer to the selected mesh. The deformer will be applied to the last element in the selection. Other elements in the list (optional) will be considered as target meshes. Double click will launch a simple UI to assign a custom name and configure generic solver parameters. | AdonisFX Menu > Create Solvers > *Skin* |
| ![Create AdnSkinMerge](images/adn_skin_merge.png) | Launches the Create Skin Merge UI used to create an AdnSkinMerge deformer. | AdonisFX Menu > Create Deformers > *Skin Merge* |
| ![Add Targets](images/adn_add_skin_targets.png) | Assigns target meshes to the selected AdnSkin deformer. The mesh with the deformer applied must be the last element in the selection. | AdonisFX Menu > Edit Skin > *Add Targets* |
| ![Remove Targets](images/adn_remove_skin_targets.png) | Removes target meshes assigned to the selected AdnSkin deformer. The mesh with the deformer applied must be the last element in the selection. | AdonisFX Menu > Edit Skin > *Remove Targets* |
|||
| ![Create AdnFat](images/adn_fat.png) | Applies an AdnFat deformer to the selected mesh. The deformer will be applied to the second element in the selection, while the first element will be considered as base mesh. | AdonisFX Menu > Create Solvers > *Fat* |
|||
| ![Create AdnRibbonMuscle](images/adn_ribbon_muscle.png) | Creates AdnRibbonMuscle deformer to the selected mesh. The deformer will be applied to the last element in the selection. Other elements in the list (optional) will be considered as target objects. Double click will launch a simple UI to assign a custom name and configure generic solver parameters. | AdonisFX Menu > Create Solvers > *Ribbon Muscle* |
| ![Create AdnMuscle](images/adn_muscle.png) | Creates AdnMuscle deformer to the selected mesh. The deformer will be applied to the last element in the selection. Other elements in the list (optional) will be considered as target objects. Double click will launch a simple UI to assign a custom name and configure generic solver parameters. | AdonisFX Menu > Create Solvers > *Muscle* |
| ![Add Targets](images/adn_add_target.png) | Assigns target objects to the selected deformer (utility compatible with AdnRibbonMuscle and AdnMuscle deformers). The mesh with the deformer applied must be the last element in the selection. | AdonisFX Menu > Edit Muscle > *Add Targets* |
| ![Remove Targets](images/adn_remove_target.png) | Removes target objects assigned to the selected deformer (utility compatible with AdnRibbonMuscle and AdnMuscle deformers). The mesh with the deformer applied must be the last element in the selection. | AdonisFX Menu > Edit Muscle > *Remove Targets* |
| ![Add Slide On Segment](images/adn_add_sliding_constraint.png) | Adds slide segments based on the two (or more) transform objects and the mesh with the deformer node applied (utility compatible with AdnRibbonMuscle and AdnMuscle deformers). The mesh must be the last element in the selection. | AdonisFX Menu > Edit Muscle > *Add Slide On Segment* |
| ![Remove Slide On Segment](images/adn_remove_sliding_constraint.png) | Removes slide segments assigned to the selected deformer (utility compatible with AdnRibbonMuscle and AdnMuscle deformers). The mesh with the deformer applied must be the last element in the selection. | AdonisFX Menu > Edit Muscle > *Remove Slide On Segment* |
| ![Create AdnGlue](images/adn_glue.png) | Creates an AdnGlue node and connects the selected geometries to the inputs array plug of the node. A new geometry will be generated as the result of gluing all the inputs together. | AdonisFX Menu > Create Solvers > *Glue* |
|||
| ![Importer Tool](images/adn_importer.png) | Launches the Importer to load and create nodes from an AdonisFX Asset Definition file (.JSON). | AdonisFX Menu > Tools *Importer* |
| ![Exporter Tool](images/adn_exporter.png) | Launches the Exporter to save AdonisFX nodes information into an AdonisFX Asset Definition file (.JSON). | AdonisFX Menu > Tools *Exporter* |
| ![Paint Tool](images/adn_paint_tool.png) | Opens the AdonisFX Paint Tool to modify the paintable maps in AdnSkin, AdnMuscle and AdnRibbonMuscle deformers. | AdonisFX Menu > *Tools* Paint Tool |
| ![Interactive Playback](images/adn_interactive_playback.png) | Enables Maya Interactive Playback. In this playback mode, dynamic interaction with objects and parameters while simulating is allowed. | AdonisFX Menu > Tools *Interactive Playback* |

## AdonisFX Maya Menu

The AdonisFX Menu provides access to the options in the shelf and other more advanced utilities that are organised in 5 groups: Create, Edit, Tools, License and Help.

<figure style="width: 30%;" markdown>
  ![AdnLocatorPosition within a scene](images/adonis_menu_1.png)
  <figcaption><b>Figure 2</b>: AdonisFX Menu.</figcaption>
</figure>

### Create Section

#### Locators

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Create Locators](images/adonis_menu_locators.png)
  <figcaption><b>Figure 3</b>: AdonisFX Menu Create Locators section.</figcaption>
</figure>

- **Position**. Creates an AdnLocatorPosition from the selected transform node. The locator shape represents the position change of the element provided. Double click will launch a simple UI to provide a custom name for the node. This item corresponds to the shelf button ![AdnLocator](images/adn_adonis_locator.png){style="width:4%"}.
- **Distance**. Creates an AdnLocatorDistance from the two selected transform nodes. The locator shape represents the distance between the two elements provided. Double click will launch a simple UI to provide a custom name for the node. This item corresponds to the shelf button ![AdnLocatorDistance](images/adn_distance_locator.png){style="width:4%"}.
- **Rotation**. Creates an AdnLocatorRotation from the three selected transform nodes. The locator shape corresponds to the angle between the two segments represented by the three nodes. Double click will launch a simple UI to provide a custom name for the node. This item corresponds to the shelf button ![AdnLocatorRotation](images/adn_angle_locator.png){style="width:4%"}.

#### Sensors

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Create Sensors](images/adonis_menu_sensors.png)
  <figcaption><b>Figure 4</b>: AdonisFX Menu Create Sensors section.</figcaption>
</figure>

- **Position**. Creates an AdnSensorPosition from the transform object and the AdnLocatorPosition selected. If only the transform nodes is provided, then both the locator and the sensor are created. Double click will launch a simple UI to provide a custom name for the node. This item corresponds to the shelf button ![AdnSensorPosition](images/adn_point_sensor.png){style="width:4%"}.
- **Distance**. Creates an AdnSensorDistance from the two transform nodes and the AdnLocatorDistance selected. If only the transform nodes are provided, then both the locator and the sensor are created. Double click will launch a simple UI to provide a custom name for the node. This item corresponds to the shelf button ![AdnSensorDistance](images/adn_distance_sensor.png){style="width:4%"}.
- **Rotation**. Creates an AdnSensorRotation from the three transform nodes and the AdnLocatorRotation selected. If only the transform nodes are provided, then both the locator and the sensor are created. Double click will launch a simple UI to provide a custom name for the node. This item corresponds to the shelf button ![AdnSensorRotation](images/adn_angle_locator.png){style="width:4%"}.

Both in Locators and Sensors there are option boxes to launch a simple UI to provide a custom name for the node to create.

<figure style="width: 50%;" markdown>
  ![Locator Sensor Creator UI](images/adn_position_locator_sensor_locator_creator.png)
  <figcaption><b>Figure 5</b>: Locators and Sensors creator UI.</figcaption>
</figure>

#### Nodes

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Edit AdnSimshape](images/adonis_menu_nodes.png)
  <figcaption><b>Figure 6</b>: AdonisFX Menu Create Nodes section.</figcaption>
</figure>

- **Edge Evaluator**. Creates an AdnEdgeEvaluator node from two selected meshes with the same topology. 

#### Deformers

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Create Deformers](images/adonis_menu_deformers.png)
  <figcaption><b>Figure 7</b>: AdonisFX Menu Create Deformers section.</figcaption>
</figure>

- **Skin Merge**. Launches the Create Skin Merge UI used to create an AdnSkinMerge deformer. This item corresponds to the shelf button ![Create AdnSkinMerge](images/adn_skin_merge.png){style="width:4%"}.

#### Solvers

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Create Solvers](images/adonis_menu_solvers.png)
  <figcaption><b>Figure 8</b>: AdonisFX Menu Create Solvers section.</figcaption>
</figure>

- **Simshape**. Applies an AdnSimshape deformer to the selected mesh. This item corresponds to the shelf button ![Create AdnSimshape](images/adn_simshape.png){style="width:4%"}.
- **Skin**. Creates an AdnSkin deformer to the selected mesh. This item corresponds to the shelf button ![Create AdnSkin](images/adn_skin.png){style="width:4%"}.
- **Fat**. Applies an AdnFat deformer to the selected mesh. The deformer will be applied to the second element in the selection. The first element will be considered as base mesh. This item corresponds to the shelf button ![Create AdnFat](images/adn_fat.png){style="width:4%"}.
- **Ribbon Muscle**. Creates AdnRibbonMuscle deformer to the selected mesh. The deformer will be applied to the last element in the selection. Other elements in the list (optional) will be considered as attachment objects. This item corresponds to the shelf button ![Create AdnRibbonMuscle](images/adn_ribbon_muscle.png){style="width:4%"}.
- **Muscle**. Creates AdnMuscle deformer to the selected mesh. The deformer will be applied to the last element in the selection. Other elements in the list (optional) will be considered as attachment objects. This item corresponds to the shelf button ![Create AdnMuscle](images/adn_muscle.png){style="width:4%"}.
- **Glue**. Creates an AdnGlue node and connects the selected geometries to the inputs array plug of the node. A new geometry will be generated as the result of gluing all the inputs together. This item corresponds to the shelf button ![Create AdnGlue](images/adn_glue.png){style="width:4%"}.

Option boxes can be used to launch a UI to assign the name to the deformer and configure generic solver parameters.

<figure style="width: 50%;" markdown>
  ![AdonisFX AdnSkin Deformer Creator](images/adn_skin_deformer_creator.png)
  <figcaption><b>Figure 9</b>: Deformer Creator UI creating for an AdnSkin deformer.</figcaption>
</figure>

### Edit Section

#### Sensors

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Edit Sensors](images/adonis_menu_connection_editor.png)
  <figcaption><b>Figure 10</b>: AdonisFX Menu Edit Sensors section.</figcaption>
</figure>

- **Connection Editor**. Launches the Sensors Connection Editor UI. This tool will assist with the connection of the locators and sensors output plugs with the AdonisFX deformer nodes.

#### Deformers

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Create Solvers](images/adonis_menu_edit_deformers.png)
  <figcaption><b>Figure 11</b>: AdonisFX Menu Edit Deformers section.</figcaption>
</figure>

- **Edit Skin Merge**. Launches the Edit Skin Merge UI. This tool will assist with the edition of simulation and animation meshes lists of an AdnSkinMerge deformer. To open this UI a mesh with an AdnSkinMerge applied must be selected.

#### Simshape

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Edit AdnSimshape](images/adonis_menu_simshape.png)
  <figcaption><b>Figure 12</b>: AdonisFX Menu Edit AdnSimshape section.</figcaption>
</figure>

- **Learn Muscle Patches UI**. Launches the Learn Muscle Patches UI required to generate the *AdonisFX Muscle Patches* (.amp) file. This item corresponds to the shelf button ![AdnSimshape Learn Muscle Patches Tool](images/adn_learn_muscle_patches.png){style="width:4%"}.
- **Activations Debugger**. Toggles the AdnSimshape activations debug mode. The current frame must match the specified initialisation frame at the AdnSimshape deformer to toggle. This item corresponds to the shelf button ![AdnSimshape Activations Debugger](images/adn_simshape_debugger.png){style="width:4%"}. 
- **Add Collider**. Assigns the collider to the selected deformer. The selection must consist of: first the mesh to assign as a Collider and lastly the mesh with the deformer applied. This item corresponds to the shelf button ![Add AdnSimshape Collider](images/adn_add_collider.png){style="width:4%"}. 
- **Remove Collider**. Removes the collider from the selected deformer. The selection must consist of: first the Collider mesh to remove and lastly the mesh with the deformer applied. This item corresponds to the shelf button ![Remove AdnSimshape Collider](images/adn_remove_collider.png){style="width:4%"}. 
- **Add Rest Collider**. Assigns the collider at rest to the selected deformer. The selection must consist of: first the mesh to assign as a Rest Collider and lastly the mesh with the deformer applied.
- **Remove Rest Collider**. Removes the collider at rest from the selected deformer. The selection must consist of: first the Rest Collider mesh to remove and lastly the mesh with the deformer applied.
- **Add Rest Mesh**. Assigns the rest mesh to the selected deformer. The selection must consist of: first the Rest Mesh to assign and lastly the mesh with the deformer applied.
- **Remove Rest Mesh**. Removes the rest Mesh from the selected deformer. The selection must consist of: first the Rest Mesh to remove and lastly the mesh with the deformer applied.
- **Add Deform Mesh**. Assigns the deform mesh to the selected deformer. The selection must consist of: first the Deform Mesh to assign and lastly the mesh with the deformer applied.
- **Remove Deform Mesh**. Removes the deform mesh from the selected deformer. The selection must consist of: first the Deform Mesh to remove and lastly the mesh with the deformer applied.
- **Add Anim Mesh**. Assigns the animated mesh to the selected deformer. The selection must consist of: first the Anim Mesh to assign and lastly the mesh with the deformer applied.
- **Remove Anim Mesh**. Removes the animated mesh from the selected deformer. The selection must consist of: first the Anim Mesh to remove and lastly the mesh with the deformer applied.
- **Connect Activations Plug**. Connects the output compression map from an AdnEdgeEvaluator node to the activations plug of the AdnSimshape selected deformer. The selection must consist of: first the Edge Evaluator node and lastly the AdnSimshape deformer node.
- **Disconnect Activations Plug**. Disconnects the output compression map from an AdnEdgeEvaluators node from the activations plug of the AdnSimshape selected deformer. The selection must consist of: first the Edge Evaluator node and lastly the AdmSimshape deformer node.

#### Skin

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Edit Skin](images/adonis_menu_skin.png)
  <figcaption><b>Figure 13</b>: AdonisFX Menu Edit Skin section.</figcaption>
</figure>

- **Add Targets**. Adds target meshes to the selected skin. The mesh with the deformer applied must be the last element in the selection. This item corresponds to the shelf button ![Add Targets](images/adn_add_skin_targets.png){style="width:4%"}.
- **Remove Targets**. Removes target meshes from the selected skin. The mesh with the deformer applied must be the last element in the selection. If only the skin geometry is selected, then all targets are removed. This item corresponds to the shelf button ![Remove Targets](images/adn_remove_skin_targets.png){style="width:4%"}.

### Fat

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Edit Fat](images/adonis_menu_fat.png)
  <figcaption><b>Figure 14</b>: AdonisFX Menu Edit Fat section.</figcaption>
</figure>

- **Add Base Mesh**. Assigns a base mesh to the selected fat. The selection must consist of: first the mesh to assign as Base Mesh and lastly the mesh with the deformer applied.
- **Remove Base Mesh**. Removes the base mesh from the selected fat. The selection must consist of: the mesh with the deformer applied.

#### Muscle

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Edit Muscle](images/adonis_menu_muscle.png)
  <figcaption><b>Figure 15</b>: AdonisFX Menu Edit Muscle section.</figcaption>
</figure>

- **Add Targets**. Adds target objects to the selected muscle. The mesh with the deformer applied must be the last element in the selection. This item corresponds to the shelf button ![Add Targets](images/adn_add_target.png){style="width:4%"}.
- **Remove Targets**. Removes target objects from the selected muscle. The mesh with the deformer applied must be the last element in the selection. If only the muscle geometry is selected, then all targets are removed. This item corresponds to the shelf button ![Remove Targets](images/adn_remove_target.png){style="width:4%"}.
- **Add Slide On Segment Constraint**. Adds segments based on the two (or more) transform objects and the mesh with the deformer node applied selected. This item corresponds to the shelf button ![Add Slide On Segment](images/adn_add_sliding_constraint.png){style="width:4%"}.
- **Remove Slide On Segment Constraint**. Removes anchors from segments based on the transform objects and the mesh with the deformer node applied selected. This item corresponds to the shelf button  ![Remove Slide On Segment](images/adn_remove_sliding_constraint.png){style="width:4%"}.
- **Draw Fibers**. Enables *Muscle Fibers* Debugging from all the AdnRibbonMuscle and AdnMuscle in the scene.
- **Hide Fibers**. Disables *Muscle Fibers* Debugging from all the AdnRibbonMuscle and AdnMuscle in the scene.

#### Glue

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Edit Muscle](images/adonis_menu_glue.png)
  <figcaption><b>Figure 16</b>: AdonisFX Menu Edit Glue section.</figcaption>
</figure>

- **Add Inputs**. Adds input meshes to an existing AdnGlue node. The output mesh of the destination AdnGlue has to be the last object selected.
- **Remove Inputs**. Removes input meshes from an existing AdnGlue node. The output mesh of the destination AdnGlue has to be the last object selected. If only the glue output mesh is selected, then all inputs will be removed.

#### Debug

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Debug Section](images/adonis_menu_debug.png)
  <figcaption><b>Figure 17</b>: AdonisFX Menu Debug section.</figcaption>
</figure>

- **Refresh Debugger**. Refreshes the scene graph for debugging purposes by making sure the AdnDataNode and the AdnDebugLocator exist in the scene and are properly connected.

### Tools section

#### Utils

<figure style="width: 50%;" markdown>
  ![AdonisFX Menu Debug Section](images/adonis_menu_utils.png)
  <figcaption><b>Figure 18</b>: AdonisFX Menu Utils section.</figcaption>
</figure>

- **Upgrade Deprecated Nodes**. Refreshes the node graph and upgrades all deprecated nodes making sure that the scene still works the same.

<br/>

- **Import**. Launches the AdonisFX Asset Definition Importer to load and create AdonisFX nodes from file (.JSON). This item corresponds to the shelf button ![Importer Tool](images/adn_importer.png){style="width:4%"}.
- **Export**. Launches the AdonisFX Asset Definition Exporter to save AdonisFX nodes information into a file (.JSON). This item corresponds to the shelf button ![Exporter Tool](images/adn_exporter.png){style="width:4%"}.
- **Paint Tool**. Opens the Paint Tool UI to modify the paintable maps in AdnSkin, AdnMuscle and AdnRibbonMuscle deformers. This item corresponds to the shelf button ![Paint Tool](images/adn_paint_tool.png){style="width:4%"}.
- **Interactive Playback**. Enables Maya Interactive Playback. In this playback mode, dynamic interaction with objects and parameters while simulating is allowed. This item corresponds to the shelf button ![Interactive Playback](images/adn_interactive_playback.png){style="width:4%"}.

### License section

- **Activate License**. Checks the license status and if it is not activated yet, then a dialog will be prompted to guide on the product key registration. This functionality is only available in Interactive Node-Locked license.

### Help section

- **Documentation**. Opens the AdonisFX technical documentation on a web browser.
- **Tutorials**. Opens the AdonisFX tutorials on YouTube on a web browser.
- **About**. Launches the AdonisFX About dialog with version information and credits.
