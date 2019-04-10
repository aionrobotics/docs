======
AIONio
======

Getting Started
---------------

`AIONio <https://github.com/aionrobotics/aion_io_dev>`_ is a complete system image that enables seamless advanced control of AION ROBOTICS companion computer equipped vehicles.

+-----------------------+-------------------------------------+
| Companion Computer:   |  Recommended Use:                   |
+=======================+=====================================+
| Jetson TX2            | High performance edge computing     |
+-----------------------+-------------------------------------+
| Jetson Xavier         | Ultimate performance edge computing |
+-----------------------+-------------------------------------+

:doc:`Jetson Hardware Info <../companion-computer>`

AIONio provides developers with the base tools and networking interfaces required to efficiently develop their own advanced projcects.

**Included:**

- Full Ubuntu Operating System
- ROS installation
- AIONio ROS control package
- MavROS - MAVlink communication node
- Telemetry and Message routing between Autopilot, Companion and remote Computers. (Serial/UDP/TCP)
- Networking support for:

  - WLAN - WiFi
  - LAN - Ethernet, p2p, LTE
  - Serial

- H264 video streaming
- NVIDIA Jetpack

ROS Packages
------------

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

*Add on packages are available for purchase from AION ROBOTICS*

Calibrate Autopilot
-------------------

UGV Instructions `[HERE] <http://docs.aionrobotics.com/en/latest/ardupilot-mandatory-hardware-setup.html#>`_

The calibration example is provided using Mission Planner Ground Control Station
`[HERE] <http://ardupilot.org/planner/>`_

Vehicle Bringup
---------------

1. Power on the vehicle

2. Connect to the WiFi network with a host computer.

.. tip:: The name of the network is ``AIONio-`` plus the last four hexadecimal digits of the vehicles unique mac address. For example: ``AIONio-c71a``

3. The default passphrase to connect to the network is ``aionrobotics``

4. Open a terminal and ssh to the UGV over wireless network:
::

  ssh -X aion@10.0.1.128

**Username** ``aion``

**Password** ``aion``

5. launch AIONio:
::
  cd ~/AIONio_ws
  roslaunch aion_control aion_io.launch

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

7. Follow the appropriate vehicle control guide below.

UGV Control
-----------

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


Copter Control
--------------

.. warning:: ROS control of UAS is for advanced users only. Serious risk of injury or property damage! Read these instructions in full several times before attempting to execute in real life. Safe operation is the responsibility of the user.

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


Running ROS remotely
--------------------

AION ROBOTICS vehicles ship with ROS networking configured as Master. You can run ROS nodes and programs such as `rviz <http://wiki.ros.org/rviz>`_ on a remote computer by installing ROS and configuring it to use the vehicle as Master.

To point the remote computer to the vehicle (ROS Master) add the following lines to its ``.bashrc`` file:
::
    export ROS_MASTER_URI=http://IP_OF_VEHICLE:11311
    export ROS_HOSTNAME=IP_OF_THIS_COMPUTER

If you are using Ubuntu, you can substitute ``IP_OF_VEHICLE`` with the hostname of your vehicle. The hostname is the same as the WiFi network name followed by ``.local``.

Following our previous example above, the hostname would be ``AIONio-c71a.local``. Otherwise, you will substitute this with the actual IP address of the vehicle.

Likewise if using Ubuntu, you may substitute ``IP_OF_THIS_COMPUTER`` with your computers hostname followed by ``.local`` or again, with the computers IP address.

For more detailed information or troubleshooting tips on configuring ROS networking look at the `ROS Documentation <http://wiki.ros.org/turtlebot/Tutorials/indigo/Network%20Configuration>`_

Video Streaming
---------------
Video streaming is *enabled* by default.

- To use this feature, simply plug in a `USB Camera <https://www.amazon.com/Logitech-Widescreen-Calling-Recording-Desktop/dp/B006JH8T3S>`_ and it will automatically start an H264 UDP stream to port ``5600``

.. tip:: To access the control panel, type ``10.0.1.128:8000`` into a connected devices web browser.
