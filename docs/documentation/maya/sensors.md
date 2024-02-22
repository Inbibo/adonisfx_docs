# AdnSensors

AdnSensors in Adonis are nodes in charge of interpreting data extracted from transform nodes and compute information that can be fed into the deformers to alter their behavior. In Adonis sensors work in combination with [AdnLocators](locators.md) to display the computed information in an intuitive way using coloring. To be able to display the information computed from the sensors, remappers are used to convert the computed data (Eg. angle) to a valid value in a given range of activation that will drive the coloring of the locators and the activation of an AdnMuscle for example.

## AdnSensorPosition

AdnSensorPosition is the Adonis sensor for computing meaningful output values representing the velocity or acceleration of a transform node. The values of velocity an acceleration can then be remapped to produce desirable activation values to drive the simulation of the deformer. This sensor has to work in combination with an AdnLocatorPosition both for setup and visualization. And example use case for this sensor would be applying it to the wrist connection of an arm outputting velocities while swinging.

### Create AdnSensorPosition

There are two different methods of creating an AdnSensorPosition, depending if we are applying it to an existing [AdnLocatorPosition](locators.md) or creating it alongside the sensor.

 - If applying to an already existing AdnLocatorPosition:

    1. Select an AdnLocatorPosition from your scene.
    2. Press the ![AdnSensorPosition button](images/adn_point_sensor.png) button (click or double-click) in the AdonisFX shelf or press *Position* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnSensorPosition is created, applied to the selected AdnLocatorPosition.

 - If creating the locator alongside the sensor:

    1. Select a scene object with a transform node.
    2. Press the ![AdnSensorPosition button](images/adn_point_sensor.png) button (click or double-click) in the AdonisFX shelf or press *Position* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnSensorPosition is created, alongside a new AdnLocatorPosition is applied to the same transform node.

### How to use

An AdnSensorPosition will be in charge of feeding, after remapping, activation (or other) values into the deformer for driving the simulation and the AdnLocatorPosition for visualization purposes. The value of the sensor can be used to drive the activation of a muscle simulating contraction to increase its stiffness. Find more information for connecting the sensor to the deformer in sections below.

<figure markdown>
  ![AdnSensorPosition velocity display on AdnLocatorPosition within a scene](images/adn_sensor_position.png){width=60%}
  <figcaption>Figure 1: AdnSensorPosition used in a human model.</figcaption>
</figure>

## AdnSensorDistance

AdnSensorDistance is the Adonis sensor for computing meaningful output values representing the distance, velocity or acceleration between two transform nodes. The values of distance, velocity an acceleration can then be remapped to produce desirable activation values to drive the simulation of the deformer. This sensor has to work in combination with an AdnLocatorDistance both for setup and visualization. And example use case for this sensor would be applying it to the connection made between bones which would compute the distance between two bones moving together.

### Create AdnSensorDistance

There are two different methods of creating an AdnSensorDistance, depending if we are applying it to an existing [AdnLocatorDistance](locators.md) or creating it alongside the sensor.

 - If applying to an already existing AdnLocatorDistance:

    1. Select an AdnLocatorDistance from your scene.
    2. Press the ![AdnSensorDistance button](images/adn_distance_sensor.png) button (click or double-click) in the AdonisFX shelf or press *Distance* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnLocatorDistance is created, applied to the selected AdnLocatorDistance.

 - If creating the locator alongside the sensor:

    1. Select two scene objects with transform nodes.
    2. Press the ![AdnSensorDistance button](images/adn_distance_sensor.png) button (click or double-click) in the AdonisFX shelf or press *Distance* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnSensorDistance is created, alongside a new AdnLocatorDistance is applied to the same transform nodes.

### How to use

An AdnSensorDistance will be in charge of feeding, after remapping, activation (or other) values into the deformer for driving the simulation and the AdnLocatorDistance for visualization purposes. The value of the sensor can be used to drive the activation of a muscle simulating contraction to increase its stiffness. Find more information for connecting the sensor to the deformer in sections below.

<figure markdown>
  ![AdnSensorDistance distance display on AdnLocatorDistance within a scene](images/adn_sensor_distance.png){width=60%}
  <figcaption>Figure 2: AdnSensorDistance used in a human model.</figcaption>
</figure>

## AdnSensorRotation

AdnSensorRotation is the Adonis sensor for computing meaningful output values representing the angle, angular velocity or angular acceleration between three transform nodes. The values of velocity and acceleration can then be remapped to produce desirable activation values to drive the simulation of the deformer. This sensor has to work in combination with an AdnLocatorRotation both for setup and visualization. And example use case for this sensor would be applying it to the arc connection made between bones which would compute the angle between two bones rotating.

### Create AdnSensorRotation

There are two different methods of creating an AdnSensorRotation, depending if we are applying it to an existing [AdnLocatorRotation](locators.md) or creating it alongside the sensor.

 - If applying to an already existing AdnLocatorRotation:

    1. Select an AdnLocatorRotation from your scene.
    2. Press the ![AdnSensorRotation button](images/adn_angle_sensor.png) button (click or double-click) in the AdonisFX shelf or press *Rotation* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnLocatorRotation is created, applied to the selected AdnLocatorRotation.

 - If creating the locator alongside the sensor:

    1. Select two scene objects with transform nodes.
    2. Press the ![AdnSensorRotation button](images/adn_angle_sensor.png) button (click or double-click) in the AdonisFX shelf or press *Rotation* in the AdonisFX menu, under the *Sensor* submenu.
    3. The AdnSensorRotation is created, alongside a new AdnLocatorRotation is applied to the same transform nodes.

