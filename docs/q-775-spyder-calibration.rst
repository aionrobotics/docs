
.. caution:: The Q-775 Spyder aircraft comes pre-calibrated from AION ROBOTICS. Should you ever need to recalibrate the aircraft or transmitter, follow the instructions below.

1.	Transmitter Calibration
---------------------------

  1.1.	Turn on Transmitter

  1.2.	Power on the R1 and connect to the GCS via wireless telemetry link.

  1.3.	Select the **“FLIGHT DATA”** tab and look in the HUD to ensure the safety switch is ON (or RED flashing Safety LED)

  1.4.	Select **“INITIAL SETUP”** tab

  1.5.	Select **“Mandatory Hardware”**

  1.6.	Select **“Radio Calibration”**

  1.7.	Select **“Calibrate Radio”** and follow instructions

.. tip:: Don’t forget to toggle your Fly Modes and Aux. Button to verify proper function.
..

  1.8.	Select the **“FLIGHT MODES”** tab and toggle **“Fly Mode 1 - Manual, 2 – Steer and 3 – Auto”**. The corresponding mode should turn green upon activation.

2.	Accel Calibration
---------------------
  2.1.	Select **“Accel Calibration”** under the “INITIAL SETUP -> Mandatory Hardware” tabs.

  2.2.	Select **“Calibrate Accel”** and follow instructions

3.	Compass Calibration
-----------------------
  3.1.	Select **“Compass”** under the **“INITIAL SETUP -> Mandatory Hardware”** tabs.

  3.2.	Find an outdoor area, clear of power lines and ferrous objects that will cause magnetic interference. (This includes metallic objects on your person)

  3.3.	Select “Start” in the “Onboard Mag Calibration” window and you will hear the Autopilot beep to signal calibration has started.

  3.4.	To begin calibration, you must pick the aircraft up and spin it 360 degrees around each axis until the green bar next to each mag is full and the GCS alerts you of a successful calibration.


.. tabularcolumns:: |c|c|c|

+--------------------+-------------+
|Chassis Orientation | Rotate      |
+====================+=============+
| Level, Right side up   | 360 Degrees |
+--------------------+-------------+
| Left Side Up       | 360 Degrees |
+--------------------+-------------+
| Right Side Up      | 360 Degrees |
+--------------------+-------------+
|Front Up            | 360 Degrees |
+--------------------+-------------+
|Front Down          | 360 Degrees |
+--------------------+-------------+
|Level, Inverted     | 360 Degrees |
+--------------------+-------------+

.. tip:: A high pitched noise from the aircraft followed by discontinued beeping and GCS confirmation mark completion of calibration. A deep tone, followed by continued calibration beeps marks calibration failure, repeat spinning on each axis.
