======
AIONio
======

Getting Started
---------------

`AIONio <https://github.com/aionrobotics/aion_navigator>`_ is a base software package for controlling AION ROBOTICS vehicles using ROS.

This stack is intended to provide developers with the base control and communication scheme required for adding their own advanced functionality.

Add on packages are available through AION ROBOTICS.

+----------------+-------------------+----------------------------------------------------------+------------+
|Repo            | Package           | Function                                                 |   Status   |
+================+===================+==========================================================+============+
|   aion_io      | aion_control      | - Control vehicle using cmd_vel messages                 | Complete   |
|                |                   | - Publish Autopilot sensors as ROS topics                |            |
|                |                   |                                                          |            |
+----------------+-------------------+----------------------------------------------------------+------------+
|   aion_io      | aion_descriptions | - Vehicle URDFs and Mesh Files                           | Complete   |
+----------------+-------------------+----------------------------------------------------------+------------+
|   aion_io      | aion_simulator    | - Gazebo Config and launch files                         |            |
|                |                   | - Simple Teleop node for using a playstation Controller  |  Complete  |
|                |                   |                                                          |            |
+----------------+-------------------+----------------------------------------------------------+------------+

`AION ROBOTICS GitHub <https://github.com/aionrobotics>`_


Calibrate Autopilot
-------------------

UGV Instructions `[HERE] <http://docs.aionrobotics.com/en/latest/ardupilot-mandatory-hardware-setup.html#>`_

The calibration example is provided using Mission Planner Ground Control Station
`[HERE] <http://ardupilot.org/planner/>`_

Vehicle Bringup
---------------

1. Power on the vehicle

2. Connect to the wi-fi network with a host computer.

.. tip:: The name of the network is ``AIONio-`` plus the last four hexadecimal digits of the vehicles unique mac address. For example: ``AIONio-c71a``

3. The default passphrase to connect to the network is ``aionrobotics``

4. Open a terminal and ssh to the UGV over wireless network:
::

  ssh -X aion@10.0.1.128

:Username: aion
:Password: aion

5. launch AIONio:
::
  cd ~/AIONio_ws
  roslaunch aion_control aion_io.launch

.. tip:: If you see the error "Package not found" type the following: ``source devel/setup.bash``

6. Verify Autopilot sensors are streaming to ROS:

- To view GPS location:
  ::

    rostopic echo /mavros/global_position/global

- To view a list of all ROS topics:
::

  rostopic list

- To view the output of any topic:
::

  rostopic echo <topic_name>

7. Follow appropriate vehicle operation guide below. 

UGV Operation
-------------

1. Arm the vehicle:
::
    rosrun mavros mavsafety arm

.. note:: Vehicle must have a GPS lock to arm in autonomous modes. Documentation for GPS denied/indoor navigation coming soon.

.. tip:: You can also Arm using an RC transmitter or GCS such as AION ROBOTICS C3, Mission Planner etc. For instructions see vehicle specific documentation.

2. Change vehicle mode:
::
    rosrun mavros mavsys mode -c GUIDED

+----------------+---------------------------------------------------+
|Control Mode    |  Function                                         |
+================+===================================================+
| MANUAL         | - Manual control of the vehicle                   |
|                |                                                   |
+----------------+---------------------------------------------------+
|   AUTO         |  - Begin ArduPilot Point-N-Click waypoint mission |
|                |                                                   |
+----------------+---------------------------------------------------+
| GUIDED         | - ROS control of Autopilot                        |
|                |                                                   |
+----------------+---------------------------------------------------+

For full MavROS documentation see `[HERE] <http://wiki.ros.org/mavros>`_

3. To move the vehicle, we must publish  ``cmd_vel`` messages. Open another terminal, connect to the vehicle and launch rqt:
::
    rqt

5. Add topic to publisher:

``/mavros/setpoint_velocity/cmd_vel``

``geometry_msgs/Twist``

``cmd_vel``

11. Under the rqt "Plugins" tab, select "Publishers>Robot Steering"

.. warning:: UGV will move when you output ``cmd_vel``! Be ready to hit stop!

