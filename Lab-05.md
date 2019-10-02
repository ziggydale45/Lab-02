# Johnway in the Box
For this week’s lab, we will be building a Jack in the box; this is a project inspired by the known toy. We will use this lab to help you to experiment with digital fabrication tools. The methods that will be used are 3D printing and laser cutting. Video of similar box

## In the report
To submit your lab, clone this repository -- and include all files / images / code that is requested!

## Laser Cutting
Laser cut cardboard to make your box in the Maker Lab.

Download a vector editing program like Inkscape (free) or Adobe Illustrator (free for 30 day trial).
On this page, download the PDF (boxTall.pdf) and the STL files.
Open the laser cutter template file (PDF) for the Box in your vector editing program (i.e. Ink scape).
Add holes for the servo mount, and Arduino wires. This time, make sure you don't use images, but instead vectors. Make sure the all lines that you want the printer to recognize are 0.001pt thick and the proper color (red= 255, green= 0, blue =0) for cutting. Also make sure that the page size is the same size as your cardboard (or you will have to change the home on the laser cutter). Save your file as a PDF. BONUS: include lines or images that you don't plan to cut all the way through to experiment with etching.
To laser cut, open your modified file in Adobe Illustrator on the lab’s computer. Look around the laser cutting room for instructions, reference sheets, and scrap materials. The step by step instructions are attached on the suction system to the left of the computer.
Keeping in mind Niti's safety instructions, follow the instructions to cut (these are summarized for our purposes):
Load the machine with the 5/32" thick cardboard we provided. If the material is bent, tape the ends using duct tape to the sides of the printing bed to make it as flat as possible.
Disable X/Y.
Move the laser to its starting position on top left corner of the material.
Focus the laser using the focus tool and up and down arrows. Flip the focus tool up again after you're done.
Press the set home button.
Close the lid.
Open the printer preferences.
Make sure you set the different power levels for the cut values pertaining to the material you're using.
For the cardboard we are providing, the values should be: Speed 45%, Power 70%, and Frequency: 500Hz. On the same window, adjust the printing bed size to 24" horizontal, and 18" vertical. When you save the settings, make sure the image on the preview is well positioned (not too close to the edges and fitting well in the space). Under Page Sizing and Handling, click actual size. Press print.

Turn on the air assist compressor on the floor on.
Turn the suction system, the big blue box, on.
Print the job on the computer.
Find the job you're printing on the laser cutter, and press 'go'.
Assemble the parts. Make sure the holes for the servo mount, and Arduino wires fit. Once the configuration makes sense, hot glue them together. Pay attention that part “D” is the top of the box and should not be hot glued- you can attach it with tape or or some other hinge.
Notice that part G is not part of the Box itself. It will be used as the top lifter.

Picture1

## 3D Printing
3D print this servo mount stl file:

Download and install Ultimaker Cura.
Import the .stl file from the files you downloaded into the printer software.
Make sure the orientation of your part makes sense. What orientation makes the most sense for 3D printing?
Turn off the raft. There is no need to print a raft for this part.
Connect your laptop to the printer over USB, or via WiFi. Ask any member of the teaching team for WiFi credentials.
Once the Printer is connected hit "print".

## Electronics
electronics circuit

Tip: If you don't have the 9V connector, you just need to make sure that the micro controller is plugged into your computer, for power.

## Program your device
Load the example previously downloaded.

You can also make your own program but make sure you put HIGH digital value to pin 5 if you connected the circuit as the one in the electronics part.

Pay attention that you can change the position of close and open box in the following lines:

#define closePos 10

#define openPos 110

## Putting it all together
Think about where each component should go, and assemble your box so it would work as the one in the video from the beginning.

## Create Jack
To make the character in the box a 3D printed part:

Create a free education OnShape account using your student email.
Do the sketching tutorial and part design tutorial to learn the basics of Computer Aided Design (CAD) on OnShape.
Create a character to 3D print.
To make the character in the box a laser cut part:

Create a free education OnShape account using your student email.
Do the sketching tutorial and part design tutorial to learn the basics of Computer Aided Design (CAD) on OnShape.
Create a 3D character
Use the KiriMoto app from the OnShape app store (it’s free to edu users) to slice the shape into laser cuttable parts.

## Lab Submission
For your write up, include:

Your Arduino code.
```
//  Box Lab 5
//
// If we see a voltage change on pin 2 the toggle switch on top of the useless box has 
// changed position and we need to react!
//    A HIGH value on pin 2 means we should activate the servo to open the useless 
//    box and attempt to return the switch to the "off" position.
//    A LOW value on pin 2 means the switch is off and we should return to our 
//    inital (closed box) state.

#include <Servo.h> 

#define servoPin  10
#define switchPin 2

#define closePos  10
#define openPos   110

Servo servo;
int switchState;
int previousSwitchState;

// call this when the input on pin 2 changes (LOW to HIGH *or* HIGH to LOW)
void ToggleSwitch(int switchState)
{    
  if (switchState == HIGH)
  {
    servo.write(openPos);
    //Serial.println("switch state is HIGH.  servo.write(openPos) called to open useless box");
  }
  else
  {
    servo.write(closePos);
    //Serial.println("switch state is LOW.   servo.write(closePos) called to close useless box");
  }
  previousSwitchState = switchState;  // remember that the switch state has changed 
}

void setup()
{
  //Serial.begin(9600);
  //Serial.println("Useless Box Lab 5");
  pinMode(5,OUTPUT);
  digitalWrite(5,HIGH);
  // start with the box closed and the switch in the off postion
  switchState = LOW;
  previousSwitchState = LOW;

  // connect to our servo and make sure it is in the closed position
  servo.attach(servoPin);
  servo.write(closePos);

  // we should probably pay attention to the switch
  pinMode(switchPin, INPUT); 
}

void loop()
{ 
  int switchState = digitalRead(switchPin);
  if (switchState != previousSwitchState)
    ToggleSwitch(switchState);

  delay(20);
}
```

.stl or .svg files for your Jack — if you use some other technique, include the respective supporting material.

At least one photo of your box taken in the MakerLab's Portable Photo Studio (or somewhere else, but of similar quality).

A video of your box in action.
