
There are four entries here, as of 4/28/2019:
1. "Copying Code with Syntax.md" by Doug Athenosy, one of the TAs for the course offering in spring 2019
2. "Using Word Equation for Logic.pdf" by Caner Mutlu, the second of the TAs for the course offering in spring 2019
3. Joshua Cidoni-Walker, a student in the class, has developed a video tutorial on creating a new project with MPLAB X IDE. Here is the link:
[MPLABX IDE Tutorial for Lab 4 (7Seg Display)](https://www.youtube.com/watch?v=XEMjPRKgYmw) 
4. "Tutorial on Hardware Debugging Using Curiosity Standard Board (DM164137)" by Tsz Shing Soi, another student in the class. 
5. "One page lab report example", posted by Doug Athenosy. This is a report submitted by one good student in the class, posted here as a good example to follow. 
6. "MCC Resolution Error In MPLAB X IDE" - Different windows get overlapped on a smaller screen device and ability to navigate through them is lost. This is the resolution writeup, posted by Doug Athenosy. Thanks to Akiva Green, a student in the class, for helping us locate the solution and trying it out first. He has a Surface Pro, which has it set to 200% by default.
7. Some compilation errors occur. Here is one [example](https://github.com/RShankar/Intro-to-Microprocessors/blob/master/General%20Tutorials/Compilation%20Error%20-%202019-04-12T03_04_28.630Z.jpg). Thanks to Daniel Martinez, a student in the course, for bringing it to our attention. Solution for this specific error, provided by Doug Athenosy: Go to ADCC.H and delete the following lines to fix this error (others will be similar - included here to show that the fixes are typically simple):

```
#ifndef int24_t
typedef signed long int int24_t;
#endif
These lines are 73 74 and 75
```

Here is some additional information:
1. Provided by Joshua Cidoni-Walker: An online free [course link](https://developerhelptraining.thinkific.com/courses/introduction-to-the-pic16f1-enhanced-mcu-architecture). Josh's comment: "this course offered by Microchip that pertains to most of the topics we are/will be covering in the course (based off of the syllabus). It is free to enroll, and offers very concise and compact information--very useful!"
2. 
