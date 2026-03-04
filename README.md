# DZ01-USB-FIX
Turns on the USB ports at boot on the Bigtreetech DZ01 board with Allwinner H616 Linux host. This fix was specifically engineered for the Delta Flyer 3d Printer but should apply to any user of the Bigtreetech Armbian image for this board

<h2>**This change involved adding a custom user overlay to the Linux build and requires a change to the printer.cfg supplied with Delta FLyer.**</h2>

While doing the steps out of order will likely work you may suffer strange issues until all steps are completed, **do them in order to reduce frustration.**

This guide assumes the printer is already operational but can be applied in the same order during the final software preparation stages.

<h2>** Step 1 **</h2>
Connect to the DZ01 using its IP address and the username/password of biqu/biqu
Download the dz01-usb-regulator.dts file 
<img width="827" height="617" alt="image" src="https://github.com/user-attachments/assets/83de14af-551c-4782-8631-06ce634e541e" />

<h2>** Step 2 **</h2>
Download the dts file and move to that directory

```shell
cd ~ && git clone https://github.com/chromusphil/DZ01-USB-FIX.git
```

```shell
cd DZ01-USB-FIX
```

<h2>** Step 3 **</h2>
Apply the overlay
```shell
sudo armbian-add-overlay dz01-usb-regulator.dts
```

The dialog should look something like this if it is successful

```
biqu@deltaflyer:/DZ01-USB-FIX/ sudo armbian-add-overlay dz01-usb-regulator.dts
Compiling the overlay
Copying the compiled overlay file to /boot/overlay-user/
Overlay dz01-usb-regulator was already added to /boot/armbianEnv.txt, skipping
Reboot is required to apply the changes 
```
As the dialog states its time to **Power Cycle** the machine. (Full power cycle not just a linux restart).

```shell
sudo shutdown now
```
