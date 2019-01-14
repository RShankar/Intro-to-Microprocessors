This is an extension to project #5 page 55 of Lucio Di Jasio's "In 10 Lines Of code". 

 This extension displays on a four digit 7-seg display instead of the 2 digit used by Di Jasio.
 Also it is edited to work for a common cathode 7-seg display Di Jasio uses a common Anode.
 
 Before we start a warning:
 __DO NOT PLUG IN TO THE 5V or 3.3V PORTS THIS COULD DAMAGE THE DISPLAY__
 
 To Start with we should look at a section of the data sheet for the 3641AS used for this extension.
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display%20Common%20Cathode/Diagram%20Display.png "Data sheet")
 
 Picture Credited to: https://www.peterparts.com/CatalogPages/57/1007.pdf
 
 The 3641AS is a common cathode 7 segment display. This means we will use pin 12, 9, 8, and 6 to control which digit we are currently working on by setting one pin LOW and the others HIGH. The remainder of the pins are used to control which sections of the 7-segment are illuminated. For a common cathode we set the pins LOW that we need off and the pins we need on to HIGH allowing the power to flow from the segment pins that are HIGH to the common cathode pin that is LOW.
 
 For example, if we wanted to display '3' on the second digit we would set pin 9 LOW and pins 12, 8, and 6 HIGH. We would then set the pins that correspond to F, E, and DP (decimal point), pins 1, 10 and 3, to LOW and the remainder of the pins to HIGH.
 
 Now that we have some understanding of how the 7-seg display works I will show how to hook up the 7-segment display to the evaluation board.

 This method uses a printed circuit board, designed by FAU's lab manager Perry Weinthal, which will allow us to connect the 3641AS directly to the evaluation board
  
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display%20Common%20Cathode/1.jpg "New set up") 
 
  Notice with this click board set up that the decimal point side of the display is on the RB side of the evaluation board. You can wire the display anyway you want however the code provided here will not work.
  
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display%20Common%20Cathode/2.jpg "New set up") 
  
  ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display%20Common%20Cathode/3.jpg "New set up") 
  
  __DO NOT PLUG IN TO THE 5V or 3.3V PORTS THIS COULD DAMAGE THE DISPLAY__
  
  Now that the display is hooked up time to figure out which port on the board corresponds to what on the 7-segment display. The way I did it was to first write (Red text) the port that each pin was hooked up to on the upper pinout then transfer the ports down to the lower diagram (Blue text) to get a full representation of which port was controlling what.
  
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display%20Common%20Cathode/Diagram%20Display%20Marked%20Up.png "Pin Map")  
 
 From here we will move over to the MCC in the MPLAP IDE to reserve the pins on the board 
 
 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/Pin_Manager.JPG "Pin Manager")  

And then assign them how our program will see them. For this I used the blue text from our marked-up data sheet.
If you wired differently from me your pin module will look different from mine

 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display%20Common%20Cathode/Pin_Module.png"Pin Module") 
 
 Following the naming convention Di Jasio was using we should have labeled all our pins as above. 
 
 **Note** We are now useing C1 and C2 insteady of A1 and A2, Cathode instead of Anode
 
 Now that we have the pins set we must construct the proper CCDNC and CCDNB binary strings for the constant current control when driving the output low. We need the constant current control on the low pins which turn on Segments for Common Cathode those pins would be the common cathodes. To recap for the wiring used in this document the pins on the board that have a Cathode hooked up to them are RC7, RC5, RC4, and RB5. This is a total of 4 ports one for each digit. Now to construct CCDNC we simply set the bits high that we need current control on 10110000 and similarly for CCDPB 00100000
 
