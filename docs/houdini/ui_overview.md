# UI Overview

## AdonisFX TAB Menu

The catalog of SOPs in AdonisFX can be inspected in the TAB Menu inside any geometry context under the submenu *AdonisFX*. It allows for quick access and creation of AdonisFX SOPs and HDAs. All of them are distributed in 5 submenus by type: Deformers, Locators, Sensors, Solvers and Utils.

<figure style="width: 50%;" markdown>
  ![AdonisFX TAB menu](images/ui_overview_tab_menu.png)
  <figcaption><b>Figure 1</b>: AdonisFX TAB Menu.</figcaption>
</figure>

| Icon | Description | TAB Submenu |
| :--- | :---------- | :---------- |
| ![AdnRelax](../images/adn_relax.png) | Creates an AdnRelax SOP. | AdonisFX > Deformers > *AdnRelax* |
| ![AdnPush](../images/adn_push.png) | Creates an AdnPush SOP. | AdonisFX > Deformers > *AdnPush* |
|||
| ![AdnLocatorPosition](../images/adn_point_locator.png) | Creates an AdnLocatorPosition SOP. | AdonisFX > Locators > *AdnLocatorPosition* |
| ![AdnLocatorDistance](../images/adn_distance_locator.png) | Creates an AdnLocatorDistance SOP. | AdonisFX > Locators > *AdnLocatorDistance* |
| ![AdnLocatorRotation](../images/adn_angle_locator.png) | Creates an AdnLocatorRotation SOP. | AdonisFX > Locators > *AdnLocatorRotation* |
|||
| ![AdnSensorPosition](../images/adn_point_sensor.png) | Creates an AdnSensorPosition SOP. | AdonisFX > Sensors > *AdnSensorPosition* |
| ![AdnSensorDistance](../images/adn_distance_sensor.png) | Creates an AdnSensorDistance SOP. | AdonisFX > Sensors > *AdnSensorDistance* |
| ![AdnSensorRotation](../images/adn_angle_sensor.png) | Creates an AdnSensorRotation SOP. | AdonisFX > Sensors > *AdnSensorRotation* |
|||
| ![AdnFat](../images/adn_fat.png) | Creates an AdnFat SOP. | AdonisFX > Solvers > *AdnFat* |
| ![AdnGlue](../images/adn_glue.png) | Creates an AdnGlue SOP. | AdonisFX > Solvers > *AdnGlue* |
| ![AdnMuscle](../images/adn_muscle.png) | Creates an AdnRelax SOP. | AdonisFX > Solvers > *AdnMuscle* |
| ![AdnRibbonMuscle](../images/adn_ribbon_muscle.png) | Creates an AdnRibbonMuscle SOP. | AdonisFX > Solvers > *AdnRibbonMuscle* |
| ![AdnSimshape](../images/adn_simshape.png) | Creates an AdnSimshape SOP. | AdonisFX > Solvers > *AdnSimshape* |
| ![AdnSkin](../images/adn_skin.png) | Creates an AdnSkin SOP. | AdonisFX > Solvers > *AdnSkin* |
| ![AdnSkinMerge](../images/adn_skin_merge.png) | Creates an AdnSkinMerge SOP. | AdonisFX > Solvers > *AdnSkinMerge* |
|||
| ![AdnActivation](../images/adn_activation.png) | Creates an AdnActivation SOP. | AdonisFX > Solvers > *AdnActivation* |
| ![AdnEdgeEvaluator](../images/adn_edge_evaluator.png) | Creates an AdnEdgeEvaluator SOP. | AdonisFX > Solvers > *AdnEdgeEvaluator* |
| ![AdnFiberDiffusion](../images/adn_fiber_diffusion.png) | Creates an AdnFiberDiffusion SOP. | AdonisFX > Solvers > *AdnFiberDiffusion* |
| ![AdnFiberGroom](../images/adn_fiber_groom.png) | Creates an AdnFiberGroom HDA. | AdonisFX > Solvers > *AdnFiberGroom* |
| ![AdnFiberProjection](../images/adn_fiber_projection.png) | Creates an AdnFiberProjection SOP. | AdonisFX > Solvers > *AdnFiberProjection* |
| ![AdnLearnMusclePatches](../images/adn_learn_muscle_patches.png) | Creates an AdnLearnMusclePatches SOP. | AdonisFX > Solvers > *AdnLearnMusclePatches* |
| ![AdnSkinMerge](../images/adn_remap.png) | Creates an AdnSkinMerge SOP. | AdonisFX > Solvers > *AdnRemap* |
|||

## AdonisFX Maya Menu

The AdonisFX Menu provides access to the options in the shelf and other more advanced utilities that are organized in four groups: Tools, I/O, License and Help.

<figure style="width: 30%;" markdown>
  ![AdnLocatorPosition within a scene](images/ui_overview_menu.png)
  <figcaption><b>Figure 2</b>: AdonisFX Menu.</figcaption>
</figure>

### Tools section

- **Utils > Clear**. Removes all AdonisFX nodes from the scene.

- **Turbo**. Opens the Turbo UI, which allows users to build an AdonisFX rig on a clean asset from scratch. The UI is divided into sections for each simulation layer that the AdnTurbo can configure. Users can toggle layers on or off to include or skip them in the execution and select the scene objects required to create and configure the solvers.

### I/O section

- **Import (beta)**. Opens the Import UI which allows to import an AdonisFX rig from a file in disk into the scene.
- **Export (beta)**. Opens the Export UI which allows to export an AdonisFX rig from the scene into a file in disk.

### License section

- **Activate License**. Checks the license status and if it is not activated yet, then a dialog will be prompted to guide on the product key registration. This functionality is only available in the Interactive Node-Locked license.

### Help section

- **Documentation**. Opens the AdonisFX technical documentation on a web browser.
- **Tutorials**. Opens the AdonisFX tutorials on YouTube on a web browser.
- **About**. Launches the AdonisFX About dialog with version information and credits.
