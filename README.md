# DZ01-USB-FIX
Turns on the USB ports at boot on the Bigtreetech DZ01 board with Allwinner H616 Linux host. This fix was specifically engineered for the Delta Flyer 3d Printer but should apply to any user of the Bigtreetech Armbian image for this board

**This change involved adding a custom user overlay to the Linux build and requires a change to the printer.cfg supplied with Delta FLyer.**

While doing the steps out of order will likely work you may suffer strange issues until all steps are completed, **do them in order to reduce frustration.**

This guide assumes the printer is already operational but can be applied in the same order during the final software preparation stages.

<u> ** Step 1 ** </u>
