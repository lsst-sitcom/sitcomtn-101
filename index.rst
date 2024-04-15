#####################################################
Investigation into vibrations in the M1M3 due to FCUs
#####################################################

.. abstract::

   This technote uses data from the VMS, dc accelerometers and IMS to estimate the effect of the Fan Coil Units (FCUs) are likely to have on image quality



.. Metadata such as the title, authors, and description are set in metadata.yaml

.. TODO: Delete the note below before merging new content to the main branch.

.. note::

   **This technote is a work-in-progress.**

Introduction
============

.. Assuming units of VMS = mg
.. -displacement for total_1
..  FCU on = 41.55 μm
..  FCU off = 2.30 μm
.. -displacement for total_2
..  FCU on = 11.56 μm
..  FCU off = 2.21 μm
.. -displacement for total_3
..  FCU on = 46.05 μm
..  FCU off = 1.94 μm


This technote uses data from the VMS, dc accelerometers and IMS to estimate the effect of the Fan Coil Units (FCUs) are likely to have on image quality.
Primarily we use the Vibration Monitoring System (VMS) attached to M1M3 (for more information see the 
`VMS confluence page <https://confluence.lsstcorp.org/pages/viewpage.action?pageId=156502157>`_).
The description of the FCU is avaiable in 
`SPIE 77331E <https://www.spiedigitallibrary.org/conference-proceedings-of-spie/7733/77331E/LSST-primarytertiary-mirror-thermal-control-system/10.1117/12.857438.short#_=_>`_.

The VMS data are stored in a single hdf5 data file (/sdf/data/rubin/shared/mtm1m3_test_files/vms_data/2023/12/M1M3-2023-12-07T00:00.hdf) acquired on 2023/12/07. A description of the 
data taking procedure with exact timing is available in a log file attached to the JIRA ticket `SITCOM-1131 <https://rubinobs.atlassian.net/browse/SITCOM-1131>`_ associated to this Technical Note. 
The timing of each data taking period corresponding to the various fan speeds expressed in percent of the maximum speed is deduced from the log file.

Times of events
================

.. _table-label2:

.. table:: Timestamps for data with FCU state labels.

   +---------+------------------------+------------------------+
   |FCU state| Start Time             | End Time               |
   +=========+========================+========================+
   |       0 | 2023-12-07 14:20:00.00 | 2023-12-07 14:30:00.00 |
   +---------+------------------------+------------------------+
   |      10 | 2023-12-07 14:55:30.00 | 2023-12-07 14:59:55.00 |
   +---------+------------------------+------------------------+
   |      20 | 2023-12-07 15:00:05.00 | 2023-12-07 15:04:00.00 |
   +---------+------------------------+------------------------+
   |      30 | 2023-12-07 15:05:05.00 | 2023-12-07 15:10:00.00 |
   +---------+------------------------+------------------------+
   |      40 | 2023-12-07 15:12:30.00 | 2023-12-07 15:14:30.00 |
   +---------+------------------------+------------------------+
   |      50 | 2023-12-07 15:16:15.00 | 2023-12-07 15:20:00.00 |
   +---------+------------------------+------------------------+
   |      60 | 2023-12-07 15:21:40.00 | 2023-12-07 15:25:00.00 |
   +---------+------------------------+------------------------+
   |      70 | 2023-12-07 15:26:05.00 | 2023-12-07 15:30:00.00 |
   +---------+------------------------+------------------------+
   |      80 | 2023-12-07 15:31:05.00 | 2023-12-07 15:40:00.00 |
   +---------+------------------------+------------------------+
   |      90 | 2023-12-07 17:48:55.00 | 2023-12-07 17:50:10.00 |
   +---------+------------------------+------------------------+
   |     100 | 2023-12-07 14:33:00.00 | 2023-12-07 14:45:00.00 |
   +---------+------------------------+------------------------+
   |     100 | 2023-12-07 17:51:30.00 | 2023-12-07 17:53:00.00 |
   +---------+------------------------+------------------------+

Data quality
============
We have checked that the TMA was not moving during this test and that the mirror was raised (MTM1M3.logevent_detailedState == ACTIVEENGINEERING) with Hard Point in standby mode. 

