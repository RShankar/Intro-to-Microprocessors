 This is an extension to project #5 page 55 of Lucio Di Jasio's "In 10 Lines Of code". 

 This extension displays on a four digit 7-seg display instead of the 2 digit used by Di Jasio.
 
 Before we start a warning:
 __DO NOT PLUG IN TO THE 5V or 3.3V PORTS THIS COULD DAMAGE THE DISPLAY__
 
 To Start with we should look at a section of the data sheet for the 5641BH used for this extension.
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/diagram%20display.png "Data sheet")
 
 Picture Credited to: http://idielectronica.blogspot.com/2016/02/button-press-counter-using-4-digit-7.html
 
 The 5641BH is a common anode 7 segment display. This means we will use pin 12, 9, 8, and 6 to control which digit we are currently working on by setting one pin high and the others low. The remainder of the pins are used to control which sections of the 7-segment are illuminated. For a common anode we set the pins High that we need off and the pins we need on to Low allowing the power to flow from the common anode pin that is high to the segment pins that are low 
 
 For example, if we wanted to display '3' on the second digit we would set pin 9 High and pins 12, 8, and 6 low. We would then set the pins that correspond to F, E, and DP (decimal point), pins 1, 10 and 3, to high and the remainder of the pins to low.
 
 Now that we have some understanding of the 7-seg display I will show 2 ways to hook up the 7-segment display to the evaluation board.

 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/O1.jpg "Original set up")
 
 First is as above using the original method this method runs wires from the display to the evaluation board notice pin 12->7 are hooked up to the RC side of the board starting at RC7 to RC3. Then that pins 1->6 are hooked up similarly to the RB side of the board.
 
 You can wire the board in any order you wish however this code will only work with the ordering as seen in the picture.
 
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/O2.jpg "Original closeup display")
  
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/O3.jpg "Original closeup board")
  
  There is a second method that we will be using which is much easier. This method uses a printed circuit board, designed by FAU's lab manager Perry Weinthal, which will allow us to connect the 5641BH directly to the evaluation board
  
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/N1.jpg "New set up") 
 
  Notice with this click board set up that the decimal point side of the display is on the RB side of the evaluation board. Again, you can wire the display anyway you want however the code provided here will not work.
  
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/N2.jpg "New set up") 
  
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/N3a.jpg "New set up") 
  
  __DO NOT PLUG IN TO THE 5V or 3.3V PORTS THIS COULD DAMAGE THE DISPLAY__
  
  Now that the display is hooked up time to figure out which port on the board corresponds to what on the 7-segment display. The way I did it was to first write (Red text) the port that each pin was hooked up to on the upper pinout then transfer the ports down to the lower diagram (Blue text) to get a full representation of which port was controlling what.
  
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/diagram%20display%20marked%20up.png "Pin Map")  
 
 From here we will move over to the MCC in the MPLAP IDE to reserve the pins on the board 
 
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/Pin_Manager.JPG "Pin Manager")  

And then assign them how our program will see them. For this I used the blue text from our marked-up data sheet.
If you wired differently from me your pin module will look different from mine

 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/Pin_Module.JPG "Pin Module") 
 
 Following the naming convention Di Jasio was using we should have labeled all our pins as above.
 
 Now that we have the pins set we must construct the proper CCDNC and CCDNB binary strings for the constant current contriole when driving the output low. We need the constant current control on the low pins for all the pins which have a Segment of the 7-segmnt display on them. To recap for the wiring used in this document the pins on the board that have a segment hooked up to them are RB0-RB4, RC2, RC3 and RC6. This is a total of 8 ports 7 for the digit and one for the decimal point. Now to construct CCDNC we simply set the bits high that we need current control on 01001100 and simmilary for CCDNB 00011111
 
```C
    CCDNC |= 0b01001100;//Enables constant current for pin RC6(SEG_F) RC3(SEG_B) and RC2(SEG_A)
    CCDNB |= 0b00011111;//Enables constant current for pin RB4(SEG_G) RB3(SEG_C) RB2(SEG_DP) RB1(SEG_D) and RB0(SEG_E)
```
 
 The last step is to extend Di Jasio's code for the 2 extra common anodes
 
 Notice how only one anode (A1,A2,A3,A4) is set high at a time this controls which digit is being displayed at current. 
 
 ```C
        digit=(ADCC_GetSingleConversion(POT)>>6);//pulls digit from POT
        
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
The full project is attached above see SevenSeg.X.zip
