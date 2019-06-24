=========
Operation
=========

1.	Booting The System
----------------------

  1.1.	Turn on the Transmitter

  1.2.	Power on the aircraft by plugging in both batteries.

  .. note:: Upon booting, the aircraft will attempt to acquire a GPS fix. When a fix is achieved, the vehicle marks its location as “Home” as can be seen in the “FLIGHT PLAN” tab in your GCS. **This is the location the aircraft will attempt to RTL** (If desired, you can move this position manually using the GCS)

  1.3. Ensure the aircraft is not disturbed during the IMU calibration procedure. (Rapid RED/BLUE flashing LED)

  1.4.	Boot is complete when the Autopilot tones and vehicle achieves GPS lock. (Flashing GREEN LED)

.. tip::	The vehicle boots with safety switch disabled. (Transmitter input is ignored)

2.	Connecting to the Aircraft
------------------------------

  2.1.	On the device Mission Planner is installed on, go to your wireless settings and look for the aircrafts wireless ID.

SSID: ``AIONio-XXXX``

Password: ``aionrobotics``

  2.2.	Open Mission Planner, select UDP in the upper right hand corner and click “Connect”.

  2.3.  Choose port `14558`.

  2.3.	The GCS and Autopilot module will establish a connection.

3. Avoidance
------------

.. warning:: Colision avoidance is active in **LOITER** flight mode only.

The Q-775 Spyder is equipped with a RealSense D435i 3D Depth sensor and configured to avoid objects at a distance of **5 meters**.

.. warning:: The sensor is highly sensitive to changing light conditions. This can cause anomalies such as false positives and missed objects. Users should manunally test its sensitivity under varying conditions and never adopt a sense of false security.

- Tall grass or objects within the 5 meter detection zone will prevent the aircraft from arming.

To change parameters, go to Mission Planners **CONFIG/TUNING** screen, select **"Full Parameter Tree"** and search for the below parameters.

+----------------------+--------------+----------------+
| ArduPilot Parameter  | Setting      | Function       |
+======================+==============+================+
| AVOID_ENABLE         | 0            | Disabled       |
+----------------------+--------------+----------------+
| AVOID_ENABLE         | 3            | Enabled        |
+----------------------+--------------+----------------+
| AVOID_BEHAVE         | 0            | Slide          |
+----------------------+--------------+----------------+
| AVOID_BEHAVE         | 1            | Stop           |
+----------------------+--------------+----------------+
| AVOID_MARGIN         | 0-10         | Meters         |
+----------------------+--------------+----------------+

After changing a parameter, you must select **"Write"** to save the parameter to the autopilot.

.. tip:: To visualize the detection zone in Mission Planner press `Cntrl-F` and select `Proximity`.


4. Manual Takeoff
-----------------

.. warning:: To ensure stable operation, do not fly near tree’s or tall structures that can block the vehicles line of sight to GPS satellites.

.. warning:: Do not fly near ferrous objects that can cause magnetic interference.

.. warning:: Never change vehicle parameters unless you are fully aware of their function and consequences!

.. tip:: In case of sudden irratic or unintended behavior, always be prepared to change the flight mode to **ALTIDUDE HOLD** and manually take control of the aircraft. This mode does not rely on GPS or the onboard Compass.

  4.1 Always perform a `[Pre-Flight Check] <https://docs.aionrobotics.com/en/dev/q-775-spyder-pre-flight-checklist.html>`_

  4.2 Put the aircraft in `LOITER` flight moode.

  4.3  To arm the aircraft, hold the left control stick fully down and to the right.

.. tip:: If the aircraft will not arm please see: `[Understanding ArduPilot mandatory onboard pre-arm safety checks] <http://ardupilot.org/copter/docs/prearm_safety_check.html>`_

  4.4 The aircraft will arm and props will start spinning.

  4.5 To take off, quickly raise the throttle and release when the aircraft reaches desired elevation.

  4.6 Move SWD to the down position to raise landing gear.

.. tip:: The highest risk of a crash is just before and after takeoff, when in close proximity to the ground.


5. Manual Landing
-----------------

 5.1 **Slowly and softly land the aircraft on level ground making sure to prevent lateral movement as it touches down.**

 5.2 As the aircraft makes contact with the ground, quickly move the throttle all the way down and to the right until it disarms and the props come to a stop.

 6. Auto Takeoff
 ---------------

 .. warning:: To ensure stable operation, do not fly near tree’s or tall structures that can block the vehicles line of sight to GPS satellites.

 .. warning:: Do not fly near ferrous objects that can cause magnetic interference.

 .. warning:: **Never** change vehicle parameters unless you are fully aware of their function and consequences!

 .. tip:: In case of sudden irratic or unintended behavior, always be prepared to change the flight mode to **ALTIDUDE HOLD** and manually take control of the aircraft. This mode does not rely on GPS or the onboard Compass.



   6.1 Always perform a `[Pre-Flight Check] <https://docs.aionrobotics.com/en/dev/q-775-spyder-pre-flight-checklist.html>`_

   6.2 Create a waypoint mission using Mission Planner. `[For detailed info see here] <http://ardupilot.org/copter/docs/common-mission-planning.html>`_

   6.3 **Write** the waypoints to the vehicle.

   6.4 Select **"Read Waypoints"** to verify the mission uploaded successfully.

   6.5 When you switch the aircraft into `AUTO` flight mode, the vehicle will Arm itself, take off and proceed with the mission.

.. tip:: You can change flight modes at any time during an Auto mission to regain control of the aircraft.

7. Auto Landing
---------------

 7.1 If configured to do so within your mission, the aircraft will land itself at the location you specified.


8.	Advanced Software Control
-----------------------------

You can SSH to access the onboard computer:

``ssh -X aion@10.0.1.128``

User: ``aion``

Password: ``aion``

See `AIONio <https://docs.aionrobotics.com/en/dev/aionio.html#getting-started>`_ for detailed documentation.
