=====================
ArduROS Configuration
=====================

.. note:: The R1 "ArduROS Package" ships "ready-to-code" with all hardware & software fully configured. The information provided below is for troubleshooting, educational or R1 upgrade purposes.

Pre-Configured ArduROS TX2 Img:
-------------------------------

`[HERE] <https://www.dropbox.com/s/i5a7q569wa3ckpj/TX2_3.3_ArduROS_Gold.tar.gz?dl=0>`_

To clone your TX2:
------------------

1. Set the TX2 into recovery mode by unplugging power, then power up, press the power button, then press and hold the force recovery button, press the reset button and after 5 sec release the force recovery button.

2. Read system.img from the gold board filesystem partition with the following command located in L4T_install_dir/64_TX2/Linux_for_Tegra:

``sudo ./flash.sh -r -k APP -G clone.img jetson-tx2 mmcblk0p1``

*This creates a clone.img and clone.img.raw in the <top> directory.*

To flash your TX2 with the pre-configured image or your cloned image:
---------------------------------------------------------------------

1. Copy clone.img.raw to the <L4T>/bootloader/system.img directory with the following command:

``sudo cp clone.img.raw bootloader/system.img``

2. If the board has already been flashed with default release images, use the following command to flash the clone image to the APP partition:

``sudo ./flash.sh -r -k APP jetson-tx2 mmcblk0p1``

3. If the board has NOT been flashed with default release images, use the following command:

``sudo ./flash.sh -r jetson-tx2 mmcblk0p1``

4. For AION's images, after flashing it is required to set the correct hostname and Access Point names to add the last two bytes of the MAC address. To do this log into the TX2 using the following command:

``ssh apsync@aionugvflash.local``

5. Run the following command to set the hostname and access points and then reboot and check for the correct accesspoint:

``sudo ./runonce.sh``

Jetson TX2 Requirements:
------------------------

1. The following prerequisites must be installed/setup on NVIDIA Jetson TX2

  [x] NVIDIA Jetpack 3.3

Build APSync on the TX2
-------------------------
Directions `[HERE] <https://github.com/aionrobotics/companion/blob/next-tx2/Nvidia_JTX1/Ubuntu/1_create_base_image-tx2.txt>`_

When the UGV boots, a Wifi Access Point is created:

SSID: ``AIONio-XXXX``

Password: ``aionrobotics``

User: ``aion``

Password: ``aion``

``ssh -X aion@10.0.1.128``

Install ROS on the TX2
----------------------
Use the ``installROS.sh`` script from our `[installROSTX2 GitHub Repo] <https://github.com/aionrobotics/installROSTX2>`_


Install MAVROS packages:
---------------------

Use the ``installMAVROS.sh`` script from our `[installROSTX2 GitHub Repo] <https://github.com/aionrobotics/installROSTX2>`_


Configure Autopilot:
--------------------

Detailed Setup `[HERE] <http://docs.aionrobotics.com/en/latest/ardupilot-package.html>`_

Parameter File `[HERE] <https://github.com/ArduPilot/ardupilot/blob/master/Tools/Frame_params/AION_R1_Rover.param>`_

Connect Wheel Encoders to Autopilot
-----------------------------------

Wiring Directions `[HERE] <http://ardupilot.org/copter/docs/common-wheel-encoder.html>`_

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


Build aion_navigator package on the TX2
-------------------------------

.. note:: These packages are installed automatically using the scripts mentioned above in the installROS and installMAVROS sections. The instructions here are only for reference but are not needed if the scripts above are used. Also note that installing the package this way may generate errors if the packages it depends on are not installed. 

ssh to the TX2 from a host machine over the wireless network created when the UGV boots (AIONio-XXXX where XXXX are the last four MAC address digits).

``ssh -X aion@10.0.1.128``

Password: ``aion``

1. Setup Workspace:
::

  mkdir AIONio_ws
  cd AIONio_ws
  mkdir src
  cd src


2. Clone aion_navigator pkg:
::

  git clone https://github.com/aionrobotics/aion_navigator.git
  cd ..
  catkin_make


3. Source:
::

  echo "source /home/apsync/AIONio_ws/devel/setup.bash" >> ~/.bashrc
  source ~/.bashrc

MAVLINK_ROUTER Configuration
----------------------------

ArduPilot's APSync relies on MAVLINK_ROUTER to distribute MAVLINK packets to other nodes that need them. MAVLINK router has a configuration file to tell it to which ports it should send MAVLINK data. If you need to have comunication with the Autopilot using MAVLINK, you will need to modify the configuration to open a port for your application.

To do so, you need to modify the file ``/home/apsync/start_mavlink-router/mavlink-router.conf``

For details on the configuration file usage, checkout the `[mavlink-router GitHub Repo] <https://github.com/intel/mavlink-router>`_

UGV Bringup
-------------
`[HERE] <http://docs.aionrobotics.com/en/latest/arduros-getting-started.html>`_
