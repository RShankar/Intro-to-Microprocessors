In the Express Web IDE right click on the project then "Package as MPLAB X Project"

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/21.png "Package as MPLAB X Project")

This will download a .ZIP file which will contain a folder that ends with .X place this folder in your IDE projects folder. Then open the project in MPLAB X IDE. The 3rd icon is the open button navigate to where you unzipped the zip file to, Your IDE Projects folder.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/22.png "Open")

Now that you have the project in the IDE there is a small problem with the export/Import problem there is no compiler assigned to this project. __You will have to assign the compiler__ 

To start with right click on the project and go to properties 

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/23.png "Property")

in the conf: Section you will see the complier toolchain section has nothing selected

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/24.png "No comp")

Select the XC8 Compiler and click ok. Your project should now work exactly how it did in the Xpress IDE

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/25.png "selected XC8")

Now would be a good time to set your build folder also.

The Evaluation board is programed by moving a .HEX file to the "Mass storage device" representation of the board on your PC. To easily find the new .HEX files it is recommended you make a folder that is easily accessible, the __Recommended__ example is a folder on your C Drive (Z drive if you are using VMware or zero point client). This will allow you to easily move the files every time you sit down to work on a project.

To have the .HEX file show up in your new folder you must follow the following steps for all new projects.

Select Building on the left

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/18.png "Building")

Finally add __cp ${ImagePath} c:\HEX__ or __cp ${ImagePath} z:\HEX__ to the execute this line after build field and check the check box. C:\Users\Doug\Desktop\HEX is the path used for this example.

__You must create a new folder called HEX on your C or Z drive for this to work otherwise you will get errors__

__Having more complex file paths like the one below to the desktop may cause errors__

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/MPLab%20X%20IDE/19.png "Add Path")
