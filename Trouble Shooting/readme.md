Troubleshooting tips:

* Problem finding Com Port for the DM164140 Evaluation board.

This problem was encoutered on a windows 7 64 bit system
 
If you open cool term and recive an error like below when you have your board attached to you pc via the usb cable you may have a driver problem. Even with out this error you may have this driver problem you just might have other items acting as com ports for coolterm to find.
 
![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/T1.png "Error")

This is a possible fix to the problem.

First go to the device manager in your computer

This can be found by typeing "Decive Manager" in the search bar of the start menu.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/T2.png "Start Menu")

Once in the Device Manager under "Other Devices" you should find "Microchip Composite Device".

**Note** If you do not see this then either your evaluation board is not connected to your PC or this is not the problem you are having

Now either download "mdmcpq.inf" or search for it on your computer. You will need this driver to get the evaluation board to work properly.

From here right click on "Microchip Composite Device" and choose "Update Driver Software..." and follow the next few pictures.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/T4.png)

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/T5.png)

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/T6.png)

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/T7.png)

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/T8.png)

Once you are on this screen click browse and find where you either located "mdmcpq.inf" or where you saved the one you downloaded.

Next click "OK"

Now you should be looking at a screen similar to this.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/T9.png)

Click Next 

Windows will now throw a security window up. Click to "Install this driver software anyway". This security is because this is not an offical driver for the evaluation board but this was the only driver I could find to work for our board.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/T10.png)

And you are done you sould now find that the "Microchip Composite Device" is no longer under "Other Device" and a new device under "Ports" That new devices com# (Photo shows com10) is the com port you should use with cool term to communicate with the evaluation board.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/T11.png)
