# Terminology

## Activation Node

The Activation Node, or **AdnActivation**, is an AdonisFX node that performs operations on input activation values to produce a final activation value. This value can be used to drive the activation of a muscle. The node supports operations such as overriding, adding, subtracting, multiplying, and dividing multiple input activations to generate a single output. Input activations can be derived from AdonisFX sensor data (e.g., AdnSensorPosition, AdnSensorDistance, AdnSensorRotation). This node is recommended for on-demand activations or when multiple activations from several sensors need to be merged into one value.

## Constraints

Constraints are rules applied by an AdonisFX solver during simulation to maintain relationships between elements, such as distances between geometry points, external attachments, rig joints, or external meshes. Below is a catalog of constraints:

- **Attachment To Transform**: Defines the relationship between a geometry point and an external transform object. During simulation, it keeps the geometry point at a constant location relative to the transform.

- **Attachment To Geometry**: Defines the relationship between a geometry point and an external mesh object. During simulation, it keeps the geometry point at a constant location relative to the closest point on the target geometry at rest.

- **Distance**: Defines the relationship between two points of a geometry. During simulation, it maintains the edge lengths of the mesh at rest.

- **Fiber**: A specialization of the distance constraint that considers the muscle fiber flow to emulate real fiber contraction behavior.

- **Glue**: Defines the relationship between a geometry point and another point on an external geometry. It keeps the point at a certain distance from the external geometry point without restricting relative orientation. This constraint is used to glue muscles together.

- **Hard**: Defines the location of a geometry point in the tangent space of a polygon. Similar to the attachment constraint, but the transformation used is derived from the tangent space at the closest point on an external geometry.

- **Self-Collision**: Corrects points that intersect with the geometry itself. There are two modes:
  - **Point-to-Point**: Detects intersections when the volume around a point overlaps with another point's volume (e.g., spheres or spheroids).
  - **Triangle-to-Triangle**: Detects intersections when edges of one triangle cross the area of another triangle.

- **Shape Preservation**: Maintains the shape formed by a vertex and its adjacent vertices during simulation.

- **Slide**: Defines the distance between a geometry point and a surface, allowing the point to travel along the surface while maintaining a constant distance.

- **Slide Collision**: Extends the slide constraint by including information about the point's relative orientation to the surface (inside/outside) and allowing proximity adjustments up to a threshold.

- **Slide On Segment**: Defines the relationship between a geometry point and a segment defined by two transform objects (e.g., rig joints). It allows the point to travel along the segment while maintaining a certain distance and restricting twisting.

- **Slide On Geometry**: Defines the relationship between a geometry point and the surface of an external mesh object. It allows the point to travel along the surface while maintaining a constant distance.

- **Soft**: Similar to the glue constraint, it keeps a geometry point at a certain distance from an external geometry point without restricting relative orientation.

- **Uber**: A compound constraint that combines hard, slide, and soft constraints.

- **Volume**: Preserves the volume of a geometry during simulation, with the ability to modulate volume gain or loss using the volume ratio parameter.

- **Volume Shape Preservation**: Maintains the shape of volumetric geometry units during simulation. Used by the fat solver to preserve the shape of the volume between inner and outer layers (fascia and fat geometries).

## Fat

Fat, or **AdnFat**, is an AdonisFX solver for fat simulation. It simulates a mesh surface as if it were a closed volume of fat tissue. The volume is procedurally constructed using two compatible geometries: a base mesh (e.g., fascia) to drive the simulation and a destination mesh (e.g., fat) to apply the simulation. This solver produces realistic dynamics typical of fat tissues.

## Glue

Glue, or **AdnGlue**, is an AdonisFX solver for gluing muscles together after simulation. It creates a more compact muscle layer by combining muscles into one output mesh with glue constraints. The gluing effect can be modulated using a maximum glue distance to reduce unwanted effects. This solver is useful for improving fascia layer simulations by minimizing gaps between muscles.

## Locator

Locators visualize the output of AdonisFX sensors. There are three types of locators, each requiring specific inputs and adopting custom shapes in the viewport:
- **AdnLocatorPosition**: A square box at the location of a node.
- **AdnLocatorDistance**: A parallelepiped with a line connecting two nodes.
- **AdnLocatorRotation**: An angle with two segments connecting three nodes.

Each locator type corresponds to its associated sensor.

## Muscle

**AdnMuscle** is an AdonisFX solver for muscle simulation, including volume preservation. It applies dynamics such as fiber contraction and volume gain to a geometry.

## Muscle Anisotropy

Muscle anisotropy refers to the property of muscle tissue that causes it to behave differently depending on the direction of applied force. In AdonisFX, this property affects edge stiffness based on alignment with the fiber flow:
- Edges aligned with the fiber direction have stiffness equal to the object's overall stiffness.
- Edges orthogonal to the fiber direction have reduced stiffness.

This behavior is modulated at the muscle solver level, where:
- A value of `0.0` (default) makes the object fully isotropic.
- A value of `1.0` makes the object fully anisotropic.

The anisotropy ratio parameter controls the softening of non-aligned edges.

## Muscle Patches

A muscle patch is a group of connected geometry vertices representing an internal muscle projected onto the skin. Muscle patches are not physically modeled geometries. They are used by the AdnSimshape solver for facial simulation. Muscle patches can be generated using the Learn Muscle Patches Tool, which applies machine learning to estimate muscle distribution based on a facial rig's expressions.

**AdonisFX Muscle Patches File**: A proprietary file format (`.amp`) that stores the distribution of muscle patches generated by the Learn Muscle Patches Tool.

## Ribbon Muscle

The Ribbon Muscle, or **AdnRibbonMuscle**, is an AdonisFX solver for muscle simulation. It applies dynamics, such as fiber contraction, to planar geometries.

## Sensor

Sensors measure positions, distances, angles, velocities, and accelerations. There are three types of sensors:
- **AdnSensorPosition**: Requires one input to compute velocity and acceleration.
- **AdnSensorDistance**: Requires two inputs to compute the distance and relative velocity/acceleration.
- **AdnSensorRotation**: Requires three inputs to compute angles, angular velocity, and acceleration.

Each sensor type corresponds to its associated locator for visualizing output values.

## Simshape

Simshape, or **AdnSimshape**, is an AdonisFX solver for facial simulation. It applies dynamics on top of facial rig deformations and mimics changes in skin rigidity due to internal muscle patch activation.

## Skin

Skin, or **AdnSkin**, is an AdonisFX solver for skin and fascia simulation. It applies dynamics to character skin, producing realistic effects like wrinkles.

## Skin Merge

Skin Merge, or **AdnSkinMerge**, is a Maya deformer that merges simulation and animation meshes into a single final mesh. It allows dynamic blending of multiple animated and simulated skin geometries.
