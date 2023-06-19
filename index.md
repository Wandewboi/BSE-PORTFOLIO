# Pet Planter Project
A smart plant pot that can record humidity and temperature and upload that data to io.adafruit.com. It alerts the user when the soil is too dry or moist and the user can adjust the too-low or too-high levels using 5 pre-programmed profiles.
| Andrew B. | Sacred Heart Cathedral Prepratory| Aerospace Engineering | Incoming Sophmore

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone
My final milestone for my base project was the completion of a profile system, which allows the user to customize the water alert levels using 5 different pre-programmed profiles. I did this by prompting the user to input an integer 1-5, and based on that changing the alert values. The program also punishes the user with a very loud sound that doesn't stop until unplugged if they input anything other than 1,2,3,4 or 5. 

I initially tried implementing this solution with some touchscreen buttons because I thought my screen had touchscreen functionality. It didn't so now the user selects the setting based on keyboard input. This milestone marks the end of my core project, however, I still plan to add a self-watering system that will use an Arduino and valve.



<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Second Milestone
My second milestone is getting the planter software to work and interface with adafruit.io. I had to download a few libraries and download them onto the pcb's drive. I encountered quite a few issues in this step that led to almost a full day of troubleshooting. The first thing that I did wrong was updating the pcb to the incorrect version of circuit python. I fixed that by flashing a different version of circuit python. The real issue that I encountered was the default code that was provided in the kit. The first issue was with an argument name. In one of the setup folders, an argument was called aio_username, but in the code, it was called aio_name, something that took me a long time to catch. After I fixed that, I kept getting an issue that caused the pcb to  be unable to read sensor data, which caused the program to crash because ada fruit io was set up in a way where it would kick the user off if new data wasn't being added at least once every 60 seconds. This was solved by deleting a portion of faulty code. I also changed the low water warning to something a bit funnier. My next step is adding a profile system so the user can select what type of plant they have and have the water alerts change based on that.
<iframe width="560" height="315" src="https://www.youtube.com/embed/wMOQiFmWf6o" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# First Milestone
My first milestone is the assembly of my planters pcb, sensor, speaker and body. The first thing I did was assemble my pcb, which entalied plugging in some ribbon cables. My second process was attaching my sensor to a mounting mechanism and plugging in the cable that would attach to the pcb. I then assembled my planters body, which was 3d printed. I first attached the pot to the drip tray, then attached it to the housing. Then, I attached my sensor to the assembled body and attacehd the pcb and screen to the body. I then attached the back part to finish the physical aspect of this project.

The assembly was pretty straight forward and simple, except attaching the speaker cable to the pcb. The cable was exteremly short and was therefore very tense when attaching. It was also a very small and fragile cable, which would be very easy to break. My next step is programing the software for the planter.
<iframe width="560" height="315" src="https://www.youtube.com/embed/bPSWvVxIx5k" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Completion Of Starter Project
My first milestone is the completion of my starter project, that being the useless box. The function of the box is essentially to have no function (except perhaps pinching the user), as no items can be taken out or placed inside it. The box does this by contaning a switch that when flipped, causes a mechanical arm to be raised which hits the switch, lowering the arm and closing the box. The basic components of the box are the box itself, a pcb, a motor and a plastic arm. I had an issue while soldering components to the pcb which caused multiple short circuits. After I replaced the pcb, I had an issue with my motor, where it wasn't generationg enough torque to push the switch. I fixed this by replacing the motor. However, after doing this, I found that the motor was too powerful, causing the lid of the box to stay open. I solved this by putting some tape on the sides of the hinge.










# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
|:--:|:--:|:--:|:--:|

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
