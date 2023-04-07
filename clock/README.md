
The clock involved building a breadboard for a clock and then using the Pi to turn the clock on and count upwards. I then added two buttons to allow for the clock time to be adjusted and how this works is defined below. I really enjoyed this assignment as you could see a physical output pn the clock and use this physical output to debug. The unit tests were a helpful way to debug code and ensure proper functionality for the gpio and timer libraries. To work out the register numbers, I used the Broadcom ARM Peripherals Manual.

User guide for two-button interface:

Red button is on the left
Blue button is on the right.

To start the clock click the red button.

The display flashes, so you're now in set mode.

Set the time - the red button controls minutes and the blue button controls seconds. You can only go up in time.
Reset if you go to high by holding down blue button.

Don't click each button for too long because holding the buttons down for at least 2 seconds has special functionality.

In set mode:

Holding red button for 2 seconds or more goes into start mode.
Holding blue button down in set mode for 2 seconds resets clock to 00 00.

In start mode:

Clock starts counting upwards from set time.
Click red button once to pause time and go from start mode to set mode. The time will pause.
