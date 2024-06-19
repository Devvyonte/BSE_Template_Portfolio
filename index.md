# Smile Detection Project
<!--
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
-->

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Ryan D | Wilcox High School | Computer Science | Incoming Junior |

<img src="images/Ryan.jpg" height="500" alt="Headstone Image">

<!--
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE
-->

# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Summary
  During this milestone, I was able to finish up, modify, and clean up my code. I made the program identify the face, and then identify whether they are smiling or not currently with displayed text as output. I also changed the boxes to match the status in color, so red for not smiling and green for smiling. Though not the most accurate, it works with decent efficiency and returns an acceptable output. However, I had to restart all my progress at some point since my SD card was fried. I installed 64-bit Raspbian (Raspberry Pi OS) this time and installed the software needed along with recording what I lost. After that, I also tried changing the aspect ratio of the output to a larger window, but it would not work since the Raspberry Pi's graphical power could not handle above 480p. 

## Challenges
  One of my most difficult challenges with the program and perhaps the most fatal one is when my Raspberry Pi stopped booting correctly. Somehow, one day my Raspberry Pi stopped working on boot saying the message that it could not open blockdev and was unable to mount root fs on unknown-block. I tried to use fsck but failed to do so, figuring out that my SD card was gone since it somehow had a broken pin.
So after that, I had to restart all my progress in downloading the firmware and software needed along with all my code. Luckily, flashing a new SD and installing Raspbian (Raspberry Pi OS) 64-bit was a lot easier than its 32-bit counterpart. I got all of my things working again almost flawlessly though I had a small trouble with installing OpenCV. It would error with the message that this environment was externally managed and would say that my OpenCV was already installed when it did not show up in ```pip list```. This was solved through some small research though, not taking that long with my eventual discovery of a StackOverflow post with the terminal command ```sudo mv /usr/lib/python3.11/EXTERNALLY-MANAGED /usr/lib/python3.11/EXTERNALLY-MANAGED.old```. After that, it was just figuring out how to make my code more accurate with the only challenge being how configurable the OpenCV library was. 

## Next Step
  My next step is to finalize the improvements in my code to make it more accurate and more efficient if possible with OpenCV configurations. I also plan to CAD and assemble a Pi Camera Stand so that my camera does not need a human hand to hold it anymore. I will most likely first print out prototypes and then finely refine the design to work for my purposes.  

## Code for Second Milestone

```python
import cv2;
from picamera2 import Picamera2;


face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades +'haarcascade_frontalface_default.xml')
smile_cascade = cv2.CascadeClassifier(cv2.data.haarcascades +'haarcascade_smile.xml')


picam2 = Picamera2()                                                                                                                                                                                 
picam2.configure(picam2.create_preview_configuration(main={"format": 'XRGB8888', "size": (640, 480)}))
picam2.start()


while True:
   frame = picam2.capture_array()
   gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
   faces = face_cascade.detectMultiScale(gray, 1.3, 5)


   for (x, y, w, h) in faces:
       cv2.rectangle(frame, (x, y), ((x + w), (y + h)), (255, 255, 255), 2)
       roi_gray = gray[y:y + h, x:x + w]
       roi_color = frame[y:y + h, x:x + w]
       smiles = smile_cascade.detectMultiScale(roi_gray, 1.8, 20)


       for (sx, sy, sw, sh) in smiles:
           if len(smiles) == 2:
               cv2.putText(frame, "Smiling", (x + 100, y - 30), cv2.FONT_HERSHEY_DUPLEX, 1.25, (0, 255, 0), 1, cv2.LINE_AA)
               cv2.rectangle(roi_color, (sx, sy), ((sx + sw), (sy + sh)), (0, 255, 0), 2)  # BGR
           else:
               cv2.putText(frame, "Not Smiling", (x + 45, y - 30), cv2.FONT_HERSHEY_DUPLEX, 1.25, (0, 0, 255), 1, cv2.LINE_AA)
               cv2.rectangle(roi_color, (sx, sy), ((sx + sw), (sy + sh)), (0, 0, 255), 2)


   cv2.imshow('Video', frame)


   if cv2.waitKey(1) & 0xff == ord('q'):
       break


picam2.stop()               
cv2.destroyAllWindows()
```

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/1HToM-Ea3wc?si=JWhQp1fXB9ZPbLfZ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Summary
  For my first milestone, I fully set up my Raspberry Pi, along with the following software I needed to accomplish my project. I started with installing (recording/streaming software) OBS on my Macbook to use as an external monitor for my Raspberry Pi as it did not come with one pre-installed. I then installed Raspbian (Raspberry Pi OS) 32-bit and ran ``` sudo apt update``` and ```sudo apt upgrade```. After that, I installed VSCode using ```sudo apt install code``` and upgraded it with ```sudo apt upgrade code``` and OpenCV, which was the AI recognition library that I needed for my project with much difficulty in the steps explained below. Finally, I fixed my broken camera and started to test some basic pre-written code I made on the side with a couple of tutorials while setting up the Raspberry Pi.

