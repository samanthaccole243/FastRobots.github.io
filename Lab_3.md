## Lab 3

Much of this lab was spent soldering the Time of Flight sensors to the QWIIC cables. I planned ahead by deciding to cut the longer cables so that I can have freedom to place the sensors on the robot rather than being limited by the cable length.
A single ToF sensor looks like this:

I used the QWIIC breakout board as an intermediary between the ToF sensor and the artemis board. This allows me to plug more than one sensor into the port on the board. This 4-way connector QWIIC breakout board can be seen here:

As said above I cut one side of each long wire and soldered the wires directly to the ToF sensors. The red wire is Vin, the black wire is ground, the yellow wireis SCL, and the blue wire is SDA. These lables pins are all clearly labeled on the ToF sensor. The first task of the lab was only to run a single sensor at once, but I figured I could get the soldering of the cables on both ToF sensors out of the way and then just not plug the second sensor in till later. The whole setup can be seen below:

I did make an additional adjustment later with soldering which can be seen in this photo (the purple wire), but I will why this addition was neccessary later.
Next, I ran the example code, 'Example1_wire_I2C.ino'. I first chose to run the sensor in the default distance mode just to see if it was functioning appropriately. This code did not work! ah! It seems like the board was getting stuck in a loop waiting for data from the sensor to be received. Turns out the port on my Artemis board was broken. I first tried bypassing the QWIIC breakout board to see if that was the issue, but the sensor still did not work. I also noticed that the QWIIC breakout board was lighting up on other students setups. This led me to try a new Artemis board, to see if my Artemis was the issue. It was. I have not used this port befor, so it is hard to say if I did something to break it or if the board came with a broken port. I have been using the new board since and have not had any issues. I then ran a series of test to compare accuracy between modes,  and if the range affected the accuracy, as well as the sensor range, repeatability, and ranging time.
