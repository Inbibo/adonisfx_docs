# How To Use

**Simshape** is a Maya deformer to get facial simulation in the animation rig of an asset. Given a facial expression, the deformer is able to compute the activation of the vertices in order to emulate the changes in the rigidity of the skin. As result, the dynamics of the simulated skin mimic the behaviour of internal muscles contracting.

During the simulation, the solver reduces the inertias of the vertices with higher values of activation, while it computes standard simulation in the vertices that are not activated. One of the key features of Simshape is the ability to extract muscle information directly from the neutral geometry and the set of deformed geometries with the facial expressions using Machine Learning techniques.

## Requirements

The Simshape deformer requires the following inputs to be provided:

  - <b class="mesh_color"> Rest Mesh (R) </b> with no deformation or animation. (optional) 
  - <b class="mesh_color"> Deform Mesh (D)</b> with deformation driven by the facial expressions. (optional)
  - <b class="mesh_color"> Anim Mesh (A)</b> with deformation driven by the facial expressions and animation result of to the binding to the animation rig. (optional)
  - <b class="mesh_color"> Simulation Mesh (S)</b> to apply the deformer onto. This mesh can be the animation mesh or a separate mesh with no deformation nor animation.

!!! Notes
    - All input geometries must have the same number of vertices.
    - If <b class="mesh_color">R</b> is not provided, the system will use the initial state of <b class="mesh_color">S</b> as the rest mesh.
    - If <b class="mesh_color">D</b> is not provided, the simulation will not produce activations.
    - If <b class="mesh_color">A</b> is not provided, the system will use the input mesh to the deformer (<b class="mesh_color">S</b>) as animated mesh.
## Create Simshape

  1. Select the meshes in the following order:
    ``` mermaid
    graph LR
      A["Rest Mesh\n <i style='font-size:12px;'>Optional</i>"]:::opt --> B;
      B["Simulation Mesh\n <i style='font-size:12px;'>Required</i>"];
      classDef opt fill:#413E63,stroke-dasharray: 5 5
    ```
  2. Press the ![Simshape button](../img/adn_simshape_sim.png) in the AdonisFX shelf or press Simshape in AdonisFX menu.
  3. Simshape is ready to simulate with default settings. Check [this page](attributes.md#attributes) to customize the configuration.

In order to add or remove any of those optional meshes, a set of menu items are exposed in AdonisFX menu > Edit Simshape. In that submenu, we can find the options to manage each mesh type as we present in the Figure 1.

<figure style="width:45%" markdown>
  ![Edit Simshape submenu](../img/simshape_menu.png)
  <figcaption>Figure 1: Edit Simshape submenu.</figcaption>
</figure>
