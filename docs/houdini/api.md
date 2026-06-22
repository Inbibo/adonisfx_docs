# Houdini Python API

## Experimental Python API

> [!WARNING]
> This API is experimental and may change in future versions of Adonis.
>
> The use of this API in production applications is not supported.

An experimental Python API is available for Technical Directors who need to implement custom Python scripts for exporting and rebuilding Adonis rigs programmatically.

This API enables users to:

- Extract the setup from an existing Adonis rig in Houdini.
- Rebuild the rig in another Houdini scene.
- Export rig data in a format that can be imported into other DCCs, such as Maya.
- Build an entire Adonis rig programmatically.

As this API is still under active development, please send feedback and feature requests to **adonis.support@inbibo.co.uk**. The support and development teams will work together to incorporate user feedback and refine the implementation.

The API can be found in:

`Adonis/python/adn/api/adnx.py`

The definitions can be imported with:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">from adn.api.adnx import *
</code></pre>

The API exposes Adonis rig entities through Python classes and type identifiers. The available classes, supported data entries, and implementation details are defined directly in `adnx.py`.

## Requirements

Before using the Houdini Python API, the Houdini scene must follow the expected Adonis rig structure.

A Houdini context must be defined with `rig.setContext("/obj/geo1")`. This tells the API which Geometry context should be used to extract or rebuild the rig.

Rig components in Houdini must live directly inside the Geometry context. Encapsulating Adonis SOP nodes inside subnetworks is not supported.

Each geometry to be deformed must be separated and encapsulated in a deformable region using two Null nodes prefixed with:

- `ADN_IN_<geo_name>`
- `ADN_OUT_<geo_name>`

The `<geo_name>` value should match the expected shape name counterpart in Maya.

The API uses these deformable region Null nodes to identify the geometry name associated with Adonis SOP nodes. When extracting data from Houdini, the API first looks for an `ADN_IN_` node upstream of the Adonis node, and can also use the corresponding `ADN_OUT_` node as a fallback.

Nodes used to drive attachment to transform or slide on segment constraints, such as Null, joint, or rivet nodes, must live in the `/obj` context.

To ease the process of separating geometries, use:

**Adonis > Utils > Separate Geometries**

This tool works when there is a valid piece attribute on the geometry stream, such as `path`, `name`, or `muscle_id`.

## Basic Usage Examples

The method definitions may change before the API becomes production-ready. The following examples show how to use the current experimental Python API for Houdini.

### Create a Rig Instance

Create a rig instance with Houdini as the host:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">rig = AdnRig(AdnHost.kHoudini)
</code></pre>

### Set the Houdini Context

Set the context where rig information will be gathered or created:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">rig.setContext("/obj/geo1")
</code></pre>

The context must be a valid Houdini node.

### Create a Rig Component

Create an Adonis rig component and add it to the rig. For example, to create an **AdnMuscle** component:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">muscle = AdnMuscle(rig)
rig.addSolver(muscle)
</code></pre>

Some components are added automatically when they are created with a rig instance, depending on their base class. However, explicitly adding the component to the rig can help make the workflow clearer.

### Extract Data from an Existing Node

Gather data from an existing Adonis node in the Houdini scene.

For example, if an **AdnMuscle** node named `AdnMuscle1` exists in the current Houdini context:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">muscle.fromNode("AdnMuscle1")
</code></pre>

### Get Extracted Data

Get the dictionary containing the extracted data:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">data = muscle.getData()
</code></pre>

The returned dictionary contains the component parameters, maps, connections, node information, and other data required to rebuild or update the component.

### Populate a Component from a Dictionary

Populate a rig component from a dictionary that contains all required entries:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">muscle.fromDict(data)
</code></pre>

The required dictionary formatting can be found in the `__init__` methods of the corresponding classes, for example `AdnMuscleBase` and `AdnMuscle`.

Modifying dictionary entries allows users to update or rebuild rigs with custom values.

### Update an Existing Component

Update an existing rig component in the scene after modifying its values:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">muscle.update()
</code></pre>

This method assumes that the target Adonis node already exists in the Houdini scene.

### Build Rig Components

Build a single component in the scene:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">muscle.build()
</code></pre>

Build all components registered in the rig:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">rig.build()
</code></pre>

### Define the Execution Order

Define the execution order when extracting data from an existing scene:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">rig.buildExecutionOrder()
</code></pre>

With an already configured scene, this deduces the reconstruction order required to preserve deformation order and node dependency chains.

The execution order is built from:

1. Sensors.
2. Non-deformable utility nodes.
3. Deformers and solvers in deformation chain order.

### Clear a Component

Clear a specific rig component from the scene:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">muscle.clear()
</code></pre>

In Houdini, clearing a component deletes the corresponding Houdini node. This operation is only expected to work when the network is not cooking.

## Connections

The API can extract and rebuild connections between Adonis nodes.

In Houdini, connections are represented through parameter expressions. The API supports:

- Detail attribute connections.
- Channel reference connections.

When extracting connections from Houdini, the API searches the evaluated node parameters and converts compatible expressions into serialized connection data.

When rebuilding connections in Houdini, the API attempts to recreate those connections using the appropriate expression type.

> [!NOTE]
> Exported connections between Adonis nodes may differ depending on the DCC. This is expected due to differences between DCC applications. However, the rig should be reconstructed correctly when imported into any supported target DCC, as long as the required nodes, geometry, and rig structure are compatible.

## Exported Rig Data

The API is the foundation for the Import and Export tools in Adonis.

Below is an example of exported rig data in a `.json` file:

<figure markdown>
  ![Houdini API JSON example](images/houdini_api_json_example.png)
  <figcaption><b>Figure 1</b>: Houdini API JSON example.</figcaption>
</figure>

All other methods and data definitions can be found in:

`Adonis/python/adn/api/adnx.py`

## Houdini Network Structure

Houdini rigs require extra nodes to be added for API support.

Each geometry to be deformed must be separated and encapsulated in a deformable region with two Null nodes:

- `ADN_IN_<geo_name>`
- `ADN_OUT_<geo_name>`

The `<geo_name>` should match the expected shape name counterpart in Maya.

<figure markdown>
  ![Houdini muscle network example](images/muscle_net_example.png)
  <figcaption><b>Figure 2</b>: Muscle network example with a deformable region.</figcaption>
</figure>

## Naming and Interoperability

When transferring data between DCCs, some naming conventions must be respected.

Deformed geometry uses the `Shape` suffix to describe the `geometry` entry. This is important when moving data between DCCs, because the geometry name must follow the expected naming convention.

Data such as `geometryAttachments` is represented using the name without the `Shape` suffix. This is also important for interoperability between DCCs.

The `<geo_name>` used in `ADN_IN_<geo_name>` and `ADN_OUT_<geo_name>` should match the equivalent expected shape name in Maya.

## Limitations

- Subnetworks inside the Geometry context are not supported. All Adonis SOP nodes, and any SOP nodes containing geometry required by the Adonis rig, must exist at the same level inside the Geometry context, for example `/obj/geo1`.
- Nodes used to drive attachment to transform or slide on segment constraints must live in the `/obj` context.
