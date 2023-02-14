## Lab 3

Much of this lab was spent soldering the Time of Flight sensors to the QWIIC cables. I planned ahead by deciding to cut the longer cables so that I can have freedom to place the sensors on the robot rather than being limited by the cable length.
I used the QWIIC breakout board as an intermediary between the ToF sensors and the artemis board so I could later plug more than one sensor into the port on the board. 
As said above I cut one side of each long wire and soldered the wires directly to the ToF sensors. The red wire is Vin, the black wire is ground, the yellow wireis SCL, and the blue wire is SDA. These lables pins are all clearly labeled on the ToF sensor. The first task of the lab was only to run a single sensor at once, but I figured I could get the soldering of the cables on both ToF sensors out of the way and then just not plug the second sensor in till later. The whole setup can be seen below:![IMG_6886](https://user-images.githubusercontent.com/89661904/218805187-22d05471-366b-4259-9303-11c7b512d9da.jpg)
The empty port cable would be connected to the Artemis Board.

I did make an additional adjustment later with soldering which can be seen in this photo (the purple wire), but I will why this addition was neccessary later.
Next, I ran the example code, 'Example1_wire_I2C.ino'. I first chose to run the sensor in the default distance mode just to see if it was functioning appropriately. This code did not work! ah! It seems like the board was getting stuck in a loop waiting for data from the sensor to be received. Turns out the port on my Artemis board was broken. I first tried bypassing the QWIIC breakout board to see if that was the issue, but the sensor still did not work. I also noticed that the QWIIC breakout board was lighting up on other students setups. This led me to try a new Artemis board, to see if my Artemis was the issue. It was. I have not used this port befor, so it is hard to say if I did something to break it or if the board came with a broken port. I have been using the new board since and have not had any issues. The board first prints the ToF address as can be seen here:
![address  part 4](https://user-images.githubusercontent.com/89661904/218786842-7ea15503-3885-434f-b466-5787fa763b3a.PNG)

This is expected because the datasheet informs us that this will be the address of all ToF sensors.
A screenshot of the serial monitor output for the example code with default settings can be seen here:
![distance single sensor](https://user-images.githubusercontent.com/89661904/218786884-452cff1c-7ee1-48d0-ab66-1bc572e2ce4d.PNG)

I then ran a series of test to compare accuracy between modes,  and if the range affected the accuracy, as well as the sensor range, repeatability, and ranging time.

### Explain tests and results here

Next, we were tasked with running two ToF sensors at once. Both sensors have the same address 0x29 which we initially confirmed using the first sensor. To use both sensors at once, I needed to turn on sensor off, change the other sensors address, then turn the first sensor back on. Luckily there is a shutoff pin located on the ToF sensor. I soldered an additional purple wire from the shuttof pin of one sensor to a digital pin on the Artemis board (I chose pin 8 but many other pins could have worked). The code below explains how I got the two sensors working together:

A full wiring diagram can be seen here:
![IMG_1139](https://user-images.githubusercontent.com/89661904/218803154-35f3a3cb-eb44-4b38-bf9d-a26b6b3d0dfe.jpg)

Serial monitor output showing both sensors working together can be seen here:


I then performed series of tests with my 2 ToF sensors running to again compare accuracy, range, reliability, and ranging time.

### Explain tests and results here

### Answer Q 8,9 

## MENG question



