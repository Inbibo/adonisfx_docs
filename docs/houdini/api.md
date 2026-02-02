# API

### Experimental Python API

> [!NOTE]
> - This API is experimental, and will be subject to changes in following versions of AdonisFX.
> - The use of this API in production applications is not supported.

An experimental Python API has been developed to allow Technical Directors to implement custom Python scripts for exporting and rebuilding AdonisFX rigs programmatically.

This API enables users to:
- Extract the setup from an existing rig in Houdini.
- Rebuild the rig in another Houdini scene.
- Export rig data in a format that could be imported into other DCCs (for example Maya).

As this API is still under active development, please do not hesitate to send an email to **adonis.support@inbibo.co.uk** to provide feedback and/or feature requests. The support and development teams will work together to incorporate user feedback and refine the implementation.

The API can be found in `AdonisFX/python/adn/api/adnx.py`.
The definitions can be imported with `from adn.api.adnx import *`.

Since the method definitions may change before the API becomes production-ready, here are some examples showing how to use the current experimental Python API for Houdini. Similar methods can be found directly in the `adnx.py` file.

1. How to create a rig instance with Houdini as the host: `rig = AdnRig(AdnHost.kHoudini)`
2. How to set the context in which the rig information will be gathered or created: `rig.setContext("/obj/geo1")`
3. How to create an AdonisFX rig component and add it to the rig (e.g. an AdnMuscle inside the rig): `muscle = AdnMuscle(rig)` and `rig.addSolver(muscle)`
4. How to gather data from an existing AdonisFX scene to populate the rig component entry (assuming AdnMuscle1 exists in the Houdini scene): `muscle.fromNode("AdnMuscle1")`
5. How to get the dictionary containing the extracted data: `data = muscle.getData()`
6. How to populate the rig component from a dictionary that contains all required entries: `muscle.fromDict(data)`. The required dictionary formatting can be found in the `__init__` methods of the `AdnMuscleBase` and `AdnMuscle` classes. Modifying dictionary entries allows users to update or rebuild rigs with custom values.
7. How to update an existing rig component in the scene after modifying its values: `muscle.update()`. This method assumes that the target AdnMuscle already exists in the scene.
8. How to build rig components in the scene: `muscle.build()` to build the muscle or `rig.build()` to build all the components.
9. How to define the execution order when extracting data from an existing scene: `rig.buildExecutionOrder()`. With an already configured scene, this deduces the correct reconstruction order required to preserve deformation and node dependency chain.
10. How to clear a specific rig component from the scene: `muscle.clear()`

All other methods can be found in the `AdonisFX/python/adn/api/adnx.py` file.

The API is the base foundation for the Import/Export tools of AdonisFX. Below is an example of exported rig data in a .json file:

<figure markdown>
  ![Houdini API Json example](images/houdini_api_json_example.png)
  <figcaption><b>Figure 1</b>: Houdini API Json example.</figcaption>
</figure>

Houdini rigs require some extra nodes to be added for API support. Below is an example network for an AdnMuscle rig component in Houdini.

Each geometry to be deformed must be separated and encapsulated in a deformable region with two null nodes prefixed with:
- `ADN_IN_<geo_name>`
- `ADN_OUT_<geo_name>`

The `<geo_name>` should match the expected shape name counterpart in Maya.

To ease the process of separating geometries, use the utility:
- *AdonisFX* > *Utils* > *Separate Geometries*

This tool works when there is a valid piece attribute (path, name, or muscle_id) on the geometry stream.

<figure markdown>
  ![Houdini muscle net example](images/muscle_net_example.png)
  <figcaption><b>Figure 2</b>: Muscle network example with a deformable region.</figcaption>
</figure>

> [!NOTE]
> - Deformed geometry uses the `Shape` suffix to describe the "geometry" entry. This is important when moving data between DCCs, as it must adhere to the naming convention.
> - Data such as "geometryAttachments" are represented using the name without the `Shape` suffix. This is also important for interoperability between DCCs.
> - A context must be defined in Houdini using the `rig.setContext("/obj/geo1")` method. This allows the API to know from which geometry context to extract data and where to reconstruct the rig.
> - Rig components in Houdini must live directly inside the geometry node. Encapsulating components inside subnetworks (for example placing AdnMuscle nodes in a subnetwork) is not supported.
