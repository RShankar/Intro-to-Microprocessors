The EMC1001 is hard wired to RC3 and RC4 for its I2C communication. So, we must use 2 other pins for our seven-segment display. RC3 is what we were using for controlling our B_SEG and RC4 controls the cathode hooked up to digit 3.

For this work around we reroute B_SEG from RC3 to RA1 and our C3 from RC4 to RA0. To achieve this we first bend the 2 pins in question, so they are out some. Be careful this should bend with no problem, but you do not want to snap the pin or break the solder joint.

 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven_Segment_Display_With_EMC1001/T1.jpg)
 
 Now take 2 of the Male to Female jumpers provided, that you would have used for the ping sensor, to wire these pins as shown below. This will not make perfect contact, but it will be good enough for our purposes.
 
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven_Segment_Display_With_EMC1001/T2.jpg)
 
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven_Segment_Display_With_EMC1001/T3.jpg)
 
 Now we need to change the code. Most of you probably will start with the code given for the seven-segment display. So, I have shown below the 2 changes needed in the MCC for this.
 
 You will need to release RC 3 and RC4 to be used by your MSSP and Lock RA0 and RA1 as GPIO.
 
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven_Segment_Display_With_EMC1001/TPM.png)
 
 Next you will need to make sure to label the pins RA0 should be named C3 and RA1 should be named SEG_B for the existing code to work.
 
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven_Segment_Display_With_EMC1001/TPM2.png)
 
The onboard LEDS will turn on and off but that is to be expected as they are hardwired in to RA0 and RA1

