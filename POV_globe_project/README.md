<h1> :earth_asia:  Persistence of Vision (POV) Display  :earth_asia: </h1>

<h1> Team Members </h1>
- Didi Kamalova <br>
- Naomi Mo <br>
- Aanya Tashfeen <br>

<h1> Project Description </h1>
We created a spherical persistence of vision (POV) LED Display that works by spinning a circular array of LEDs and relies on our eyes' natural “refresh rates” to create the illusion of a solid image on a sphere. Equipped with an LED strip, a hall sensor, 3 battery packs and framed in a desk fan, it creates patterns upon reacting to magnets spaced out across the circular base.

<h1> Member Contribution </h1>
- Aanya: image graphics code, 3D modeling by editing STL files, round trip time code, mechanical assembly <br>
- Didi: led driver code, soldering, cable management, hardware assembly & sourcing <br>
- Naomi: hall sensor code, graphics code, hardware assembly and troubleshooting <br>

<h1> References </h1>
- POV Globe <a href="https://www.youtube.com/watch?v=E4yqSw38R_Q&t=178s](https://youtu.be/E4yqSw38R_Q">Video</a>, <a href="https://github.com/rottaca/PovGlobe.git">GitHub Repository</a>, and <a href="https://www.thingiverse.com/thing:4871230">Thingiverse (STL Files)</a> <br>
- SPI module code by <a href="https://github.com/cs107e/cs107e.github.io/blob/25d6d0b08f8accd1bdcaf4e400c9574a3f2c0dcf/lectures/Sensors/code/arducam/spi.c">Arducam</a> <br>
- Pat's hall effect sensor code <br>
- Image to C array website: https://notisrac.github.io/FileToCArray/

<h1> Self-Evaluation </h1>
<p> We created a fully functioning prototype of a spherical LED Display that allows for free spinning, coded an LED strip driver, integrated hall sensor interrupts and successfully projected a soccerball pattern on the sphere. While we have not been able to project a spherical image of the globe as was initally planned, we were able to complete all other goals that we have set for this project! </p>

One of the most memorable moments of this past week is definitely the moment we stumbled upon an interesting bug: the motor on our fan was generating a magnetic field which would induce current interfering with our circuitry, displaying weird artifacts and an undefined behavior on the strip. In attempts to block/redirect the magnetic field, we created a shield made out of thin stainless steel plates layered onto one another. However, this ended up trapping the heat and ultimately overheated the motor, making it no longer functionable... at 12:30AM, the night before the demo. Thankfully, we were able to find a different fan (shoutout to Frances!) to reinstall our ring onto a new fan 15 minutes before the demo session.


**Aanya**: I started off by editing the STL files to interface with the long rod we found. This involved figuring out how to edit an STL file on Fusion 360 and printing out hole testers to ensure we were going to print out the correct size. I also CADed the Pi and battery mounts to interface with the STL file. After mechanical assembly, I then moved on to understanding how to implement the POV effect. This started by using the working hall effect sensor code to calculate round trip time and use this code to determine what column of the image the LED strip should be displaying based on this data and the magnet readings. The tricky part for this was accounting for the non-equal distance of each magnet and then ensuring the code was constantly keeping track of changing columns. I then moved onto the graphics code to and display an image. Once I found the image to C array website, I used this array for the graphics code to iterate through the columns and drive the LEDs in this way, which is what we used to display the soccer ball. I also wrote the code to interface with the RTT code, but then we spent a lot of time trying to debug the magnetic field issue and couldn't really effectively test the graphics code on the spinning globe until we solved the artifacts issue.

**Didi**: Understanding how to drive an LED strip was not trivial; however, I felt comfortable navigating the datasheet for the APA102 communication protocol in the absense of reliable information about start/end bits sent to with the data pin! What helped me the most was using the logic analyzer to debug and experiment with data frames bit by bit (one of many useful skills learned in class!) and using a logic converter. I'm also happy with the electrical assembly of the display! I focused on placing our wires and circuit components in way that would look neat & help wires remain static during the rotation of the ring - mission accomplished!

**Naomi**: Implementing the hall sensor was relatively simple, as it only required three electrical connections, and I had Pat's hall sensor code to work with from the start (thank you Pat!). I built upon the existing code by adding interrupts so that sensor readings could be obtained while the Pi drove the LED strip; I also added debouncing so that magnet events would not be registered continuously in a magnetic field, and would instead only be registered by a change of state. After implementing the hall driver, I moved onto mechanical/electrical assembly; many nights these past few weeks were spent in Room 36 and Lab 64 working through hardware issues (the aforementioned magnetic field problems, power supply insufficiencies, fan stability, etc.). After all these issues, it was a relief to see the Pi spinning properly on demo day. It was also interesting to work through the logistics of powering and operating the Pi independently of the computer (I have developed a profound appreciation for the bootloader).

<h1> Photos </h1>

<p align="center">
  <img src="media/IMG_8513.jpg" title="LED Display" width = "500">
</p>
<p align="center">
  <img src="media/IMG_1285.JPG" title="LED Display" width = "250">
  <img src="media/IMG_8415.jpg" title="LED Display" width = "250">
  <img src="media/IMG_8499.jpg" title="LED Display" width = "250">
</p>

<p align="center">
  <img src="schematics/circuit.jpeg" title="schematics" height = "400">
</p>
More images provided in the "media" folder!

NOTE ABOUT CODE ORGANIZATION:
The simple code that we ran during demo day is under main, but more intricate implementations involving round trip time and displaying image arrays (the globe, soccer ball, and checkerboard) are under globe.c and RTTmeasure.c. We unfortunately did not get these to be fully optimized and integrated by the end of the project, although we made the soccer ball display operational after our demonstration.
