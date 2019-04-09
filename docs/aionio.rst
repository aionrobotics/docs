======
AIONio
======

`[AIONio] <https://github.com/aionrobotics/aion_navigator>`_ is a base software package for controlling AION ROBOTICS vehicles using ROS.

+----------------+----------------------------------------------+
|Control Mode    |  Function                                    |
+================+==============================================+
| MANUAL         | - Manual control of the vehicle              |
|                |                                              |
+----------------+----------------------------------------------+
|   AUTO         |  - ArduPilot Point-N-Click Waypoint Missions |
|                |                                              |
+----------------+----------------------------------------------+
| GUIDED         | - ROS slave control of Autopilot             |
|                |                                              |
+----------------+----------------------------------------------+

This stack is intended to provide developers with a base control and communication scheme required for adding their own advanced functionality.

Add on packages are also available through AION ROBOTICS.

`AION ROBOTICS GitHub <https://github.com/aionrobotics>`_

+----------------+-------------------+-----------------------------------------------+------------+
|Repo            | Package           | Function                                      |   Status   |
+================+===================+===============================================+============+
|   aion_io      | aion_control      | - Control vehicle using cmd_vel messages      | Complete   |
|                |                   | - Publish Autopilot sensors as ROS topics     |            |
|                |                   |                                               |            |
+----------------+-------------------+-----------------------------------------------+------------+
|                | aion_descriptions | - Vehicle URDFs and Mesh Files                | Complete   |
+----------------+-------------------+-----------------------------------------------+------------+
|                | aion_simulator    | - Gazebo Config and launch files              |            |
|                |                   | - Simple Teleop node for using a playstation  |  Complete  |
|                |                   |    controller                                 |            |
+----------------+-------------------+-----------------------------------------------+------------+


For a full list of MavROS topics published see `[HERE] <http://wiki.ros.org/mavros>`_


.. tip:: AIONio equipped vehicle packages ship Ready-to-Code with all hardware & software fully configured.


Getting Started - Calibrate the Autopilot
-----------------------------------------

See instructions `[HERE] <http://docs.aionrobotics.com/en/latest/ardupilot-mandatory-hardware-setup.html#>`_

The calibration example is provided using Mission Planner Ground Control Station
`[HERE] <http://ardupilot.org/planner/>`_

Vehicle Bringup
---------------

1. Power on the vehicle

2. Connect to the wi-fi network with a host computer.

.. tip:: The name of the network is ``AIONio-`` plus the last four hexadecimal digits of the companion computers unique mac address. For example: ``AIONio-c71a``

3. The default passphrase to connect to the network is ``aionrobotics``

4. Open a terminal and ssh to the UGV over wireless network using ``aion`` as the username and password
::

  ssh -X aion@10.0.1.128

5. launch ROS
::
  cd ~/AIONio_ws
  roslaunch aion_control aion_io.launch

.. tip:: If you get an error "Package not found" type the following: ``source devel/setup.bash``

6. Arm the vehicle:
::
    arm throttle

.. note:: Vehicle must have a GPS lock. Documentation for GPS denied/indoor navigation coming soon.

.. tip:: You can also Arm using the RC transmitter or a GCS such as AION ROBOTICS C3, Mission Planner etc.

7. Change the vehicles mode to ``GUIDED`` using the transmitter or a GCS.

8. Verify that the vehicle is in guided mode by checking GPS LED status.


9. To test if ROS is now controlling the vehicle, publish the ``cmd_vel`` topic, to do so open another terminal, connect to the vehicle and launch rqt
::
    rqt

10. Add topic to publisher

``/mavros/setpoint_velocity/cmd_vel``

``geometry_msgs/Twist``

``cmd_vel``

11. Under the rqt "Plugins" tab, select "Publishers>Robot Steering"

.. warning:: UGV will move when you output ``cmd_vel``! Be ready to hit stop!

.. note:: This example control tool works by publishing ``cmd_vel`` messages which MavROS is subscribed to. ``cmd_vel`` messages are used to physically control the UGV in the real world and serve as the base for you to build advanced integrations from.

12. System shutdown - simply power off the UGV.

Advanced uses
-------------

For more advanced configuratons of ROS, take a look at the `[Ardupilot Wiki] <http://ardupilot.org/dev/docs/ros.html>`_

A second launch file called ``apm_cartographer.launch`` is provided for launching the ardupilot implementation of cartographer. For more information visit this `[WIKI PAGE] <http://ardupilot.org/dev/docs/ros-cartographer-slam.html>`_

Running ROS nodes on a remote computer
--------------------------------------

The rover ships with its ROS networking setup configured so that it acts as the ROS Master. You can run ROS nodes and programs on a remote computer by setting up the remote computer to use the rover as a ROS master.

In order for the remote computer to know where the ROS master is, you need to add the follwing lines to your ``.bashrc`` file:
::
    export ROS_MASTER_URI=http://IP_OF_ROVER:11311
    export ROS_HOSTNAME=IP_OF_THIS_COMPUTER

If you are using Ubuntu, you can substitute ``IP_OF_ROVER`` by the hostname of your rover. The hostname is the same as the Wi-Fi network name followed by ``.local``, following our previous example the hostname would be ``AIONio-c71a.local``. Otherwise you will need to substitute it by the actual IP address of the rover.

Likewise if using Ubuntu, you may substitute ``IP_OF_THIS_COMPUTER`` by your computers hostname followed by ``.local`` or by the computers IP address.

For more detailed information or troubleshooting tips on configuring ROS networking look at the `[ROS Documentation] <http://wiki.ros.org/turtlebot/Tutorials/indigo/Network%20Configuration>`_

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

.. tip:: To use rqt_graph remotely without setting up ROS networking, you may want to export the TX2 display to your remote machine.

To do so:
::

  export DISPLAY=:10

Complete list of ROS tools `[HERE] <http://wiki.ros.org/Tools>`_

To learn more about how this package works please check `[HERE] <http://docs.aionrobotics.com/en/latest/arduros-robot-configuration.html#>`_
