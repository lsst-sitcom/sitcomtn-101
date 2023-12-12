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

   +-------------+--------------------------+--------------------------+
   | FCU state   | Start Time               | End Time                 |
   +=============+==========================+==========================+
   | All off     | '2023-12-07 14:20:00.00' | '2023-12-07 14:30:00.00' |
   +-------------+--------------------------+--------------------------+
   | All on 100% | '2023-12-07 14:33:00.00' | '2023-12-07 14:50:00.00' |
   +-------------+--------------------------+--------------------------+
   | All on 10%  | '2023-12-07 14:33:00.00' | '2023-12-07 14:50:00.00' |
   +-------------+--------------------------+--------------------------+
   | All on 20%  | '2023-12-07 14:33:00.00' | '2023-12-07 14:50:00.00' |
   +-------------+--------------------------+--------------------------+
   | All on 30%  | '2023-12-07 14:33:00.00' | '2023-12-07 14:50:00.00' |
   +-------------+--------------------------+--------------------------+
   | All on 40%  | '2023-12-07 14:33:00.00' | '2023-12-07 14:50:00.00' |
   +-------------+--------------------------+--------------------------+
   | All on 50%  | '2023-12-07 14:33:00.00' | '2023-12-07 14:50:00.00' |
   +-------------+--------------------------+--------------------------+
   | All on 60%  | '2023-12-07 14:33:00.00' | '2023-12-07 14:50:00.00' |
   +-------------+--------------------------+--------------------------+
   | All on 70%  | '2023-12-07 14:33:00.00' | '2023-12-07 14:50:00.00' |
   +-------------+--------------------------+--------------------------+
   | All on 80%  | '2023-12-07 14:33:00.00' | '2023-12-07 14:50:00.00' |
   +-------------+--------------------------+--------------------------+
   | All on 90%  | '2023-12-07 14:33:00.00' | '2023-12-07 14:50:00.00' |
   +-------------+--------------------------+--------------------------+
   | All on 100% | '2023-12-07 14:33:00.00' | '2023-12-07 14:50:00.00' |
   +-------------+--------------------------+--------------------------+

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

See appendix for IMS behaviour the system was not sensitive to vibrations.

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

   VMS telemetry zoom for all FCUs at 100% (blue) and all off (orange).


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
