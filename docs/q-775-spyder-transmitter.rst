===========
Transmitter
===========

The included FrySky i6S transmitter and FS-IA6B receiver come pre-configured from AION ROBOTICS.

.. image:: ../images/transmitter/FrySky_Callout.JPG
    :scale: 50%
    :align: center

`Download User Manual <https://www.flysky-cn.com/s/FS-i6S-User-manual-20170706-compressed.zip>`_

**Channel Mapping:**

.. tabularcolumns:: |c|c|c|

+---------------------------+-------+
|Function                   |Channel|
+===========================+=======+
| Roll                      | 1     |
+---------------------------+-------+
| Pitch                     | 2     |
+---------------------------+-------+
| Throttle                  | 3     |
+---------------------------+-------+
| Yaw                       | 4     |
+---------------------------+-------+
| Mode Selection            | 5     |
+---------------------------+-------+
| Landing Gear              | 7     |
+---------------------------+-------+


**Switch Functions:**

.. tabularcolumns:: |c|c|c|

+------------+-----------+------------+----------------+--------------------+
| Switch     | Position  | Switch     | Position       | Mode/Function      |
+============+===========+============+================+====================+
| SWA        | UP        | SWB        | UP             | ALTITUDE HOLD      |
+------------+-----------+------------+----------------+--------------------+
| SWA        | UP        | SWB        | MIDDLE         | LOITER             |
+------------+-----------+------------+----------------+--------------------+
| SWA        | UP        | SWB        | DOWN           | AUTO               |
+------------+-----------+------------+----------------+--------------------+
| SWA        | DOWN      | SWB        | UP             | ALTITUDE HOLD      |
+------------+-----------+------------+----------------+--------------------+
| SWA        | DOWN      | SWB        | MIDDLE         | GUIDED             |
+------------+-----------+------------+----------------+--------------------+
| SWA        | DOWN      | SWB        | DOWN           | RTL                |
+------------+-----------+------------+----------------+--------------------+
| SWD        | UP        |            |                | LANDING GEAR DOWN  |
+------------+-----------+------------+----------------+--------------------+
| SWD        | DOWN      |            |                | LANDING GEAR UP    |
+------------+-----------+------------+----------------+--------------------+

**Flight Mode Specifications:**

.. raw:: html

   <table border="1" class="docutils">
   <tr><th>Mode</th><th>Alt Ctrl</th><th>Pos Ctrl</th><th>GPS</th><th>Summary</th></tr>
   <tr><td>ALTITUDE HOLD</td><td>P</td><td>+</td><td></td><td>Holds altitude and self-levels the roll & pitch</td></tr>
   <tr><td>AUTO</td><td>A</td><td>A</td><td>Y</td><td>Executes pre-defined mission</td></tr>
   <tr><td>GUIDED</td><td>A</td><td>A</td><td>Y</td><td>Navigates to single points commanded by GCS</td></tr>
   <tr><td>LOITER</td><td>P</td><td>P</td><td>Y</td><td>Holds altitude and position, uses GPS for movements</td></tr>
   <tr><td>RTL</td><td>A</td><td>A</td><td>Y</td><td>Returns to takeoff location, may also include landing</td></tr>
   </table>

**Mode Function Key:**

.. raw:: html

   <table border="1" class="docutils">
   <tr><th>Symbol</th><th>Definition</th></tr>
   <tr><td>-</td><td>Manual control</td><tr>
   <tr><td>+</td><td>Manual control with limits & self-level</td><tr>
   <tr><td>P</td><td>Pilot controls climb rate/position target</td></tr>
   <tr><td>A</td><td>Automatic control</td></tr>
   </table>
