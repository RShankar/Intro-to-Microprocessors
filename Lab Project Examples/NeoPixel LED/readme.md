The main difference for us is that we are using a single NeoPixel whereas Di Jasio uses a homemade board with more than one NeoPixel. 

For this we will edit to code to alternate multiple colors on a single LED instead of pushing multiple colors to different LEDs.

To start with Di Jasio uses RC3 for SDO1 we will be using RB5 as it lines up nicely with 3.3v and GND that we need.
SCK1 and SDI1 can be assigned to arbitrary pins as we will not be using them

Note: you must supply the NeoPixel with 3.3v if you are communicating to it with 3.3v it will not hear the 3.3v communication if you are supplying 5v.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/NeoPixel%20LED/NP1.png)

In the pin module we set a custom name for SDO1 to RB5.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/NeoPixel%20LED/NP2.png)

From here we are going to move on to hooking up the NeoPixel, we need to place data in to our RB5 +5v we are going to use 3.3v for the reason above, Ground will go to GRN. We will not use data out however if you wanted to chain some NeoPixels you would attach this to the next NeoPixel's data in.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/NeoPixel%20LED/NP3.jpg)

Here is a photo of it connected in our board.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/NeoPixel%20LED/NP4.jpg)

The only change to the code is to move the delay from inside the main to inside NeoPixel_Stream. This can be seen in the given code.

The delay is importaint as it tells the NeoPixel to update to the color that just got sent to it.




