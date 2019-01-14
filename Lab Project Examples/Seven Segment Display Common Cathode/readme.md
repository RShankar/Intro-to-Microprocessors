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

 ![alt text](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/Lab%20Project%20Examples/Seven%20Segment%20Display/Pin_Module.JPG "Pin Module") 
 
 Following the naming convention Di Jasio was using we should have labeled all our pins as above.
 
 Now that we have the pins set we must construct the proper CCDPC and CCDPB binary strings for the constant current control when driving the output low. We need the constant current control on the low pins for all the pins which have a Segment of the 7-segmnt display on them. To recap for the wiring used in this document the pins on the board that have a segment hooked up to them are RB0-RB4, RC2, RC3 and RC6. This is a total of 8 ports 7 for the digit and one for the decimal point. Now to construct CCDPC we simply set the bits high that we need current control on 01001100 and similarly for CCDPB 00011111
 
```C
    CCDPC |= 0b01001100;//Enables constant current for pin RC6(SEG_F) RC3(SEG_B) and RC2(SEG_A)
    CCDPB |= 0b00011111;//Enables constant current for pin RB4(SEG_G) RB3(SEG_C) RB2(SEG_DP) RB1(SEG_D) and RB0(SEG_E)
```
 
 The last step is to extend Di Jasio's code for the 2 extra common cathodes
 
 Notice how only one anode (A1,A2,A3,A4) is set LOW at a time this controls which digit is being displayed at current. 
 
 ```C        
        digit=(ADCC_GetSingleConversion(POT)>>6);// The >>6 gives us 16 digits of freedom enough for 0-F
        //Note this code has been changed for a common cathode there for setting A#High turns off that digit and setting A#Low turns on that digit.
        A4_SetHigh();//turns off 4th digit
        A1_SetLow();//turns on 1st digit
        CCDCON=LIMIT_2mA;//currentlimit
        digitShow(digit);
        __delay_ms(5);
        
        A1_SetHigh();//turns off 1st digit
        A2_SetLow();//turns on 2nd digit
        CCDCON=LIMIT_5mA;//currentlimit
        digitShow(digit);
        __delay_ms(5);
                
        A2_SetHigh();//turns off second digit
        A3_SetLow();//turns on 3rd digit
        CCDCON=LIMIT_10mA;//currentlimit
        digitShow(digit);
        __delay_ms(5);
        
        A3_SetHigh();//turns off 3rd digit
        A4_SetLow();//turns on 4th digit
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
