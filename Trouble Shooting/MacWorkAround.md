There is an issue with using this board on MACs where IOS will not allow you to program the board. The issue is the **Mass storage device** Shows up as read only. It seems to only effect certain Macs. So, if your Mac lets you write to the board then you are good to go otherwise this document will help you. Addtionally serial communication should work just fine on Mac with the CoolTerm Program.

Once you have a .HEX file that you want to program to the board load up VMware (photos are taken from a PC) and log in to the all engineering student’s desktop. 

__-If you do not have VMware on your computer please follow the steps here https://tsg.eng.fau.edu/software/vmware-remote-desktop-access/__

Next activate the USB for VMware
![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/M1a.png)

The icon will look slightly different on the VMware version of mac

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/M2.png)

You can choose to turn on the automatic options most people find it convent, or you can select the individual USB every time you log on to VMware.

From here go to the my computer on VMware

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/M3.png)

Next select the bottom drive option it should be the name of your Mac/PC (Mine is called Doug-LT)

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/M4.png)

Lastly navigate to where you have stored your .HEX file in your MAC file system. Then simply drag and drop the .HEX you want to program to the Xpress mass storage drive.

**Note your drive letter maybe different and that is fine it is assigned by each pc/mac**

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Trouble%20Shooting/M5.png)
