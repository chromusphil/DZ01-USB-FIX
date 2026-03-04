# DZ01-USB-FIX
Turns on the USB ports at boot on the Bigtreetech DZ01 board with Allwinner H616 Linux host. This fix was specifically engineered for the Delta Flyer 3d Printer but should apply to any user of the Bigtreetech Armbian image for this board

<h2>**This change involves adding a custom user overlay to the Linux build and requires a change to the printer.cfg supplied with Delta FLyer, do a backup of your configs.**</h2>

While doing the steps out of order will likely work you may suffer strange issues until all steps are completed, **do them in order to reduce frustration.**

<h2>Do I need to do this?</h2>
No, you <u>don't need to do this</u> fix unless you wish to use a USB powered touch screen and or USB connectivity for a toolhead board or other secondary MCU.

This guide assumes the printer is already operational but can be applied in the same order during the final software preparation stages.

<h2>** Step 1 ** </h2>
Modify your printer.cfg to stop klipper from trying to do a workaround to turn on the USB.

This can be done either before uploading to the printer or once the printer.cfg is uploaded to your Mainsail interface.

** If you already have a working printer.cfg right click it and choose Duplicate a dialog will appear, asking for a name to call the duplicate. I add .backup to the end of mine for ease.

<img width="487" height="256" alt="image" src="https://github.com/user-attachments/assets/c2a5814a-3587-46f4-98a6-94052f316e8f" />



Now right click printer.cfg and choose edit



<img width="780" height="416" alt="image" src="https://github.com/user-attachments/assets/cf3f26ba-9bff-4f95-abd0-c62a0fe9d377" />


I recommend simply # out the lines and addint a comment to that section

Find his section:
```
# MORE INFO:  https://www.klipper3d.org/Config_Reference.html#output_pin
[output_pin _usb_host_en] # This turns on the USB ports on the DZ01, you should not need to change this.
pin: h616:gpio209  #PG17
value: 1
```

and change it to this (by adding the # to the beginning of each line)
```
#[output_pin _usb_host_en] # This turns on the USB ports on the DZ01, you should not need to change this.
#pin: h616:gpio209  #PG17
#value: 1
```
Then add this just above the changes we made to remind you what you did and why

```shell
### This has been changed to be handled by a custom overlay from https://github.com/chromusphil/DZ01-USB-FIX ###
```

<h2>** Step 2 **</h2>
Connect to the DZ01 using its IP address and the username/password of biqu/biqu
Download the dz01-usb-regulator.dts file 
<img width="827" height="617" alt="image" src="https://github.com/user-attachments/assets/83de14af-551c-4782-8631-06ce634e541e" />

<h2>** Step 3 **</h2>
Download the dts file and move to that directory

```shell
cd ~ && git clone https://github.com/chromusphil/DZ01-USB-FIX.git
```

```shell
cd DZ01-USB-FIX
```

<h2>** Step 4 **</h2>
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
