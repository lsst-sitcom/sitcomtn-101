:tocdepth: 1

.. sectnum::

.. Metadata such as the title, authors, and description are set in metadata.yaml

.. TODO: Delete the note below before merging new content to the main branch.

.. note::

   **This technote is a work-in-progress.**

Abstract
========

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


This technote uses data from the VMS, dc accelerometers and IMS to estimate the effect of the Fan Coil Units (FCUs) are likely to have on image quality
Primarily we use the Vibration Monitoring System (VMS) of the M1M3 for more information see the VMS confluence page (link here).

Times of events
================

.. _table-label2:

.. table:: Timestamps for data with FCU state labels.

   +---------+------------------------+------------------------+
   |FCU state| Start Time             | End Time               |
   +=========+========================+========================+
   |       0 | 2023-12-07 14:20:00.00 | 2023-12-07 14:30:00.00 |
   +---------+------------------------+------------------------+
   |     100 | 2023-12-07 14:33:00.00 | 2023-12-07 14:50:00.00 |
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
   |      80 | 2023-12-07 15:30:05.00 | 2023-12-07 15:40:00.00 |
   +---------+------------------------+------------------------+
   |      90 | 2023-12-07 15:40:40.00 | 2023-12-07 15:43:40.00 |
   +---------+------------------------+------------------------+
   |      90 | 2023-12-07 15:48:55.00 | 2023-12-07 15:50:10.00 |
   +---------+------------------------+------------------------+
   |     100 | 2023-12-07 15:53:00.00 | 2023-12-07 16:09:00.00 |
   +---------+------------------------+------------------------+

First event All 100% vs off
===========================
The first event we look at is comparing the state with no fans on and the state will all fans running at 100%.

Telemetry
---------

.. figure:: /_static/images/vms_telemetry_1.png
   :name: fig-vms-telemetry-1
   :target: ../_images/vms_telemetry_1.png
   :alt: event 1 vms telemetry

   VMS telemetry for all FCUs at 100% (blue) and all off (orange).

.. figure:: /_static/images/hardpoints_telemetry_1.png
   :name: fig-hardpoints-telemetry-1
   :target: ../_images/hardpoints_telemetry_1.png
   :alt: event 1 hardpoints telemetry

   hardpoints telemetry for all FCUs at 100% (blue) and all off (orange).

.. figure:: /_static/images/dc_accelerometers_telemetry_1.png
   :name: fig-dc-accelerometers-telemetry-1
   :target: ../_images/dc_accelerometers_telemetry_1.png
   :alt: event 1 dc accelerometers telemetry

   dc accelerometers telemetry for all FCUs at 100% (blue) and all off (orange).

See appendix for IMS behavior the system was not sensitive to vibrations.

PSD analysis
------------

.. figure:: /_static/images/vms_psd_1.png
   :name: fig-vms-psd-1
   :target: ../_images/vms_psd_1.png
   :alt: event 1 vms psd

   VMS psd for all FCUs at 100% (blue) and all off (orange).

.. figure:: /_static/images/hardpoints_psd_1.png
   :name: fig-hardpoints-psd-1
   :target: ../_images/hardpoints_psd_1.png
   :alt: event 1 hardpoints psd

   hardpoints psd for all FCUs at 100% (blue) and all off (orange).

.. figure:: /_static/images/dc_accelerometers_psd_1.png
   :name: fig-dc-accelerometers-psd-1
   :target: ../_images/dc_accelerometers_psd_1.png
   :alt: event 1 dc accelerometers psd

   dc accelerometers psd for all FCUs at 100% (blue) and all off (orange).

VMS low frequency
-----------------

.. figure:: /_static/images/vms_telemetry_zoom_1.png
   :name: fig-vms-telemetry-zoom-1
   :target: ../_images/vms_telemetry_zoom_1.png
   :alt: event 1 vms telemetry zoom

   VMS telemetry zoom for all FCUs at 100% (blue) and all off (orange). We see a low frequency oscillation that could be beating due to variations in the FCU frequencies.

PSD analysis for FCUs powered at different speeds
=================================================
First we show PSDs (nomalized to have a peak of 1) for each fan state and each channel.

.. figure:: /_static/images/total_1_psd_comp.png
   :name: fig-total-psd-comp-1
   :target: ../_images/total_1_psd_comp.png
   :alt: compare psd across fan states

   The legend shows the commanded power for each line (going from off, 0%, to full power, 100%). This data is the total acceleration from channel 1 M1M3 VMS.

.. figure:: /_static/images/total_2_psd_comp.png
   :name: fig-total-psd-comp-2
   :target: ../_images/total_2_psd_comp.png
   :alt: compare psd across fan states

   The legend shows the commanded power for each line (going from off, 0%, to full power, 100%). This data is the total acceleration from channel 2 M1M3 VMS.

.. figure:: /_static/images/total_3_psd_comp.png
   :name: fig-total-psd-comp-3
   :target: ../_images/total_3_psd_comp.png
   :alt: compare psd across fan states

   The legend shows the commanded power for each line (going from off, 0%, to full power, 100%). This data is the total acceleration from channel 3 M1M3 VMS.

.. figure:: /_static/images/displacement_comp.png
   :name: fig-displacement-comp
   :target: ../_images/displacement_comp.png

   Comparison of the displacement rms for all frequencies above 1 Hz as a function of fan power state, each row shows the behavior for one of the VMS channels.

.. figure:: /_static/images/duration_comp.png
   :name: fig-duration-comp
   :target: ../_images/duration_comp.png

   Comparison of the duration of the measurement window for the measurement of the VMS telemetry a function of fan power state.

Appendix
=========
.. figure:: /_static/images/ims_positions_1.png
   :name: fig-ims-positions
   :target: ../_images/ims_positions_1.png
   :alt: event 1 IMS positions telemetry

   IMS positions during event 1

.. figure:: /_static/images/ims_rotations_1.png
   :name: fig-ims-rotations
   :target: ../_images/ims_rotations_1.png
   :alt: event 1 IMS rotations telemetry

   IMS rotations during event 1
