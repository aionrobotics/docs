===============
Getting Started
===============

The following documentation provides an example ROS stack and usage instructions for the R1 ArduROS edition UGV with our AIONio Software package.

The stack provided by AION ROBOTICS is intended to provide a quick and easy way to learn the basics as well as give developers a basis for adding their own functionality.

`AION ROBOTICS GitHub <https://github.com/aionrobotics>`_

+----------------+---------------+-----------------------------------------------+------------+
|Repo            | Package       | Function                                      |   Status   |
+================+===============+===============================================+============+
|   aion_r1      | r1_control    | - Control Autopilot using cmd_vel             | Deprecated |
|                |               | - Publish MavROS topics for Autopilot sensors |            |
|                |               |                                               |            |
+----------------+---------------+-----------------------------------------------+------------+
| r1_ugv_sim     | r1_description| - URDFs and Mesh Files                        |  Complete  |
|                | r1_gazebo     | - Gazebo Config and launch files              |  Complete  |
|                | r1_teleop     | - Simple Teleop node for using an Xbox        |  Untested  |
|                |               |                                               |            |
+----------------+---------------+-----------------------------------------------+------------+
| aion_navigator | aion_navigator| - Basic launch file for MAVROS node           |  Complete  |
|                |               | - Ardupilot Google Cartographer launch file   |            |
|                |               |                                               |            |
+----------------+---------------+-----------------------------------------------+------------+



**New packages will be added to this list as they are ready for use.**

Expanding on all the excellent waypoint based navigational features of a stand alone Autopilot, the `[aion_navigator] <https://github.com/aionrobotics/aion_navigator>`_ pkg uses MavROS to allow for highly advanced "slave" control of the Autopilot by simply switching modes. To enable this on the Autopilot side, it must be Armed, safety off and switched into "Guided Mode".

Manual control of the UGV is provided via RC style TX by switching back to "Manual Mode". Quick and easy, waypoint based mission planning is accomplished by switching to "Auto" mode and using Ardupilot's missions previously planned and uploaded to the autopilot.

For a full list of MavROS topics see `[HERE] <http://wiki.ros.org/mavros>`_


.. tip:: The R1 "ArduROS Package" UGV ships "ready-to-code" with all hardware & software fully configured.


Calibrate the Autopilot
-----------------------

See instructions `[HERE] <http://docs.aionrobotics.com/en/latest/ardupilot-mandatory-hardware-setup.html#>`_

The calibration example is provided using Mission Planner Ground Control Station
`[HERE] <http://ardupilot.org/planner/>`_

Robot Bringup
-------------

1. Power on the R1 UGV

.. note:: The smart battery shipped with the R1 has a low current cutoff feature. To maintain minimum current requirements, the TX2 power harness must be connected.

2. Use a host computer to connect to the wireless network, the name of the network is composed of "AIONio-" and the last four hexadecimal digits of the companion computers mac address. So for example "AIONio-c71a"

3. The default passphrase to connect to the wi-fi network is "aionrobotics"

4. Open a terminal and ssh to the UGV over wireless network using "aion" as the username and password
::

  ssh -X aion@10.0.1.128

5. launch ROS using the provided launch file (early versions of the image shipped with a catkin workspace named AionR1_ws, later versions use AIONio_ws)
::
  cd ~/AionR1_ws or cd ~/AIONio_ws
  roslaunch aion_navigator apm.launch

.. note:: UGV must have a GPS lock. Documentation for GPS denied/indoor navigation coming soon.

.. tip:: If you get an error "Package not found" type the following: ``source devel/setup.bash``

6. Arm the rover either by using the RC transmitter switch, or using a GCS like mission planner or mavproxy.
::
    arm throttle

7. Change Autopilot mode using the transmitter or using a GCS to Guided Mode

8. Verify that the rover is in guided mode by checking the reported mode to the GCS or by trying to move the rover with the RC transmitter (The rover will not move with the transmitter if it is in Guided Mode)

9. To test if ROS is now controlling the rover, publish the ``cmd_vel`` topic, to do so open another terminal, connect to the rover and launch rqt
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
