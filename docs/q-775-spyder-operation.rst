=========
Operation
=========

.. note:: Upon booting the aircraft, it will attempt to acquire a satellite lock as well as check magnetic health. When satellite lock is achieved, it marks its location as “Home” as can be seen in the “FLIGHT PLAN” tab in your GCS. **This is the location the aircraft will attempt to RTL** (This can be moved manually)

.. tip:: To ensure stable operation, do not fly near tree’s or tall buildings/structures that can block line of sight between the GPS receiver and satellites, nor fly near ferrous objects that can cause magnetic interference.

1.	Booting The System
----------------------

  1.1.	Turn on the Transmitter

  1.2.	Power on the aircraft by plugging in both batteries.

  1.3. Ensure the aircraft is not disturbed during the IMU calibration procedure. (Rapid RED/BLUE flashing LED)

  1.4.	Boot is complete when the Autopilot tones and vehicle achieves GPS lock. (Signaled by flashing GREEN Status LED)

.. tip::	The system boots with safety switch disabled. (Transmitter input is ignored)

2.	Connecting to the Aircraft
------------------------------

  2.1.	On the device your GCS is installed on, go to your wireless settings and look for the aircrafts wireless ID.

SSID: ``AIONio-XXXX``

Password: ``aionrobotics``

  2.2.	Open Mission Planner, select UDP in the upper right hand corner and click “Connect”

  2.3.  Choose port `15668`

  2.3.	The GCS and Autopilot module will establish a connection.

.. tip:: You can also connect to the vehicle directly from an internet browser via APweb. To do so, type: 10.0.1.128 into your browser address bar. (Limited functionality)
..

3.	Advanced Software Control
-----------------------------

You can SSH to access the onboard computer:

``ssh -X aion@10.0.1.128``

User: ``aion``

Password: ``aion``

See `AIONio <https://docs.aionrobotics.com/en/dev/aionio.html#getting-started>`_ for detailed documentation.