The second test was to check the VMS accelerometers sampling rate which is supposed to be 200 Hz. To do so, we compute the time difference (*delta t*) between consecutive samples.
In the following plot (left), we see that while most of the samples are separated by ~0.005s (200 Hz), some samples are separated by ~0.00444s. If we plot *delta t* as a function of 
the sample number (right plot) we see that this feature is periodic and could potentially impact the PSD analyses. This issue has been reported as a bug in the JIRA ticket 
`DM-43219 <https://rubinobs.atlassian.net/browse/DM-43219>`_. Petr Kubanek pointed that the 200 Hz sampling rate is fixed by the hardware, so the observed behavior is probably due to a 
wrong timestamp recording and will not affect the PSD analyses.

.. figure:: /_static/images/sampling.png
   :name: sampling
   :target: _images/sampling.png
   :alt: VMS sampling rate verification.

   Histogram of the time between consecutive samples (left) - Time between consecutive samples as a function of the sample number (right).


First event All 100% vs off
===========================
We compare the state with fans off (0%) and the state will all fans running at 100% for various sensors.
In the first plot the quantity refered as the total acceleration correspond to the norm of the acceleration vector measured by the accelerometers.

Telemetry
---------

.. figure:: /_static/images/vms_telemetry_1.png
   :name: fig-vms-telemetry-1
   :target: _images/vms_telemetry_1.png
   :alt: event 1 vms telemetry

   VMS total acceleration (norm of the acceleration vector) for all FCUs at 100% (blue) and all off (orange).

.. figure:: /_static/images/hardpoints_telemetry_1.png
   :name: fig-hardpoints-telemetry-1
   :target: _images/hardpoints_telemetry_1.png
   :alt: event 1 hardpoints telemetry

   Hardpoints forces for all FCUs at 100% (blue) and all off (orange).

.. figure:: /_static/images/dc_accelerometers_telemetry_1.png
   :name: fig-dc-accelerometers-telemetry-1
   :target: _images/dc_accelerometers_telemetry_1.png
   :alt: event 1 dc accelerometers telemetry

   Acceleration measured by dc accelerometers for all FCUs at 100% (blue) and all off (orange).

We clearly see that the FCU running at 100% has a measurable effect on M1M3. In the following section we will try to characterize this effect
and check how it behaves while varying the fan speed.


PSD analysis
============

For clarity reason and as we have multiple plots corresponding to the three sensors (accelerometers) each measuring the acceleration along 3 axes and for 11 values of the fan speed we
choose to show only typical plots in this section. The whole set of plots will be given in the appendix.

Acceleration
------------

In the following plot we show the PSD acceleration for sensor 1 - z axis and for every fan speed. We see that there is a narrow peak at about 38 Hz which is visible
for almost every speed. As the peak is present when the fans are not running, it is clear that its origin is not rekated to the FCU.

.. figure:: /_static/images/psd_sensor_3_axis_z.png
   :name: psd_sensor_3_axis_z
   :target: _images/psd_sensor_3_axis_z.png
   :alt: PSD acceleration for sensor 3 - z axis and for every fan speed

   PSD acceleration for sensor 3 - z axis and for every fan speed

The only significant feature which is likely related to the fan speed is the broad peak which appears at 80% speed and which moves from ~40 Hz at 80%, ~65 Hz at 90% and 
up to ~98 Hz at 100% speed (notice that the peak at 98 Hz is present in both datasets acquired at 100% speed and taken more than 2 hours apart).
The same behavior is observed in most of the cases (sensors and axes). The most pronounced effect is along the z axis.

For comparison we show the same plot but for sensor 1 and y axis.

.. figure:: /_static/images/psd_sensor_1_axis_y.png
   :name: psd_sensor_1_axis_y
   :target: _images/psd_sensor_1_axis_y.png
   :alt: PSD acceleration for sensor 1 - y axis and for every fan speed

   PSD acceleration for sensor 1 - y axis and for every fan speed

The following plot is showing the PSD acceleration for a fan speed set at 80% and for the 3 sensors and the 3 axes. 

.. figure:: /_static/images/psd_speed_80.png
   :name: psd_speed_80
   :target: _images/psd_speed_80.png
   :alt: PSD acceleration for a fan speed set at 80% and for the 3 sensors and the 3 axes

   PSD acceleration for a fan speed set at 80% and for the 3 sensors and the 3 axes

The appearance of the broad peak around 40 Hz is clearly visible in all cases. The effect is nevertheless much less pronounced for Sensor 2. 

