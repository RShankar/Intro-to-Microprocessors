 This is an extension to project #5 page 55 of Lucio Di Jasio's "In 10 Lines Of code"
 This extension displays on a four digit 7-seg display instead of the 2 digit used by Di Jasio.
 
 Before we start a warning:
 __DO NOT PLUG IN TO THE 5V or 3.3V PORTS THIS COULD DAMAGE THE DISPLAY__
 
 To Start with we should look at a section of the data sheet for the 5641BH used for this extension.
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/diagram%20display.png "Data sheet")
 
 Picture Credited to: http://idielectronica.blogspot.com/2016/02/button-press-counter-using-4-digit-7.html
 
 The 5641BH is a common anode 7 segment display. This means we will use pin 12, 9, 8, and 6 to control which digit we are currently working on by setting one pin high and the others low. The remainder of the pins are used to control which sections of the 7-segment are illuminated. For a common anode we set the pins High that we need off and the pins we need on to Low allowing the power to flow from the common anode pin that is high to the segment pins that are low 
 
 For example, if we wanted to display '3' on the second digit we would set pin 9 High and pins 12,8, and 6 low. We would then set the pins that correspond to F, E, and DP (decimal point), pins 1, 10 and 3, to high and the remainder of the pins to low.
 
 Now that we have some understanding of the 7-seg display I will show 2 ways to hook up the 7-segment display to the evaluation board.

 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/O1.jpg "Original set up")
 
 First is as above using the original method this method runs wires from the display to the evaluation board notice pin 12->7 are hooked up to the RC side of the board starting at RC7 to RC3. Then that pins 1->6 are hooked up similarly to the RB side of the board.
 
 You can wire the board in any order you wish however this code will only work with the ordering as seen in the picture.
 
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/O2.jpg "Original closeup display")
  
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/O3.jpg "Original closeup board")
  
  There is a second method that we will be using however that is much easier. This method uses a printed circuit board, designed by FAU's lab manager Perry Weinthal, which will allow us to connect the 5641BH directly to the evaluation board
  
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/N1.jpg "New set up") 
 
  Notice with this click board set up that the decimal point side of the display is on the RB side of the evaluation board. Again, you can wire the display anyway you want however the code provided here will not work.
  
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/N2.jpg "New set up") 
  
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/N3a.jpg "New set up") 
  
  __DO NOT PLUG IN TO THE 5V or 3.3V PORTS THIS COULD DAMAGE THE DISPLAY__
  
  Now that the display is hooked up time to figure out which port on the board corrosponds to what on the 7-segment display. The way I did it was to first write (Red text) the port that each pin was hooked up to on the upper pinout then transfer the ports down to the lower diagaram (Blue text) to get a full representation of which port was controling what.
  
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/diagram%20display%20marked%20up.png "Pin Map")  
 
 From here we will move over to the MCC in the MPLAP IDE to reserve the pins on the board 
 
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/Pin_Manager.JPG "Pin Manager")  

And then assign them how our program will see them. For this I used the blue text from our marked up data sheet.
If you wired differently from me your pin module will look different from mine

 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/Pin_Module.JPG "Pin Module") 
 
 Following the naming convention Di Jasio was useing we should have labled all our pins as above.
 ```C
         digit=(ADCC_GetSingleConversion(POT)>>6);
        A4_SetLow();//turns off 4th digit
        A1_SetHigh();//turns on 1st digit
        CCDCON=LIMIT_2mA;//currentlimit
        digitShow(digit);
        __delay_ms(5);
        
        A1_SetLow();//turns off 1st digit
        A2_SetHigh();//turns on 2nd digit
        CCDCON=LIMIT_5mA;//currentlimit
        digitShow(digit);
        __delay_ms(5);
                
        A2_SetLow();//turns off second digit
        A3_SetHigh();//turns on 3rd digit
        CCDCON=LIMIT_10mA;//currentlimit
        digitShow(digit);
        __delay_ms(5);
        
        A3_SetLow();//turns off 3rd digit
        A4_SetHigh();//turns on 4th digit
        CCDCON=LIMIT_NONE;//currentlimit
        digitShow(digit);
        __delay_ms(5);
 ```
