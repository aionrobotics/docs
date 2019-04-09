===============
Getting Started
===============

The following documentation provides example ROS stacks and usage instructions for the R1 ROS edition rovers.

The stacks provided by Aion Robotics are intended to provide a quick and easy way to learn the system as well as give developers a basis for adding their own functionality.

`AION ROBOTICS GitHub <https://github.com/aionrobotics>`_

+-----------+-------------+-------------------------------+----------+
|Repo       | Package     | Function                      | Status   |
+===========+=============+===============================+==========+
| aion_r1   | r1_control  | - Bluetooth Joystick Control  | Complete |
|           |             | - Publish Motor Driver Topics |          |
+-----------+-------------+-------------------------------+----------+

**New packages will be added to this list as they are ready for use.**

The r1_control pkg establishes a direct serial over USB connection between the TX2 and Roboclaw motor driver.

Physical control of the R1 is provided by a wireless Bluetooth Joystick controller. (Playstation, Xbox etc)

The following topics are also published for use within more advanced projects::

  /cmd_vel
  /diagnostics
  /joy
  /motors/commanded_speeds
  /motors/read_currents
  /odom
  /rosout
  /rosout_agg
  /tf

.. tip:: The R1 "ROS Package" UGV ships "ready-to-code" with all hardware & software fully configured.

First time setup
----------------

1. Connect a monitor to the TX2 Dev board.

2. Power on the R1 UGV.

3. Power on the Jetson TX2.

4. Login: ``User: nvidia`` ``Password: nvidia``

5. Connect to a local Wifi network

6. Disconnect monitor


Robot Bringup
-------------

1. Power on the R1 UGV

2. Power on the Jetson TX2

3. Open a terminal on a host computer

  3.1 ssh to the R1 over the wireless network
::

  ssh -X nvidia@<r1-ipaddress>

4. launch pkg
::
  cd /catkin_ws
  roslaunch r1_control teleop.launch

.. tip:: If "Package not found" ``source devel/setup.bash``

5. System shutdown
::

  shutdown now

.. note:: The smart battery shipped with the R1 has a low current cutoff feature. To maintain minimum current requirements, both motor driver and TX2 must be powered on.

Tools
-----

Open a new terminal

- To view topics:
::

  rostopic list


- To view topic output:
::

  rostopic echo <topic_name>


- To visualize nodes/topics:
::

  rqt_graph

.. tip:: To use rqt_graph remotely, you must first export the TX2 display to your remote machine.

To do so:
::

  export DISPLAY=:10

Complete list of tools [HERE]

To learn more about how the package works please check `[HERE] <http://docs.aionrobotics.com/en/latest/ros-robot-configuration.html#>`_
