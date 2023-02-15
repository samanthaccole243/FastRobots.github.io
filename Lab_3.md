## Lab 3

Much of this lab was spent soldering the Time of Flight sensors to the QWIIC cables. I planned ahead by deciding to cut the longer cables so that I can have freedom to place the sensors on the robot rather than being limited by the cable length.
I used the QWIIC breakout board as an intermediary between the ToF sensors and the artemis board so I could later plug more than one sensor into the port on the board. 
As said above I cut one side of each long wire and soldered the wires directly to the ToF sensors. The red wire is Vin, the black wire is ground, the yellow wireis SCL, and the blue wire is SDA. These lables pins are all clearly labeled on the ToF sensor. The first task of the lab was only to run a single sensor at once, but I figured I could get the soldering of the cables on both ToF sensors out of the way and then just not plug the second sensor in till later. The whole setup can be seen below:![IMG_6886](https://user-images.githubusercontent.com/89661904/218805187-22d05471-366b-4259-9303-11c7b512d9da.jpg)
The empty port cable would be connected to the Artemis Board.

I did make an additional adjustment later with soldering which can be seen in this photo (the purple wire), but I will explain why this addition was neccessary later.
Next, I ran the example code, 'Example1_wire_I2C.ino'. I first chose to run the sensor in the default distance mode just to see if it was functioning appropriately. This code did not work! ah! It seems like the board was getting stuck in a loop waiting for data from the sensor to be received. Turns out the port on my Artemis board was broken. I first tried bypassing the QWIIC breakout board to see if that was the issue, but the sensor still did not work. I also noticed that the QWIIC breakout board was lighting up on other students setups. This led me to try a new Artemis board, to see if my Artemis was the issue. It was. I have not used this port befor, so it is hard to say if I did something to break it or if the board came with a broken port. I have been using the new board since and have not had any issues. The board first prints the ToF address as can be seen here:
![address  part 4](https://user-images.githubusercontent.com/89661904/218786842-7ea15503-3885-434f-b466-5787fa763b3a.PNG)

This is expected because the datasheet informs us that this will be the address of all ToF sensors.
A screenshot of the serial monitor output for the example code with default settings can be seen here:
![distance single sensor](https://user-images.githubusercontent.com/89661904/218786884-452cff1c-7ee1-48d0-ab66-1bc572e2ce4d.PNG)

I then ran a series of test to assess accuracy, range, repeatability, and ranging times for the sensor.

For these test, I used my over 3ft long coffee table. I carefully measured and marked certain Measurements. Then ran the ToF sensor to gather data. I did 5 full trials for each measurement then took the average results of these trials. Here are my results:
<img width="455" alt="accuracy" src="https://user-images.githubusercontent.com/89661904/218943798-e4eee374-8b88-4a10-9ef3-5d7b7b55540c.png">
<img width="455" alt="reliability" src="https://user-images.githubusercontent.com/89661904/218943819-d9db24c2-5eb5-499f-ba1d-bf9b9b17121a.png">

Ranging: You can already see that the ToF sensor does not work well below 3 inches. I tried to gather a measurement for the long range, but I did not have a long enough table. Judging by the documentation, I might guess that the sensor begins giving faulty measurements just under 4m (13.12ft).
For accuracy I merely compared the ToF reading when I placed a book at each marker to the actual distance hand measured by me at that marker. You can see that the ToF is extremely accurate within its range.
For Reliability, I compared the standard deviations of all of these measurements. You can again see the sensor does not deviate much from the mean of the data when within range, meaning it is not giving many (or any) outliers in data. At 1 inch, the standard deviation is zero, solely because the sensor read zero even though the distance was not zero... At 2 inches, you can see the standard deviation is higher than the others because this measurement is outside the ToFs range and causes the ToF to give false readings.
To measure Ranging time, I simply took note of the time in milliseconds at the beginning of the loop and took the time at the end of the ranging and measured this. I did this again but now while leaving out the stopranging portion of the code. Here are my results: 
<img width="227" alt="rangingtime" src="https://user-images.githubusercontent.com/89661904/218943847-4fe8383e-2a83-4572-b3d4-b9b7887917e3.png">

They were subrisingly quite similar.
Next, we were tasked with running two ToF sensors at once. Both sensors have the same address 0x29 which we initially confirmed using the first sensor. To use both sensors at once, I needed to turn on sensor off, change the other sensors address, then turn the first sensor back on. Luckily there is a shutoff pin located on the ToF sensor. I soldered an additional purple wire from the shuttof pin of one sensor to a digital pin on the Artemis board (I chose pin 8 but many other pins could have worked). The code below shows tidbits of how I got the two sensors working together:
<img width="234" alt="code tidbit" src="https://user-images.githubusercontent.com/89661904/218944645-420911f3-9811-4f80-bbda-82b824ab65ea.png">
The first line enables my ToF1 shutdown pin (pin8) as an output. The second line sets it to low (which shuts off ToF1). The fourth line changes the address of ToF2 and the sixth line turns ToF1 back on. The delays are just to make sure there is time to assure shutdown before changing the other address and then assure the address is changed before turning the other back on.


Serial monitor output showing both sensors working together can be seen here:
<img width="292" alt="2 sensors working" src="https://user-images.githubusercontent.com/89661904/218944620-7db72a27-5ecf-4353-a5a7-b4383540b195.png">


A full wiring diagram can be seen here:
![IMG_1139](https://user-images.githubusercontent.com/89661904/218803154-35f3a3cb-eb44-4b38-bf9d-a26b6b3d0dfe.jpg)

We were also asked to write code so that the clock is printed repeatedly and the sensor data is only printed when ready. This means the code is not blocked waiting on the sensor to be ready. My serial monitor output for this code can be seen below. Notice how I have multiple instances where the time is printed before a sensor reading interrupts that reading.
<img width="371" alt="see lag" src="https://user-images.githubusercontent.com/89661904/218949363-85063f7d-99e3-4ca2-bccd-e7e8fd2862b8.png">

Finally, I combined what I learned in lab 2 with what I learned in lab 1. I made it so that over bluetooth I could see timestamped ToF data for a period of 5s of measuring. 
I actually just copied the setup and import/define/initialization statements outside the main loop from my ToF sensor code, then made a command for to measure time and distance and save each set in an array then sent packets of that information over bluetooth from my artemis board to my commputer. 


## MENG question
Another sensor similar to ToF which functions off of infrared transmissions is an ultrasonic sensor. The ToF sensor uses timed pulses of light and their reflection to measure distance. An ultrasonic sensor uses timed pulses of sound and measures its return to gather ditance information.
Ultrasonic sensors have a shorter range, worse accuracy outside its range, and performs longer readings (light travels faster than sound). This means ToF is better in all these areas. Unfortunately ToF does have its downfalls. Colors reflect different amounts of light and mishapen items reflect light in odd directions. A color reflecting too much light may give false readings and light reflected in the wrong direction could also cause false readings. This also means if a room is too bright the readings could be inaccurate. the ToF needs to have be able to measure the reflection of the light it sent and not some other ray.
