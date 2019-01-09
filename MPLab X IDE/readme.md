This is for the stand-alone MPLAB X IDE installation. 


__IMPORTANT:__
many users experience problems due to antivirus software during the installation.
Please disable your antivirus before the installation or if you run in to a problem please uninstall and reinstall the IDE with your antivirus off as a first step to troubleshooting.

Below is a video posted by Microchip on how to install their IDE. The information contained in the video is like the information in this document both are provided for your convenience.

<a href="http://www.youtube.com/watch?feature=player_embedded&v=T8tRqvkFZcw
" target="_blank"><img src="http://img.youtube.com/vi/T8tRqvkFZcw/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="480" height="280" border="10" /></a>

https://youtu.be/T8tRqvkFZcw

First Download both the MPLAB IDE and XC Compiler, links below. The complier needed is the XC 8 as the board used for this class is an 8-bit board.

MPLAB X IDE Download:

https://www.microchip.com/mplab/mplab-x-ide

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/1.png "IDE Download 1")

Pick the correct product for your operating system you will want the newest version.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/1a.png "IDE Download 2")

MPLAB XC Compiler:

https://www.microchip.com/mplab/compiler

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/2.png "XC Download 1")

Pick the correct version for your operating system remember the PIC16F18855 is an 8-bit system so the XC8 complier is required for this chip. Again, you will want the newest version.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/2a.png "XC Download 2")


__Install MPLAB X IDE first.__

You can use all the default setting. 
There is a setting to collect information for the betterment of the program.
Some people do not like to provide any information to the companies.
If you don't wish to provide information back to the manufacture slimly uncheck the required box

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/3.png "Privacy")

After the installer has finished the program it will pop up asking to install multiple drivers.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/4.png "Drivers")


__IMPORTANT:__ if you get an error during the driver installation please follow this link http://ww1.microchip.com/downloads/en/DeviceDoc/50002027D.pdf to the MPLABX IDE User Guide
On page 32 is the process to install the drivers manually. You can also attempt to uninstall MPLABX and reinstall.
http://microchipdeveloper.com/mplabx:manually-install-drivers-for-real-ice-or-icd


Next you will see this window, You can uncheck all the boxes they simply open your web browser to 3 more products one is the compiler which you have already downloaded, The Harmony will not be needed for our purposes, and the MCC is covered later in this document.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/5.png "IDE Final")


__Now install the compiler__ as mentioned earlier we are using the 8-Bit compiler for our 8-bit microcontroller
You can use all the default setting for this installation as well. 

The free version has no restrictions that will affect your work. It is only missing optimization options for things such as faster runtime or less memory usage

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/6.png "Free")


Now that both the IDE and XC8 are installed there is one last program to install it is the __MCC__ which is a plugin in MPLab X 
Open your MPLAB X IDE

Go to Tools->Plugins

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/7.png "Plugin Menu")

Click on the Available Plugins tab

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/8.png "Plugin")

Find the MPLAB Code Configurator in the list select it then click install

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/9.png "Plugin List")

Follow the installation instructions all default settings will work just fine.

Finally restart the IDE and you are good to go 

The IDE works almost identically to the MPLAB express web IDE. There are a few hiccups when moving a project from the Xpress IDE to the X IDE which will be covered in another document,[Xpress To X IDE.md](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/Xpress%20To%20X%20IDE.md).

One Last bit of helpful information when using the MPLAB X IDE for the evaluation boards.

The Evaluation board is programed by moving a .HEX file to the "Mass storage device" representation of the board on your PC. To easily find the new .HEX files it is recommended you make a folder that is easily accessible, the example is a folder on the desktop. This will allow you to easily move the files every time you sit down to work on a project. 

To have the .HEX file show up in your new folder you must follow the following steps for all new projects.

First right click on the project and select properties.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/17.png "Properties")

From here select Building on the left

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/18.png "Building")

Finally add __cp ${ImagePath} YOUR PATH HERE__ to the execute this line after build field and check the check box. C:\Users\Doug\Desktop\HEX is the path used for this example.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/19.png "Add Path")

