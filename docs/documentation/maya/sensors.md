# AdnSensors

Adonis sensors allow for deformers to read and interpret actions from the scene, enabling deformers to interact with various scene elements. For sensors to be able to gather data they need to get applied to [locators](locators.md), which can be previously created in the scene or created alongside the sensor.

## AdnSensorPosition

AdnSensorPosition is the Adonis sensor to compute and output the relative distance, velocity and acceleration between two transform nodes.

### Create AdnSensorPosition

There are two different methods of creating an AdnSensorPosition, depending if we are applying it to an existing [AdnLocatorPosition](locators.md) or creating it alongside the sensor.

 - If applying to an AdnLocatorPosition:

    1. Select an AdnLocatorPosition from your scene.
    2. Press the ![AdnSensorPosition button](images/adn_point_sensor.png) button in the AdonisFX shelf or press *Position* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnSensorPosition is created, applied to the selected AdnLocatorPosition.

 - If creating the locator alongside the sensor:

    1. Select a scene object with a transform node.
    2. Press the ![AdnSensorPosition button](images/adn_point_sensor.png) button in the AdonisFX shelf or press *Position* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnSensorPosition is created, alongside a new AdnLocatorPosition applied to the same transform node.

## AdnSensorDistance

AdnSensorDistance is the Adonis sensor to compute and output the relative distance, velocity and acceleration between two transform nodes.

### Create AdnSensorDistance

There are two different methods of creating an AdnSensorDistance, depending if we are applying it to an existing [AdnLocatorDistance](locators.md) or creating it alongside the sensor.

 - If applying to an AdnLocatorDistance:

    1. Select an AdnLocatorDistance from your scene.
    2. Press the ![AdnSensorDistance button](images/adn_distance_sensor.png) button in the AdonisFX shelf or press *Distance* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnLocatorDistance is created, applied to the selected AdnLocatorDistance.

 - If creating the locator alongside the sensor:

    1. Select two scene objects with transform nodes.
    2. Press the ![AdnSensorDistance button](images/adn_distance_sensor.png) button in the AdonisFX shelf or press *Distance* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnSensorDistance is created, alongside a new AdnLocatorDistance applied to the same transform node.

## AdnSensorRotation

AdnSensorRotation is the Adonis sensor to compute the angle, angular velocity and angular acceleration represented by three transform nodes.

### Create AdnSensorRotation

There are two different methods of creating an AdnSensorRotation, depending if we are applying it to an existing [AdnLocatorRotation](locators.md) or creating it alongside the sensor.

 - If applying to an AdnLocatorRotation:

    1. Select an AdnLocatorRotation from your scene.
    2. Press the ![AdnSensorRotation button](images/adn_angle_sensor.png) button in the AdonisFX shelf or press *Rotation* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnLocatorRotation is created, applied to the selected AdnLocatorRotation.

 - If creating the locator alongside the sensor:

    1. Select two scene objects with transform nodes.
    2. Press the ![AdnSensorRotation button](images/adn_angle_sensor.png) button in the AdonisFX shelf or press *Rotation* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnSensorRotation is created, alongside a new AdnLocatorRotation applied to the same transform node.

## Attributes

All AdnSensor types share similar attributes, with some specific 

The attributes present in the AdnSensor Attribute Editor are also somewhat similar to those found in the one from [AdnPosition](locators.md), With the addition of scale attributes.

[^1]:  Soft range: higher values can be used.

#### Input
 - **Position**(float3): Current transform node position.
    - In the case of AdnSensorDistance, 2 positions will be displayed, one for each transform node. 
    - In the case of AdnSensorRotation, 3 positions will be displayed, one for each transform node. 

#### Output
 - **Distance** (Float): Displays the distance between the two transform nodes.
    - This attribute is only available for AdnSensorDistance.
 - **Velocity** (Float): Displays the magnitude of the angle formed by the three transform nodes.
    - This attribute is only available for AdnSensorRotation.
 - **Velocity** (Float): Displays the transform's linear velocity magnitude.
 - **Acceleration** (Float): Displays the transform's linear acceleration magnitude.

#### Time Attributes
 - **Start Time** (Time, *Current frame*): Determines the frame at which the simulation starts.
 - **Current Time** (Time, *Current frame*): Current playback frame.

#### Scale Attributes
 - **Time Scale** (Float, 1.0): Sets the scaling factor applied to the simulation time step.
    - Has a range of \[0.0, 2.0\] [^1]
 - **Space Scale** (Float, 1.0): Sets the scaling factor applied to the masses and/or the forces.
    - Has a range of \[0.0, 2.0\] [^1]

## Connecting sensors to deformers

Sensors are meant to be connected to a deformer so that they can automatically control deformer attributes, essentially enabling the deformer to react to external inputs from the scene.

When creating a sensor, alongside it several remap nodes will get created. Thhrough these remap nodes, and their output, we are able to modulate and connect the information obtained by the sensor to a deformer.

<figure markdown>
  ![AdnLocatorPosition within a scene](images/position_sensor_nodes.png){width=60%}
  <figcaption>Figure 1: Nodes created by an AdnLocatorPosition.</figcaption>
</figure>

<figure markdown>
  ![AdnLocatorPosition within a scene](images/distance_sensor_nodes.png){width=60%}
  <figcaption>Figure 2: Nodes created by an AdnLocatorDistance.</figcaption>
</figure>

<figure markdown>
  ![AdnLocatorPosition within a scene](images/rotation_sensor_nodes.png){width=60%}
  <figcaption>Figure 3: Nodes created by an AdnLocatorRotation.</figcaption>
</figure>

<!-- Reference to index.md is meant to be to tools.md -->
This connection is made in a much more user friendly way by making use of the [Connection Editor](index.md), explained in more detail in the [tools](index.md) section.
