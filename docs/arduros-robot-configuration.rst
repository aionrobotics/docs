=====================
ArduROS Configuration
=====================

.. note:: The R1 "ArduROS Package" ships "ready-to-code" with all hardware & software fully configured. The information provided below is for troubleshooting, educational or R1 upgrade purposes.

Jetson TX2 Requirements:
------------------------

1. The following prerequisites must be installed/setup on NVIDIA Jetson TX2

  [x] NVIDIA Jetpack 3.2.1

Build APSync on the TX2
-------------------------
Directions`[HERE] <https://github.com/aionrobotics/apsync>`_

When the UGV boots, a Wifi Access Point is created:

SSID: ``AION_UGV``

Password: ``aionrobotics``

User: ``apsync``

Password: ``apsync``

``ssh -X apsync@10.0.1.128``

Install ROS on the TX2
----------------------
Directions`[HERE] <http://wiki.ros.org/kinetic/Installation/Ubuntu>`_


Install dependencies:
---------------------
::

  sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool python-catkin-tools build-essential -y


To install specific ROS pkgs:
::

  sudo apt-get install ros-kinetic-PACKAGE

Pkgs:

::

  serial
  mavros
  rqt
  rqt-common-plugins
  rqt-robot-plugins
  navigation
  xacro
  robot-state-publisher
  joint-state-controller
  diff-drive-controller
  robot-localization
  twist-mux
  interactive-market-twist-server
  opencv-apps
  gazebo-ros
  gmapping
  joy
  diagnostic-aggregator
  teleop-twist-keyboard
  teleop-twist-joy
  image-transport
  joint-trajectory-controller
  joint-limits-interface
  controller-manager
  razor-imu-9dof
  imu-transformer


Run Geographic Lib script
-------------------------

Move to the ``/opt/ros/kinetic/lib/mavros`` directory

::

  sudo ./install_geographiclib_datasets.sh

Configure Autopilot:
--------------------

Detailed Setup`[HERE] <http://docs.aionrobotics.com/en/latest/ardupilot-package.html>`_

Parameter File`[HERE] <https://github.com/ArduPilot/ardupilot/blob/master/Tools/Frame_params/AION_R1_Rover.param>`_

Connect Wheel Encoders to Autopilot
-----------------------------------

Wiring Directions`[HERE] <http://ardupilot.org/copter/docs/common-wheel-encoder.html>`_

.. note:: The Autopilot parameters settings are pre-configured in the R1 base parameter file.

Configure Motor Driver Firmware
-------------------------------

1. Download and install the “Ion Studio Setup Application” from `[HERE] <http://downloads.ionmc.com/software/IonStudio/setup.exe>`_

  1.1.	Power the motor controller by plugging in and powering on the smart battery.

.. note:: The smart battery has a low current cutoff feature. To maintain minimum current requirements the TX2 must also be powered on.
..

  1.2.	Connect a computer to the motor controller via Micro USB port.

.. note:: The RoboClaw driver will not power itself from the USB port.
..

  1.3.	Open the Ion Studio Application and select **"Connect Selected Unit"**

  1.4.	Under the General Setting tab select **"Control Mode"**

  1.5.	Select **"RC Mode"**

    1.7.7.	 Select **"Device"** tab

    1.7.8.	 Select **"Save Settings"**


.. note:: For in-depth setup guide, please refer to the complete user manual located `[HERE] <http://downloads.ionmc.com/docs/roboclaw_user_manual.pdf>`_


Build r1_control pkg on the TX2
-------------------------------

ssh to the TX2 from a host machine over the AION_UGV wireless network created when the UGV boots.

``ssh -X apsync@10.0.1.128``

Password: ``apsync``

1. Setup Workspace:
::

  mkdir catkin_ws
  cd catkin_ws
  mkdir src
  cd src


2. Clone r1_control pkg:
::

  git clone https://github.com/aionrobotics/aion_r1.git
  cd ..
  catkin_make


3. Source:
::

  echo "source /home/apsync/catkin_ws/devel/setup.bash" >> ~/.bashrc
  source ~/.bashrc

4. Replace APSync mavlink-router config file:
::

  cp /home/apsync/catkin_ws/src/aion_r1/r1_control/config/mavlink-router.conf /home/apsync/start_mavlink-router


UGV Bringup
-------------
`[HERE] <http://docs.aionrobotics.com/en/latest/arduros-getting-started.html>`_