### How to use

An AdnSensorRotation will be in charge of feeding, after remapping, activation (or other) values into the deformer for driving the simulation and the AdnLocatorRotation for visualization purposes. The value of the sensor can be used to drive the activation of a muscle simulating contraction to increase its stiffness. Find more information for connecting the sensor to the deformer in sections below.

<figure markdown>
  ![AdnSensorRotation angle display on AdnLocatorRotation within a scene](images/adn_sensor_rotation.png){width=60%}
  <figcaption>Figure 3: AdnSensorRotation used in a human model.</figcaption>
</figure>

## Attributes

[^1]:  Soft range: higher values can be used.

### AdnSensorPosition
#### Input
 - **Position**(Float3): Current transform node position.

#### Output
 - **Velocity** (Float): Magnitude of the velocity of the transform node.
 - **Acceleration** (Float): Magnitude of the acceleration of the transform node.

#### Time Attributes
 - **Start Time** (Time, *Current frame*): Determines the frame at which the playback/simulation starts.
 - **Current Time** (Time, *Current frame*): Current playback frame.

#### Scale Attributes
 - **Time Scale** (Float, 1.0): Sets the scaling factor applied to the compute the velocity or acceleration.
    - Has a range of \[0.001, 10.0\] [^1]
 - **Space Scale** (Float, 1.0): Sets the scaling factor applied to velocity or acceleration.
    - Has a range of \[0.001, 100.0\] [^1]

### AdnSensorDistance
#### Input
 - **Start Position**(Float3): Start transform node position.
 - **End Position**(Float3): End transform node position.

#### Output
 - **Distance** (Float): Magnitude of the distance between the transform nodes.
 - **Velocity** (Float): Magnitude of the velocity between the transform nodes.
 - **Acceleration** (Float): Magnitude of the acceleration between the transform nodes.

#### Time Attributes
 - **Start Time** (Time, *Current frame*): Determines the frame at which the playback/simulation starts.
 - **Current Time** (Time, *Current frame*): Current playback frame.

#### Scale Attributes
 - **Time Scale** (Float, 1.0): Sets the scaling factor applied to the compute the velocity or acceleration.
    - Has a range of \[0.001, 10.0\] [^1]
 - **Space Scale** (Float, 1.0): Sets the scaling factor applied to velocity or acceleration.
    - Has a range of \[0.001, 100.0\] [^1]

### AdnSensorRotation
#### Input
 - **Start Position**(Float3): Start transform node position.
 - **Mid Position**(Float3): Mid transform node position.
 - **End Position**(Float3): End transform node position.

#### Output
 - **Angle** (Float): Magnitude of the angle between the three transform nodes.
 - **Velocity** (Float): Magnitude of the angular velocity between the three transform nodes.
 - **Acceleration** (Float): Magnitude of the angular acceleration between the three transform nodes.

#### Time Attributes
 - **Start Time** (Time, *Current frame*): Determines the frame at which the playback/simulation starts.
 - **Current Time** (Time, *Current frame*): Current playback frame.

#### Scale Attributes
 - **Time Scale** (Float, 1.0): Sets the scaling factor applied to the compute the velocity or acceleration.
    - Has a range of \[0.001, 10.0\] [^1]
 - **Space Scale** (Float, 1.0): Sets the scaling factor applied to velocity or acceleration.
    - Has a range of \[0.001, 100.0\] [^1]

## Connecting sensors to deformers

Sensors are meant to be connected to a deformer so that they can automatically control deformer attributes, essentially enabling the deformer to react to external inputs from the scene.

When creating a sensor, a remap node for each output attribute is created. Through these remap nodes, and their output, it is possible to modulate and connect the information obtained by the sensor to a deformer and display its remapped value to its corresponding locator.

<figure markdown>
  ![AdnLocatorPosition within a scene](images/position_sensor_nodes.png){width=60%}
  <figcaption>Figure 4: Nodes created by an AdnSensorPosition.</figcaption>
</figure>

<figure markdown>
  ![AdnLocatorPosition within a scene](images/distance_sensor_nodes.png){width=60%}
  <figcaption>Figure 5: Nodes created by an AdnSensorDistance.</figcaption>
</figure>

<figure markdown>
  ![AdnLocatorPosition within a scene](images/rotation_sensor_nodes.png){width=60%}
  <figcaption>Figure 6: Nodes created by an AdnSensorRotation.</figcaption>
</figure>

Connecting the sensor to the target deformer can be done using the Node Editor in Maya:

<figure markdown>
  ![AdnSensorDistance connected to the activation of an AdnMuscle](images/adn_sensor_to_deformer_connect.png){width=60%}
  <figcaption>Figure 7: AdnSensorDistance connected to the activation of an AdnMuscle.</figcaption>
</figure>

However, these connections are made in a much more user friendly way by making use of the [Connection Editor](tools.md), explained in more detail in the [tools](tools.md) section.