## Challenges
### First Challenge
  To download OpenCV, the AI library that I was going to use, it took many trials and research to get my final result after hours of working. Using the normal command which is ```sudo apt install python3-opencv``` did not work for me since I did not have pipwheel which returned the PEP 517 error, and could not build wheels. After about 9 hours of following different tutorials, waiting, failing, and retrying I figured out that it was not downloading since the OpenCV version I wanted to download was not the version my Raspberry Pi was compatible with. Eventually, I resorted to downloading an older version which worked out fine with the command ```pip install opencv-python==3.4.13.47```. This worked perfectly fine even though it was an older version of OpenCV, so don't be afraid to install older versions of software even if they may lack a few features. 
  
### Second Challenge
  After my OpenCV was downloaded, everything was fine, or so I thought. My Pi camera I figured, was USB and was therefore not compatible with the camera library built into the Raspberry Pi as that required a ribbon cable connection to the motherboard instead of an external USB connector. After I switched it, the camera worked fine. Unfortunately, later on, my Raspberry Pi failed me again, breaking my camera again and showing no camera detected when I tried with ```libcamera-hello --list-cameras```alternatively ```libcamera-hello list-cameras``` and also ```raspistill -o image.jpeg``` for trying to take a picture with the camera. After almost 9 more hours of debugging, I found out that I needed to change my config boot commands. I did this by typing ```sudo nano /boot/config.txt``` and adding ```camera_auto_detect=1``` & ``` display_auto_detect=1``` since I did not have them already for some reason (probably caused by my messing with the raspi-config settings and enabling/disabling legacy camera, so don't do this). After replacing my Pi camera to check for hardware faults and changing many settings for software faults which ended with my edition of the boot config code, I was able to get everything to work. 

## Next step
  My next step would be to edit and modify my code for efficiency and complication as it needed to be added on with other things and cleaned up a bit. I saw a previous example with the green and red text indicating whether someone was smiling or not which I thought was a great idea that I would like to try to implement in my way. Therefore I will also be working on floating text alongside fixing up the efficiency of my program so it will be more precise when it comes to displaying the correct output wanted. If I have time, I may dip into my third milestone which is adding a modification to my project to make it differ from others and to reduce the simplicity. 

# Starter Project

<iframe width="560" height="315" src="https://www.youtube.com/embed/qjpavTqujpw?si=7UYwX531yStZ8S3u" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Summary
  The starter project I chose was the BlueStamp Arduino Starter, which allows you to utilize and custom-build an Arduino. The Arduino can take both inputs in this case I chose a PIR sensor and an output which fed into my computer. To fully employ the Arduino, I sent the code to the module via the Arduino code editor which would be able to check whether the required input was given and display the respective text in my terminal. If the sensor identified motion, it would send inputs through the if statements I set up with an infinite loop to constantly check incoming data values and then display the result of motion detected in the console. If there was no more motion, it would check against the if statements to return with the statement of motion ending in the console. 

## Challenges
  During this process, it was difficult to get the result I wanted to achieve. Though sometimes it would give me a result, it was far too delayed to be a compatible solution. Thus I tried to re-wire and re-attach new PIR sensors to attempt to get the Arduino to produce the result I wanted. After many trials of replacing my code, wires, and PIR sensor I found the solution to be a specific PIR sensor that would allow me to adjust the delay of refreshing inputs and the sensitivity of the sensor. This ultimately solved my problem and allowed me to produce a decent result although with minor delay. Learning how to work with the Arduino and how to solder was challenging, however, ultimately was worth the effort put in. 

## Next Step
  My next step is to start working on my main project, Smile Recognition with OpenCV. I plan to install Raspbian (Raspberry Pi OS) and the respective software needed to start working on my code and testing of the code. 

## Schematics 
<img src="images/arduino_thingy.png" alt="Arduino schematic">

## Code for Arduino Starter

```c++
int led = 13;                // LED pin
int sensor = 2;              // PIR sensor pin
int state = LOW;             // default no motion detected
int val = 0;                 // sensor status, HIGH = on, LOW = off

void setup() {
  pinMode(led, OUTPUT);      // initalize LED
  pinMode(sensor, INPUT);    // initialize sensor
  Serial.begin(9600);        
}

void loop(){
  val = digitalRead(sensor);   
  if (val == HIGH) {           
    digitalWrite(led, HIGH);   
    
    if (state == LOW) {
      state = HIGH;       
      Serial.println("Motion detected!"); 
    }
  } 
  else {
      digitalWrite(led, LOW); 
      
      if (state == HIGH){
        state = LOW;       
        Serial.println("Motion stopped!");
    }
  }
}
//Credits: https://projecthub.arduino.cc/electronicsfan123/interfacing-arduino-uno-with-pir-motion-sensor-593b6b
```
<!---
# Code for Smile Recognition wth Python

```c++
  thingy
```
--->
# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Canakit Raspberry Pi 4 Starter Kit | Microprocessor to compute the imagining and code | $119.95 | <a href="https://www.canakit.com/raspberry-pi-4-starter-kit.html"> Link </a> |
| HDMI Video Capture | Captures the video input from the Raspberry Pi | $16.99 | <a href="https://www.ebay.com/itm/185388680755?chn=ps&srsltid=AfmBOoofEPDEGFSFFDB4o1QKpZQmjWtTZLxRGAVgQP8GFhlkUtHT_4WjYy4"> Link </a> |
| Pi Camera Module 3 | Gives a video or photo input to the Raspberry Pi | $35 | <a href="https://www.canakit.com/raspberry-pi-camera-module-3.html?cid=usd&src=raspberrypi"> Link </a> |
