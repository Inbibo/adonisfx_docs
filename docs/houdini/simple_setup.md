# A Simple Setup

This page is dedicated to explain, step by step, a simple process of creating and setting every AdonisFX SOP in Houdini. The scenarios presented here are intended to provide the minimum required configurations to obtain plausible results.

## AdnMuscle

## AdnRibbonMuscle

## AdnGlue

To make the simulated muscles behave more compact and avoid large gaps between them, an AdnGlue node can be used. To create a basic scenario using the AdnGlue node, start with a scene with the following elements:

  - A list of simulated muscles to be glued together.
  - A merge node that combines the simulated muscles into a single geometry.

The AdnGlue node will take all the simulated muscles merged as a single input.

> [!NOTE]
> AdnGlue requires the input geometry to contain a primitive attribute to be able to identify each muscle.

### Create Node

To create the AdnGlue node, press TAB and navigate to the submenu AdonisFX > Solvers to find the AdnGlue ![AdnGlue](../images/adn_glue.png){style="width:4%"} SOP type. Then connect the merged muscles to the AdnGlue input and select the *Piece Attribute* to allow the SOP to identify each muscle piece.

<figure>
  <img src="images/simple_setup_glue_00.png">
  <figcaption><b>Figure X</b>: AdnGlue SOP creation scenario. Using null nodes with ADN_IN_ and ADN_OUT_ prefixes to encapsulate the AdonisFX deformable section is recommended to keep the net compatible with the API.</figcaption>
</figure>

Input muscles can be added or removed from the existing AdnGlue by connecting or disconnecting them from the merge node. After that, make sure to recook the AdnGlue at preroll start time for this change to take effect.

> [!NOTE]
> Adding and removing inputs requires to revisit and update the paintable maps to ensure that the painted values are correct for the new list of geometries.

The *Max Glue Distance* attribute is set to 0.0 by default. Therefore, for the glue constraints to take effect, this value must be adjusted.

### Paint Weights

To tweak the point attributes of an AdnGlue SOP, an `attribpaint` is needed. To ease the creation and initial configuration of this node, select the AdnGlue SOP and click on AdonisFX > Utils > Make Paintable. This utility will first create an `attribcreate` node to define the required point attributes and assign their default values. It will then create an `attribpaint` node, allowing these attributes to be interactively modified. Both nodes are automatically named and properly connected to the AdnGlue node.

<figure>
  <img src="images/simple_setup_glue_01.png">
  <figcaption><b>Figure X</b>: Deformable section after using the "Make Paintable" utility.</figcaption>
</figure>

With the *Max Glue Distance* previously adjusted, the default values of the paintable maps already allow the node to compute the glue constraints.

The most important maps are `adnGlueResistance`, `adnMaxGlueDistanceMultiplier`, and `adnShapePreservation`. The first two are flooded with a value of 1.0 by default, while the last one is flooded with 0.0.

Since the *Max Glue Distance* is initially the same for all muscles, you may want to adjust it for specific areas. This can be done by painting the `adnMaxGlueDistanceMultiplier` map. You can paint this map with a value of 0.0 in areas where you do not want the glue constraint to apply. This prevents the creation of the constraint in those areas and can improve the simulation performance.

<figure>
  <img src="images/simple_setup_glue_02.png">
  <figcaption><b>Figure X</b>: Glue Distance Multiplier map painted in specific areas where muscles are supposed to be glued together.</figcaption>
</figure>

The `adnGlueResistance` map modulates the strength of the glue constraint. To reduce the effect of the constraint in specific areas, lower the values in this map accordingly. Glue constraints won't be computed for vertices with a weight value of 0.0.

<figure>
  <img src="images/simple_setup_glue_03.png">
  <figcaption><b>Figure X</b>: Glue Resistance map painted in specific areas where muscles are supposed to be glued together.</figcaption>
</figure>

Finally, shape preservation constraints help to maintain the original shape of the muscles. These constraints are useful if the gluing produces undesired shape on the output mesh. If that is not the case, then this map can stay unmodified (0.0) which will make the solver run faster. If shape preservation is required, then increase the values on those areas where the shape has been altered during the simulation.

## AdnFat

## AdnSkin

## AdnRelax

## AdnPush

## AdnSkinMerge

## AdnSimshape
