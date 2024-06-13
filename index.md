# Smile Detection Project
<!--
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
-->

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Ryan D | Wilcox High School | Computer Science | Incoming Junior |

![Headstone Image](images/Ryan.HEIC)

<!--
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 

# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your first milestone, describe what your project is and how you plan to build it. You can include:
- An explanation about the different components of your project and how they will all integrate together
- Technical progress you've made so far
- Challenges you're facing and solving in your future milestones
- What your plan is to complete your project
-->
# Starter Project

<iframe width="560" height="315" src="https://www.youtube.com/embed/qjpavTqujpw?si=7UYwX531yStZ8S3u" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

The starter project I chose was the BlueStamp Arduino Starter, which allows you to utilize and custom-build an Arduino. The Arduino can take both inputs in this case I chose a PIR sensor and an output which fed into my computer. To fully employ the Arduino, I sent the code to the module via the Arduino code editor which would be able to check whether the required input was given and display the respective text in my terminal. If the sensor identified motion, it would send inputs through the if statements I set up with an infinite loop to constantly check incoming data values and then display the result of motion detected in the console. If there was no more motion, it would check against the if statements to return with the statement of motion ending in the console. During this process, it was difficult to get the result I wanted to achieve. Though sometimes it would give me a result, it was far too delayed to be a compatible solution. Thus I tried to re-wire and re-attach new PIR sensors to attempt to get the Arduino to produce the result I wanted. After many trials of replacing my code, wires, and PIR sensor I found the solution to be a specific PIR sensor that would allow me to adjust the delay of refreshing inputs and the sensitivity of the sensor. This ultimately solved my problem and allowed me to produce a decent result although with minor delay. Learning how to work with the Arduino and how to solder was challenging, however, ultimately was worth the effort put in. 

# Schematics 
<img src="images/arduino thingy.png" alt="Arduino schematic">

# Code for Arduino Starter

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

# Code for Smile Recognition wth Python
<!---
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
