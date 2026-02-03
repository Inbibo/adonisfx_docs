# Terminology

## Activation Node

Activation Node or **AdnActivation** is an AdonisFX node that allows to perform operations on input activation values to produce a final activation value that can be used to drive the activation of a muscle. This node allows to override, add, subtract, multiply, divide, etc. multiple input activations to produce one single output. The input activations can be used by ingesting AdonisFX sensor data (AdnSensorPosition, AdnSensorDistance, AdnSensorRotation). This node is recommended to be used when on-demand activations are required or when multiple activations from several sensors have to be merged into one value.

## Constraints

Constraints are rules that an AdonisFX solver applies during simulation to ensure that the relationship between elements involved in the simulation is maintained, such as distance between geometry points, distance between geometry points and external attachments, rig joints or external meshes, etc. The catalog of constraints is presented below.

**Attachment To Transform**. An attachment to transform constraint defines the relationship between a geometry point and an external transform object. During simulation, an attachment constraint will try to keep the geometry point at a constant location relative to the transform.

**Attachment To Geometry**. An attachment to geometry constraint defines the relationship between a geometry point and an external mesh object. During simulation, an attachment constraint will try to keep the geometry point at a constant location relative to the closest point to the target geometry at rest.

**Distance**. A distance constraint defines the relationship between two points of a geometry. During simulation, distance constraints will try to keep the edge lengths of the mesh at rest.

**Fiber**. A fiber constraint defines the relationship between two points of a muscle geometry. It is a specialization of the distance constraint where the muscle fibers flow is taken into consideration to emulate the behavior of a real fiber contraction.

**Glue**. A glue constraint defines the relationship between a geometry point and another point on an external geometry. These constraints aim to keep the point at a certain distance to the external geometry point without any restrictions of relative orientation. The constraint behavior aligns with Soft Constraints that are used to glue muscles together.

**Hard**. A hard constraint defines the location of a geometry point in the tangent space of a polygon. This constraint type is similar to the attachment constraint but in this case the transformation used is the one given by the tangent space at the closest point on an external geometry.

**Self-Collision**. Applies corrections to the points that are intersecting with the geometry itself. There are two modes of self-collisions correction in AdonisFX: point-to-point and triangle-to-triangle. In point-to-point mode, an intersection occurs if the volume around a point intersects with the volume of another point. This volume can be a perfect sphere (uniform, defined by a radius) or a spheroid (when there is thickness and differs with the radius). In triangle-to-triangle mode, an intersection occurs if two triangles are intersecting each other, which can happen if one or two edges of one triangle cross the area of the other triangle.

**Shape Preservation**. A shape preservation constraint defines the state of the shape formed by a vertex with its adjacents on initialization. During simulation, a shape preservation constraint will try to maintain the rest shape of the geometry with its neighboring vertices.

**Slide**. A slide constraint defines the distance between a geometry point and a surface. This constraint allows the point to travel along the surface. During simulation, this constraint will try to keep the point at a constant distance to the surface in a given radius.

**Slide Collision**. A slide collision constraint is an extension of a slide constraint that includes information about the relative orientation of the point against the surface (inside/outside) plus the ability to allow the point to be closer to the surface up to a given threshold.

**Slide On Segment**. A slide on segment constraint defines the relationship between a geometry point and a segment defined by two transform objects (i.e. two joints of a rig). This constraint aims to keep the point at a certain distance to the segment but with the possibility of traveling along the segment. It also includes a restriction by angle, preventing the simulated point to twist around the segment.

**Slide On Geometry**. A slide on geometry constraint defines the relationship between a geometry point and a surface of an external mesh object. This constraint allows the point to travel along the surface. During simulation, this constraint aims to keep the point at a constant distance to the surface in a given radius.

**Soft**. A soft constraint defines the relationship between a geometry point and another point on an external geometry. This constraint aims to keep the point at a certain distance to the external geometry point without any restrictions of relative orientation.

**Uber**. A uber constraint is a compound of hard, slide and soft constraints.

**Volume**. A volume constraint defines the volume at rest of a geometry. During simulation, this constraint will try to preserve the volume of the geometry with the ability to introduce volume gain or loss modulated by the volume ratio parameter.

**Volume Shape Preservation**. A volume shape preservation constraint defines the state of the shape of a unit of volume of a volumetric geometry on initialization. This constraint is used by the fat solver to preserve the shape of every piece of volume existing in the structure generated between the inner and outer layers (fascia and fat geometries respectively) during simulation.

## Fat

Fat or **AdnFat** is an AdonisFX solver for fat simulation. This solver allows simulating a mesh surface as if it were a closed volume of fat tissue. The volume is constructed procedurally using two compatible geometries: a base mesh to drive the simulation (i.e. the fascia) and a destination mesh (i.e. the fat) on which to apply the simulation. Thanks to that internal volume structure, the solver is able to produce realistic dynamics typical of fat tissues.

