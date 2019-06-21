=========
Operation
=========

.. note:: Upon booting the aircraft, it will attempt to acquire a satellite lock as well as check Compass & EKF health.

.. note:: When satellite lock is achieved, the vehicle marks its location as “Home” as can be seen in the “FLIGHT PLAN” tab in your GCS. **This is the location the aircraft will attempt to RTL** (This can be moved manually if desired)

.. warning:: To ensure stable operation, do not fly near tree’s or tall buildings/structures that can block the vehicles line of sight to satellites. Do not fly near ferrous objects that can cause magnetic interference.

.. warning:: Never change vehicle parameters unless you are fully aware of their function and consequences!

1.	Booting The System
----------------------

  1.1.	Turn on the Transmitter

  1.2.	Power on the aircraft by plugging in both batteries.

  1.3. Ensure the aircraft is not disturbed during the IMU calibration procedure. (Rapid RED/BLUE flashing LED)

  1.4.	Boot is complete when the Autopilot tones and vehicle achieves GPS lock. (Flashing GREEN LED)

.. tip::	The system boots with safety switch disabled. (Transmitter input is ignored)

2.	Connecting to the Aircraft
------------------------------

  2.1.	On the device Mission Planner is installed on, go to your wireless settings and look for the aircrafts wireless ID.

SSID: ``AIONio-XXXX``

Password: ``aionrobotics``

  2.2.	Open Mission Planner, select UDP in the upper right hand corner and click “Connect”

  2.3.  Choose port `15668`

  2.3.	The GCS and Autopilot module will establish a connection.

3. Arming the vehicle
---------------------

  1.1 Always perform a `[Pre-Flight Check] <https://github.com/ArduPilot/ardupilot/blob/master/Tools/Frame_params/AION_R1_Rover.param>`_ 

3.	Advanced Software Control
-----------------------------

You can SSH to access the onboard computer:

``ssh -X aion@10.0.1.128``

User: ``aion``

Password: ``aion``

See `AIONio <https://docs.aionrobotics.com/en/dev/aionio.html#getting-started>`_ for detailed documentation.
