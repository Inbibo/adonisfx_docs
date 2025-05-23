# Terminology

## Activation Node

Activation Node or **AdnActivation** is an AdonisFX node that allows to perform operations on input activation values to produce a final activation value that can be used to drive the activation of a muscle. This node allows to override, add, subtract, multiply, divide, etc. multiple input activations to produce one single output. The input activations can be used by ingesting AdonisFX sensor data (AdnSensorPosition, AdnSensorDistance, AdnSensorRotation). This node is recommended to be used when on-demand activations are required or when multiple activations from several sensors have to be merged into one value.

## Constraints

Constraints are rules that an AdonisFX solver applies during simulation to ensure that the relationship between elements involved in the simulation is maintained, such as distance between geometry points, distance between geometry points and external attachments, rig joints or external meshes, etc. The catalog of constraints is presented below.

**Attachment To Transform Constraint**. An attachment to transform constraint defines the relationship between a geometry point and an external transform object. During simulation, an attachment constraint will try to keep the geometry point at a constant location relative to the transform.

**Attachment To Geometry Constraint**. An attachment to geometry constraint defines the relationship between a geometry point and an external mesh object. During simulation, an attachment constraint will try to keep the geometry point at a constant location relative to the closest point to the target geometry at rest.

**Distance Constraint**. A distance constraint defines the relationship between two points of a geometry. During simulation, distance constraints will try to keep the edge lengths of the mesh at rest.

**Fiber Constraint**. A fiber constraint defines the relationship between two points of a muscle geometry. It is a specialization of the distance constraint where the muscle fibers flow is taken into consideration to emulate the behavior of a real fiber contraction.

**Glue Constraint**. A glue constraint defines the relationship between a geometry point and another point on an external geometry. These constraints aim to keep the point at a certain distance to the external geometry point without any restrictions of relative orientation. The constraint behavior aligns with Soft Constraints that are used to glue muscles together.

**Hard Constraint**. A hard constraint defines the location of a geometry point in the tangent space of a polygon. This constraint type is similar to the attachment constraint but in this case the transformation used is the one given by the tangent space at the closest point on an external geometry.

**Shape Preservation Constraint**. A shape preservation constraint defines the state of the shape formed by a vertex with its adjacents on initialization. During simulation, a shape preservation constraint will try to maintain the rest shape of the geometry with its neighboring vertices.

**Slide Constraint**. A slide constraint defines the distance between a geometry point and a surface. This constraint allows the point to travel along the surface. During simulation, this constraint will try to keep the point at a constant distance to the surface in a given radius.

**Slide Collision Constraint**. A slide collision constraint is an extension of a slide constraint that includes information about the relative orientation of the point against the surface (inside/outside) plus the ability to allow the point to be closer to the surface up to a given threshold.

**Slide On Segment Constraint**. A slide on segment constraint defines the relationship between a geometry point and a segment defined by two transform objects (i.e. two joints of a rig). This constraint aims to keep the point at a certain distance to the segment but with the possibility of traveling along the segment. It also includes a restriction by angle, preventing the simulated point to twist around the segment.

**Slide On Geometry Constraint**. A slide on geometry constraint defines the relationship between a geometry point and a surface of an external mesh object. This constraint allows the point to travel along the surface. During simulation, this constraint aims to keep the point at a constant distance to the surface in a given radius.

**Soft Constraint**. A soft constraint defines the relationship between a geometry point and another point on an external geometry. This constraint aims to keep the point at a certain distance to the external geometry point without any restrictions of relative orientation.

**Uber Constraint**. A uber constraint is a compound of hard, slide and soft constraints.

**Volume Constraint**. A volume constraint defines the volume at rest of a geometry. During simulation, this constraint will try to preserve the volume of the geometry with the ability to introduce volume gain or loss modulated by the volume ratio parameter.

**Volume Shape Preservation Constraint**. A volume shape preservation constraint defines the state of the shape of a unit of volume of a volumetric geometry on initialization. This constraint is used by the fat solver to preserve the shape of every piece of volume existing in the structure generated between the inner and outer layers (fascia and fat geometries respectively) during simulation.

## Fat

Fat or **AdnFat** is an AdonisFX solver for fat simulation. This solver allows simulating a mesh surface as if it were a closed volume of fat tissue. The volume is constructed procedurally using two compatible geometries: a base mesh to drive the simulation (i.e. the fascia) and a destination mesh (i.e. the fat) on which to apply the simulation. Thanks to that internal volume structure, the solver is able to produce realistic dynamics typical of fat tissues.

## Glue

Glue or **AdnGlue** is an AdonisFX solver for gluing muscles together after simulation. This solver allows to glue muscles together giving the simulation of the muscles layer a more compact look. The gluing is achieved by ingesting the muscles into the solver and generating one combined output mesh with Glue Constraints applied. Given a maximum glue distance the gluing can be modulated and controlled to reduce the gluing effect against unwanted muscles. Glue can be useful for improving the simulation of the fascia layer by creating a more compact version of the muscles layer avoiding big gaps.

## Locator

Locators are intended to visualize the output of an AdonisFX sensor. There are three types of locators that require a specific number of inputs and adopt custom shapes in the viewport: AdnLocatorPosition (a squared box at the location of a node), AdnLocatorDistance (a parallelepiped with a line connecting two nodes) and AdnLocatorRotation (an angle with two segments connecting three nodes). Each type is associated with its homologous sensor.

## Muscle

**AdnMuscle** is an AdonisFX solver for muscle simulation including volume preservation. It allows applying dynamics such as fibers contraction and volume gain to a geometry.

## Muscle Patches

A muscle patch is a group of connected geometry vertices that represent an internal muscle projected onto the skin. A muscle patch is not an actual modelled geometry. Muscle patches are used by AdnSimshape solver for facial simulation. The muscle patches of a facial geometry can be generated with the Learn Muscle Patches Tool which applies Machine Learning techniques to estimate the distribution of muscles based on the set of facial expressions that a facial rig can reproduce.

**AdonisFX Muscle Patches File**. The AdonisFX Muscle Patches File is a proprietary file format that stores the distribution of muscle patches generated by the Learn Muscle Patches tool. The file extension is `amp`.

## Ribbon Muscle

The ribbon muscle or **AdnRibbonMuscle** is an AdonisFX solver for muscle simulation. It allows applying dynamics such as fibers contraction to a planar geometry.

## Sensor

Sensors are nodes to measure positions, distances, angles, velocities and accelerations. There are three types of sensors that require different number of input transform objects: AdnSensorPosition (one single input to compute its velocity and acceleration), AdnSensorDistance (two inputs to compute the distance between them and their relative velocity and acceleration) and AdnSensorRotation (three inputs to compute the angle between them and the angular velocity and acceleration). Each type is associated with its homologous locator that will allow visualizing the output values.

## Simshape

Simshape or **AdnSimshape** is an AdonisFX solver for facial simulation. It allows applying dynamics on top of the deformation driven by a facial rig. Also, it has the ability to mimic the change in rigidity of the skin due to the activation of the internal facial muscle patches.

## Skin

Skin or **AdnSkin** is an AdonisFX solver for skin and fascia simulation. It allows applying dynamics to the skin of a character to produce realistic effects like wrinkles.

## Skin Merge

Skin Merge or **AdnSkinMerge** is a Maya deformer to merge simulation and animation meshes into a single final mesh. It allows selecting multiple animated and simulated skin geometries and dynamically blending their results.