```C    
    CCDNC |= 0b10110000;//Enables constant current for pin RC7(C1) RC5(C2) and RC4(C3)
    CCDNB |= 0b00100000;//Enables constant current for pin RB5(C4)
```
 
 The last step is to extend Di Jasio's code for the 2 extra common cathodes
 
 Notice how only one Cathode (C1,C2,C3,C4) is set LOW at a time this controls which digit is being displayed at current. 
 
 ```C        
        digit=(ADCC_GetSingleConversion(POT)>>6);//the>>6 gives us 16 digits of freedom enough for 0-F
        //Note this code has been changed for a common cathode there for setting C#High turns off that digit and setting C#Low turns on that digit.
        C4_SetHigh();//turns off 4th digit
        C1_SetLow();//turns on 1st digit
        CCDCON=LIMIT_2mA;//currentlimit
        digitShow(digit);
        __delay_ms(5);
        
        C1_SetHigh();//turns off 1st digit
        C2_SetLow();//turns on 2nd digit
        CCDCON=LIMIT_5mA;//currentlimit
        digitShow(digit);
        __delay_ms(5);
                
        C2_SetHigh();//turns off second digit
        C3_SetLow();//turns on 3rd digit
        CCDCON=LIMIT_10mA;//currentlimit
        digitShow(digit);
        __delay_ms(5);
        
        C3_SetHigh();//turns off 3rd digit
        C4_SetLow();//turns on 4th digit
        CCDCON=LIMIT_NONE;//currentlimit
        digitShow(digit);
        __delay_ms(5);
 ```
The full project is attached above see SevenSeg.X.zip

As an even further extension we have added the full alphabet to the matrix in the file marked SevenSeg0ToVTest.X.zip

This changed the matrix provided by Di Jasio to Include the full Alphabet found here: https://en.wikichip.org/wiki/seven-segment_display/representing_letters

 ```C  
 uint8_t matrix[]={//Matrix that translates needed digit to a binary string to control which of the LEDs in the 7 segment are on and off
  //a  b  c  d  e  f  g
    1, 1, 1, 1, 1, 1, 0, //1
    0, 1, 1, 0, 0, 0, 0,
    1, 1, 0, 1, 1, 0, 1, //0
    1, 1, 1, 1, 0, 0, 1, 
    0, 1, 1, 0, 0, 1, 1, //4
    1, 0, 1, 1, 0, 1, 1, 
    1, 0, 1, 1, 1, 1, 1, //6
    1, 1, 1, 0, 0, 0, 0, 
    1, 1, 1, 1, 1, 1, 1, //8
    1, 1, 1, 1, 0, 1, 1, 
    1, 1, 1, 0, 1, 1, 1, //a
    0, 0, 1, 1, 1, 1, 1, 
    0, 0, 0, 1, 1, 0, 1, //c
    0, 1, 1, 1, 1, 0, 1, 
    1, 0, 0, 1, 1, 1, 1, //e
    1, 0, 0, 0, 1, 1, 1, //the Below code had been added to include G-Z to the seven segment display matrix
    1, 0, 1, 1, 1, 1, 0, //g
    0, 1, 1, 0, 1, 1, 1,
    0, 0, 0, 0, 1, 1, 0, //i
    0, 1, 1, 1, 1, 0, 0, 
    1, 0, 1, 0, 1, 1, 1, //K
    0, 0, 0, 1, 1, 1, 0, 
    1, 1, 0, 1, 0, 1, 0, //m
    0, 0, 1, 0, 1, 0, 1,
    0, 0, 1, 1, 1, 0, 1, //o
    1, 1, 0, 0, 1, 1, 1, 
    1, 1, 1, 0, 0, 1, 1, //q 
    0, 0, 0, 0, 1, 0, 1, 
    1, 0, 1, 1, 0, 1, 1, //s
    0, 0, 0, 1, 1, 1, 1, 
    0, 0, 1, 1, 1, 0, 0, //u
    0, 1, 0, 1, 0, 1, 0, 
    0, 1, 1, 1, 1, 1, 1, //w
    1, 0, 0, 1, 0, 0, 1, 
    0, 1, 1, 1, 0, 1, 1, //y
    1, 1, 0, 1, 1, 0, 1, 

};
 ```
