This is a how to for creating a new project in MPLAP X IDE

The yellow square with a green plus is the short cut for creating a new project

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/11.png "IDE Download 1")

You will need to select a type of project the standalone project will be what we work with

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/12.png "IDE Download 1")

Select the microcontroller you are using. We are currently using the PIC16F18855 microcontroller

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/13.png "IDE Download 1")

The PIC16F18855 Needs the simulator option selected.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/14.png "IDE Download 1")

Here you will choose the compiler that the project will use. The XC8 is used for the PIC16F18855

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/15.png "IDE Download 1")

Lastly give your project a name.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/16.png "IDE Download 1")

One Last bit of helpful information when using the MPLAB X IDE for the evaluation boards.

The Evaluation board is programed by moving a .HEX file to the "Mass storage device" representation of the board on your PC. To easily find the new .HEX files it is recommended you make a folder that is easily accessible, the example is a folder on the desktop. This will allow you to easily move the files every time you sit down to work on a project. 

To have the .HEX file show up in your new folder you must follow the following steps for all new projects.

First right click on the project and select properties.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/17.png "Properties")

From here select Building on the left

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/18.png "Building")

Finally add __cp ${ImagePath} YOUR PATH HERE__ to the execute this line after build field and check the check box. C:\Users\Doug\Desktop\HEX is the path used for this example.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/19.png "Add Path")
