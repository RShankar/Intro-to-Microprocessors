As with all things we should start by looking at the data sheet below is the data sheet for the HC - SR04

https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf

The data sheet informs us that one pin is used to activate the sensor (Trig) and the other (Echo) is used to measure the distance.

The ping sensor Di Jasio uses is a 3 pin type meaning the Trig and Echo are done via one pin.

To modify his code to work for our needs we must change a few things

First our pin manager requires 2 pins

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/4-pin%20Ping%20Sensor/Pin_Manager.png)

Then we must edit the pin module

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/4-pin%20Ping%20Sensor/Pin%20Module.png)

Now the code to send the trigger signal is changed from
 
 ```C
        T1G_SetDigitalOutput();                 // send a short pulse
        __delay_us(5);
        T1G_SetDigitalInput();                  // return to input
 ```
 
to
 
 ```C
        TRIG_SetHigh();// Sends trigger pulse
        __delay_us(5);
        TRIG_SetLow();
 ```
 This change happens because we do not need to have the same pin count as input and output.
 
 __Note it would be better to use a hardware timer instead of delay_us(5); as delay could cause problems with hanging up the microchip and missing part of the return signal__
 
 The rest of the code is like Di Jasios
 
 We ran into a problem using puts(); the compiler would throw errors when attempting to use puts(); we changed to printf(); to avoid this error.