## Glue

Glue or **AdnGlue** is an AdonisFX solver for gluing muscles together after simulation. This solver allows to glue muscles together giving the simulation of the muscles layer a more compact look. The gluing is achieved by ingesting the muscles into the solver and generating one combined output mesh with Glue Constraints applied. Given a maximum glue distance the gluing can be modulated and controlled to reduce the gluing effect against unwanted muscles. Glue can be useful for improving the simulation of the fascia layer by creating a more compact version of the muscles layer avoiding big gaps.

## Locator

Locators are intended to visualize the output of an AdonisFX sensor. There are three types of locators that require a specific number of inputs and adopt custom shapes in the viewport: AdnLocatorPosition (a squared box at the location of a node), AdnLocatorDistance (a parallelepiped with a line connecting two nodes) and AdnLocatorRotation (an angle with two segments connecting three nodes). Each type is associated with its homologous sensor.

## Muscle

**AdnMuscle** is an AdonisFX solver for muscle simulation including volume preservation. It allows applying dynamics such as fibers contraction and volume gain to a geometry.

## Muscle anisotropy

Muscle anisotropy refers to the property of muscle tissue that causes it to behave differently depending on the direction of the applied forces. In AdonisFX, this property affects the edge stiffness based on the alignment with the fiber flow:

- Edges aligned with the fiber direction have stiffness equal to the object's overall stiffness.
- Edges orthogonal to the fiber direction have reduced stiffness.

This behavior is modulated with the anisotropy parameter where a value of 0.0 (default) makes the object fully isotropic, and a value of 1.0 makes the object fully anisotropic.

## Muscle Patches

A muscle patch is a group of connected geometry vertices that represent an internal muscle projected onto the skin. A muscle patch is not an actual modelled geometry. Muscle patches are used by AdnSimshape solver for facial simulation. The muscle patches of a facial geometry can be generated with the Learn Muscle Patches Tool which applies Machine Learning techniques to estimate the distribution of muscles based on the set of facial expressions that a facial rig can reproduce.

**AdonisFX Muscle Patches File**. The AdonisFX Muscle Patches File is a proprietary file format that stores the distribution of muscle patches generated by the Learn Muscle Patches tool. The file extension is `amp`.

## Push

Push or **AdnPush** is a deformer that applies a displacement to the vertices of a mesh in the direction of the normals. This effect is modulated with a scalar value to define the global displacement and a paintable map to provide control per vertex. If the sign of the scalar value is positive the displacement is applied in the direction of the normal (outwards), while if the sign is negative the displacement is applied in the opposite direction (inwards).

## Relax

Relax or **AdnRelax** is a deformer designed to smooth creases and correct over-compression or over-stretching on geometry surfaces. This deformer can help refine different types of meshes, like the fascia and skin resulting from the simulation by computing an iterative algorithm that combines smoothing, relaxation, and volume corrections.

## Remap

In terms of functionality, **AdnRemap** nodes are typically used in AdonisFX rigs to remap the output of a sensor into a value that adjusts better to the range expected at the destination attribute of a solver, like the activation or the volume ratio gain of a muscle. In terms of workflow, these nodes aim to enhance the portability of the whole AdonisFX rig, including not only the input and output connections but also the configuration of the remap ramp attribute.

## Ribbon Muscle

The ribbon muscle or **AdnRibbonMuscle** is an AdonisFX solver for muscle simulation. It allows applying dynamics such as fibers contraction to a planar geometry.

## Sensor

Sensors are nodes to measure positions, distances, angles, velocities and accelerations. There are three types of sensors that require different number of input transform objects: AdnSensorPosition (one single input to compute its velocity and acceleration), AdnSensorDistance (two inputs to compute the distance between them and their relative velocity and acceleration) and AdnSensorRotation (three inputs to compute the angle between them and the angular velocity and acceleration). Each type is associated with its homologous locator that will allow visualizing the output values.

## Simshape

Simshape or **AdnSimshape** is an AdonisFX solver for facial simulation. It allows applying dynamics on top of the deformation driven by a facial rig. Also, it has the ability to mimic the change in rigidity of the skin due to the activation of the internal facial muscle patches.

## Skin

Skin or **AdnSkin** is an AdonisFX solver for skin and fascia simulation. It allows applying dynamics to the skin of a character to produce realistic effects like wrinkles.

## Skin Merge

Skin Merge or **AdnSkinMerge** is a deformer to merge simulation and animation meshes into a single final mesh. It allows selecting multiple animated and simulated skin geometries and dynamically blending their results.