Displacement
------------

The following plot shows the cumulative displacement computed for Sensor 1 and x axis:

.. figure:: /_static/images/psd_cumul_disp_sensor_1_axis_x.png
   :name: psd_cumul_disp_sensor_1_axis_x
   :target: _psd_cumul_disp_sensor_1_axis_x.png
   :alt: Cumulative displacement for Sensor 1 and x axis

   Cumulative displacement for Sensor 1 and x axis

As expected the highest contributions to the displacement is coming from the the low frequencies. The effect of the FCU on the displacement is only noticeable for the first dataset
with fans running at 100% speed. This effect is not visible in the second 100% speed dataset (which is much shorter). The same behavior is observable for all the sensors and all
the axes.

Conclusions
===========

From this study we conclude that we see an effect of the FCU when running at 100% speed. The PSD analysis exhibits a broad peak in the spectrum for speeds
larger than 80% of the maximium speed. The contribution of this peak to the mirror displacement is negligeable at all speeds and the only sigificant contribution to the displacement
is seen at 100% speed, probably coming from the lower frequencies.

The significance of this analysis is limited by the size of the dataset and the fact that we only have one set of measurements per speed (2 for 100%). It is difficult to disentangle
the effect of contributions external to the FCU.

The measurements will have to be repeated when the glass mirror is in place.

Appendix
=========

In this appendix we put all the plots corresponding to the PSD analysis for the 3 sensors and the 3 axes.

.. figure:: /_static/images/psd_sensor_1_axis_x.png
   :name: psd_sensor_1_axis_x
   :target: _images/psd_sensor_1_axis_x.png
   :alt: PSD acceleration for sensor 1 - x axis and for every fan speed

   PSD acceleration for sensor 1 - x axis and for every fan speed

.. figure:: /_static/images/psd_sensor_1_axis_y.png
   :name: psd_sensor_1_b_axis_y
   :target: _images/psd_sensor_1_axis_y.png
   :alt: PSD acceleration for sensor 1 - y axis and for every fan speed

   PSD acceleration for sensor 1 - y axis and for every fan speed

.. figure:: /_static/images/psd_sensor_1_axis_z.png
   :name: psd_sensor_1_axis_z
   :target: _images/psd_sensor_1_axis_z.png
   :alt: PSD acceleration for sensor 1 - z axis and for every fan speed

   PSD acceleration for sensor 1 - z axis and for every fan speed

.. figure:: /_static/images/psd_sensor_2_axis_x.png
   :name: psd_sensor_2_axis_x
   :target: _images/psd_sensor_2_axis_x.png
   :alt: PSD acceleration for sensor 2 - x axis and for every fan speed

   PSD acceleration for sensor 2 - x axis and for every fan speed

.. figure:: /_static/images/psd_sensor_2_axis_y.png
   :name: psd_sensor_2_axis_y
   :target: _images/psd_sensor_2_axis_y.png
   :alt: PSD acceleration for sensor 2 - y axis and for every fan speed

   PSD acceleration for sensor 2 - z axis and for every fan speed
   
.. figure:: /_static/images/psd_sensor_2_axis_z.png
   :name: psd_sensor_2_axis_z
   :target: _images/psd_sensor_2_axis_z.png
   :alt: PSD acceleration for sensor 2 - z axis and for every fan speed

   PSD acceleration for sensor 2 - z axis and for every fan speed

.. figure:: /_static/images/psd_sensor_3_axis_x.png
   :name: psd_sensor_3_axis_x
   :target: _images/psd_sensor_3_axis_x.png
   :alt: PSD acceleration for sensor 3 - x axis and for every fan speed

   PSD acceleration for sensor 3 - x axis and for every fan speed

.. figure:: /_static/images/psd_sensor_3_axis_y.png
   :name: psd_sensor_3_axis_y
   :target: _images/psd_sensor_3_axis_y.png
   :alt: PSD acceleration for sensor 3 - y axis and for every fan speed

   PSD acceleration for sensor 3 - y axis and for every fan speed

.. figure:: /_static/images/psd_sensor_3_axis_z.png
   :name: psd_sensor_3_b_axis_z
   :target: _images/psd_sensor_3_axis_z.png
   :alt: PSD acceleration for sensor 3 - z axis and for every fan speed

   PSD acceleration for sensor 3 - z axis and for every fan speed


