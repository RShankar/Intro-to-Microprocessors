The NeoPixel will not be discussed in this GitHub please see https://github.com/RShankar/Intro-to-Microprocessors/tree/master/Lab%20Project%20Examples/NeoPixel%20LED

Spec sheet for our SG-90 can be found here: http://akizukidenshi.com/download/ds/towerpro/SG90.pdf

Using the servo at a high clock speed presents an interesting problem. The PWM used to drive the servo must run off Timers 2, 4, or 6 and the PWM gets wired in before the post scalar. This means the maximum timer period you can get for a PWM is 2.48ms not our needed 20ms. Below is a work around for this problem that uses an additional timer.

First, we will set the clock speed to the required speed to use the NeoPixel below

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Using%20The%20Servo%20with%20a%20Neopixel/S1.png)


Next, we will set Timer 4, Timer 2 would work just as well, to be a roll over pulse and use the post-scaler to get our period of 20ms. This will give us our required period of 20ms.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Using%20The%20Servo%20with%20a%20Neopixel/S2.png)

Next we will use Timer 4's post-scaler as a trigger for Timer6 set as a monostable pulse of length 2ms. This gives us a 2ms pulse riding on a 20ms period. This is exactly what we need for our max 90 position.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Using%20The%20Servo%20with%20a%20Neopixel/S3.png)


Lastly we still need the PWM to Modulate our 2ms pulse at 100% or PWM7_LoadDutyValue(499); you should be at 90+ then if you modulate so only 50% of the pulse is on you should get a 1ms pulse and get out -90.

![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Using%20The%20Servo%20with%20a%20Neopixel/S4.png)


As we have seen in class this is not exact and you may wish to further experiment with the timer length of the Timer 6 make sure that the 2ms is the largest value needed.
I have already found that the 50% does not return the desired angle and have found 180 degree of movement to be about 
PWM7_LoadDutyValue(499); to PWM7_LoadDutyValue(100); which is the PWM going from 100% to 20%
