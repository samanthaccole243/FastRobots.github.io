### Lab 5
This lab task mainly consists of hardware with a bit of software. To start we were supposed to review the datasheets and 
documentation for our hardware. One of the important things to look at was pin functionality. For this lab we are hoping to 
connect motor drivers to the artemis along with working motors. These motors will be given a PWM signal to move them. 
This means short pulses that in theory average out to create a constant speed. When you look at the pinout diagram, 
you can see some pins have tildas next to them. In the documentation, it is made clear that this is to indicate pins capable 
of operating pwm signals. I chose pins A0, A1, A2, and A3, for my two motor drivers respectively. Each motor driver needs to be 
powered from Vin (from battery) and grounded. Each motor driver also has two inputs and two outputs. Technically there are four 
pins for the inputs and four pins for the outputs on the motor driver, but we shorted them to create two input pins and two 
output pins. This can be seen here:  
![two inputs and outputs](https://user-images.githubusercontent.com/89661904/224582904-477fa5ae-c47c-4b02-b55d-f3e6b6e310f2.jpg)

The first task is to finish the wiring of only one motor driver than test it to see it is working. I took one motor driver and shorted the two inner inputs to eachother with one long wire sticking out, then I shorted the outer inputs to each other with another long wire. I did the same with the outputs. I then soldered one input to A2 on the Artemis and the other input to A3 on the artemis. I then wrote a very small PWM code just initializing the pins as outputs and sending a pwm signal to them. Here is a photo of that code:
<img width="331" alt="pwm one motor" src="https://user-images.githubusercontent.com/89661904/224582924-01fae61c-7caa-45e5-b785-d61c0728a1dd.png">

As you can see I made one motor zero, and the other one 150. Technically the top speed is 255, but I chose to use 150 for testing purposes since I did not believe the top speed was necessary.
I then connected the inputs to the oscilliscope to se if they were receiving a proper PWM signal. This signal can be seen pictured on the oscilliscope screen here:
![oscilliscope](https://user-images.githubusercontent.com/89661904/224583074-c741ff84-2b69-44fd-a455-e158acfd68a7.jpg)

Next I took my car apart to get to the motor wires. I kept the 850mAh battery on the bottom side which powers the motors. This bottom side also has the battery that will power the artemis (650mAh). I removed the original pcb board and put the artemis in its place. I also cut a whole in the top of my car so I could have the ToF sensors which we discussed in previous labs peaking out. Next, I used soldered the motor driver to the battery connector, sticking through from the bottom of the car and the high of one motor to one output and the low of the same motor to the other output. This allows me to send one "high" (a speed), and the other "low" (zero) and have the motor move in one direction. If I reverse which output has the high and low signal, the motor then moves in the other direction. I then ran my code again and my motor moved as I expected! I then repeated the whole process with the second motor driver. The full car setup can be seen here:
![top car](https://user-images.githubusercontent.com/89661904/224583153-d5f6c722-8728-42b3-b202-ab7331356873.jpg)
![bot car](https://user-images.githubusercontent.com/89661904/224583160-127673d6-ede6-4917-9a1d-5385e6d2596e.jpg)

I also rewrote my code to include both motors, as can be seen here:
<img width="317" alt="pwm two motor" src="https://user-images.githubusercontent.com/89661904/224583171-e13eaa35-aa57-4a6a-965a-cf5f0460cf9d.png">

A video of both my wheels moving forward at the 150 pwm speed set in the code, can be seen here: 

<iframe width="560" height="315" src="https://youtube.com/embed/ePWHuilji8k?feature=share" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>



Next, I decided to explore the lower limit of my pwm. First I did this from stop. For the MENG task, I also did this while it was moving, since it will require more speed to start moving from stop then to just continue moving. To test the pwm lower limit from stop I simply kept lowering the pwm to the motors slowly until they would no longer start spinning at that speed. This number was approxiamately 35 for left side and 40 for the right. To figure out the lower limit while already moving, I started off with a pwm I knew would get the motors moving (50), then in the code, I continuously lowered it, and printed the pwm to the serial monitor, I ran the code and took note at which pwm the motors stopped spinning. The right motor significantly struggles at 30 and completely ceases all activity at 25. The left motor significantly slowed at 25 and ceased all activity at 20. A video of this can be seen here: ___video here__. As well as the serial monitor output here:
<img width="196" alt="pwm serial monitor" src="https://user-images.githubusercontent.com/89661904/224583214-d323b57f-1152-494a-a50f-9e396ea7f3fe.png">

For the MENG task, I was also asked to consider the effect the frequency for analogWrite to the motor has. Technically analogwrite only has one set frequency for this board, but we could mannually write out a pwm code. This is unnecessary as the current frequency is enough to power the motors. Writing manually allows more flexibility but can actually cause jiteriness when interupts are used. The analogWrite functipn will have no jitters even when interrupted.
Note I did both of these while the car was propped on a box, when the car is moving on the ground, in reality, my lower limit would be higher since there would be more resistance on the floor. This resistance would also change depending on the floor surface. I did a majority of the software portion of this lab at home, I have carpeting. The lab has linoleum flooring. These different materials would cause the motors to have different pwm lower limits.
The last part of this lab was to do a little course of my choice on the robot untethered. I decided my course was to go forward slowly, stop, turn right, turn left, then back up. I have a very thin hallway so I did kind of hit a wall doing this, but all in all it went well. A video of this taking place untethered can be seen here. __video___. 

