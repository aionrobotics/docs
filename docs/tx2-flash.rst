============
TX2 Flashing
============

.. note:: AION ROBOTICS vehicles ship "ready-to-code" with all hardware & software fully configured. The information provided below is for upgrade or factory reset purposes.

AIONio TX2 System Img:
----------------------

- `[HERE]  <https://aionrobotics-my.sharepoint.com/:u:/p/nickn/ERv2N-CsZ09Cnz986xDi5B4BFJDjCBdXBE18VtLq64iyGA?e=UwWEwT>`_

To clone your TX2:
------------------

1. Set the TX2 into recovery mode by unplugging power, then power up, press the power button, then press and hold the force recovery button, press the reset button and after 5 sec release the force recovery button.

2. Read system.img from the gold board filesystem partition with the following command located in L4T_install_dir/64_TX2/Linux_for_Tegra:

``sudo ./flash.sh -r -k APP -G clone.img jetson-tx2 mmcblk0p1``

*This creates a clone.img and clone.img.raw in the <top> directory.*

To flash your TX2 with the pre-configured image or your own image:
------------------------------------------------------------------

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
