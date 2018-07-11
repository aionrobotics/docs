===============
Getting Started
===============

The following documentation provides example ArduROS stack and usage instructions for the R1 ArduROS edition UGV.

The stack provided by Aion Robotics is intended to provide a quick and easy way to learn the system as well as give developers a basis for adding their own functionality.

`AION ROBOTICS GitHub <https://github.com/aionrobotics>`_

+-----------+-------------+------------------------------------+----------+
|Repo       | Package     | Function                           | Status   |
+===========+=============+====================================+==========+
| aion_r1   | r1_control  | - Control Autopilot using cmd_vel  | Complete |
|           |             | - Publish MavROS topics for        |          |
|           |             | Autopilot sensors.                 |          |
+-----------+-------------+------------------------------------+----------+

**New packages will be added to this list as they are ready for use.**

Expanding on all the excellent features of a stand alone Autopilot, the r1_control pkg uses MavROS to allow for highly advanced slave control of the Autopilot. To enable this on the Autopilot side, it must be Armed, saftey off and switched into "Guideed Mode".

Physical manual control of the UGV is provided via manual RC style TX by simply switching back to "Manual Mode".

For a full list of topics go `[HERE] <http://wiki.ros.org/mavros>`_


.. tip:: The R1 "ArduROS Package" UGV ships "ready-to-code" with all hardware & software fully configured.


Robot Bringup
-------------

1. Power on the R1 UGV

.. note:: The smart battery shipped with the R1 has a low current cutoff feature. To maintain minimum current requirements, the TX2 power harness must be connected.

2. Use a host computer to connect to the AION_UGV wireless network

3. Open a terminal and ssh to the UGV over wireless network
::

  ssh -X apsync@10.0.1.128

4. launch pkg
::
  cd /catkin_ws
  roslaunch r1_control apm.launch

.. note:: UGV must have GPS lock. Documentation for GPS denied/indoor use coming soon.

.. tip:: If "Package not found" ``source devel/setup.bash``

5. Open another terminal and launch MavProxy
  ::
    mavproxy.py --mav10 --master :14550 --source-system=89

.. tip:: Allow roughly 30 seconds or so for parameters to download

6. Disable safety switch
  ::
    arm safetyoff

7. Change Autopilot mode
  ::
    mode guided

8. Open another terminal and launch rqt
  ::
    rqt

9. Add topic to publisher

``/mavros/setpoint_velocity/cmd_vel``

``geometry_msgs/Twist``

``cmd_vel``

10. Under the rqt "Plugins" tab, select "Publishers>Robot Steering"

.. note:: This primitive control tool simply publishes cmd_vel messages which MavROS is subscribed to. cmd_vel messages physically control the UGV in the real world and serve as the base for you to build advanced integrations from.

11. System shutdown - simply power off the UGV.


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

Complete list of tools `[HERE] <http://wiki.ros.org/Tools>`_

To learn more about how the package works please check `[HERE] <http://docs.aionrobotics.com/en/latest/arduros-robot-configuration.html#>`_