.. note:: This example control tool works by publishing ``cmd_vel`` messages which MavROS is subscribed to. ``cmd_vel`` messages are used to physically control the UGV in the real world and serve as the base for you to build advanced integrations from.


Copter Operation
----------------

.. warning:: ROS control of UAS is for advanced users only. Read these instructions in full several times before attempting to execute in real life. Safe operation is the responsibility of the user. Serious risk of injury or property damage.

1. Change aircraft mode:
::
    rosrun mavros mavsys mode -c GUIDED

+--------------+-----------------------------------------+
| Control Mode | Function                                |
+==============+=========================================+
| LOITER       | - GPS/Alt stabilized manual flight      |
+--------------+-----------------------------------------+
| RTL          | - Return to location when first Armed   |
+--------------+-----------------------------------------+
| GUIDED       | - ROS control of Autopilot              |
+--------------+-----------------------------------------+
| LAND         | - Lands the aircraft                    |
+--------------+-----------------------------------------+

For full MavROS documentation see `[HERE] <http://wiki.ros.org/mavros>`_

2. To control the vehicle while in flight, we must publish  ``cmd_vel`` messages. Open another terminal, connect to the vehicle and launch rqt
::
    rqt

3. Add topic to publisher:

``/mavros/setpoint_velocity/cmd_vel``

``geometry_msgs/Twist``

``cmd_vel``

4. Under the rqt "Plugins" tab, select "Publishers>Robot Steering".

.. note:: This example control tool works by publishing ``cmd_vel`` messages which MavROS is subscribed to. ``cmd_vel`` messages are used to physically control the UGV in the real world and serve as the base for you to build advanced integrations from. You will use this tool to move the aircraft in flight.

.. warning:: PROPS WILL BEGIN SPINNING WHEN ARMED!

5. Return to the first terminal to Arm the vehicle:
::
    rosrun mavros mavsafety arm

.. warning:: PROPS WILL BEGIN SPINNING WHEN ARMED!

.. note:: Vehicle must have a GPS lock to arm. Documentation for GPS denied/indoor navigation coming soon.

.. tip:: You can also Arm using an RC transmitter or GCS such as AION ROBOTICS C3, Mission Planner etc. For instructions see vehicle specific documentation.

6. To take off:
::
    rosrun mavros mavcmd takeoff

You will use the "Robot Steering" sliders to move vehicle during flight.

.. warning:: Vehicle will move when you output ``cmd_vel``! Be ready to return slider to zero position to stop! This is a primitive control example only and should NOT be used for normal operation.

7. To land:
::
    rosrun mavros mavcmd land


Useful Tools
------------

- To visualize all active nodes/topics:
::

  rqt_graph

.. tip:: To use rqt_graph remotely without setting up ROS networking, you may want to export the TX2 display to your remote machine.

To do so:
::

  export DISPLAY=:10

Complete list of ROS tools `[HERE] <http://wiki.ros.org/Tools>`_


Running ROS nodes on a remote computer
--------------------------------------

AION ROBOTICS vehicles ship with ROS networking configured as Master. You can run ROS nodes and programs on a remote computer by setting up the remote computer to use the vehicle as master.

To point the remote computer to the vehicle (ROS master) add the follwing lines to your ``.bashrc`` file:
::
    export ROS_MASTER_URI=http://IP_OF_ROVER:11311
    export ROS_HOSTNAME=IP_OF_THIS_COMPUTER

If you are using Ubuntu, you can substitute ``IP_OF_ROVER`` by the hostname of your rover. The hostname is the same as the Wi-Fi network name followed by ``.local``, following our previous example the hostname would be ``AIONio-c71a.local``. Otherwise you will need to substitute it by the actual IP address of the rover.

Likewise if using Ubuntu, you may substitute ``IP_OF_THIS_COMPUTER`` by your computers hostname followed by ``.local`` or by the computers IP address.

For more detailed information or troubleshooting tips on configuring ROS networking look at the `[ROS Documentation] <http://wiki.ros.org/turtlebot/Tutorials/indigo/Network%20Configuration>`_
