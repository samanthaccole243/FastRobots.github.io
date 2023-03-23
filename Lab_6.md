### Lab 6

For this lab I did things a bit out of order for how the lab suggested.
I wrote and tested the PID on a non-bluetooth code. I used the PID formula as discussed in class. The P stands for proportional. This is basically a scaling factor for the error. The I stands for integral. A poitive error gives a positive integral under the curve. This will have the output increase. A negative error has a negative integral under the curve. This will make the output decrease. The D stands for derivative. The derivative of the error or change in error. Basically you want to see the error changing in the correct direction and how quickly. There exists only P controls, only I, PI, PD, and PID. As an MENG student I had to choose between PI and PID control. I chose to do PI for timing reasons. My PI control code can be seen implemented here:
<img width="554" alt="Screenshot 2023-03-22 235122" src="https://user-images.githubusercontent.com/89661904/227099288-6b125057-b3e2-48bc-874e-039ba380337b.png">

to choose my constant values for PI I first started with the Kp value and basically saw what did not cause my robot to go so fast that it hit the wall before seeing the distance. To choose my Ki value, I saw what value reduced oscillations the most.
Here are the parameters I ended up with: 
<img width="310" alt="parameters" src="https://user-images.githubusercontent.com/89661904/227099301-92c6bce5-72fc-46d1-8271-b0f39cabd13d.png">

You can also see in my code I attempted to use a wind-up pretection. This means if the error stays the same for too long my I term will not indefinitely build up or 'wind up' unnecessarily affecting the output in the same way. To protect against this, I created a limit for my i term, if it goes over the limit it gets returned back to that limit. This prevents the I term from increasing indefinitely.
To make sure the data sending works I implemented and tested sending IMU and TOF data over the bluetooth for a period of time.
I basically used the send IMU cases and send ToF data cases from previous labs and combined them into one case statement. I basically measured all the data for the time period and save it into arrays, after all my measurement is complete, I then send the data over bluetooth in small sets. I tested this and received all my data as expected.
I also rewrote my bluetooth file and the demo file so that it only has statements for a test of the bluetooth sending data, the sending of TOF and IMU data, and the PID/PWM motor stuff with data sending. I also edited my PID code to run at full speed and keep looking to see if my distance was less than 1 ft. When this happens I hault stop the motors. The coded for this can be seen here:
<img width="359" alt="1st part main loop" src="https://user-images.githubusercontent.com/89661904/227099319-08f5a4f9-e14a-4f95-8b78-0f8481c0841c.png">

<img width="282" alt="2nd part main loop" src="https://user-images.githubusercontent.com/89661904/227099327-18f17ed6-0cf3-4935-8b3e-2110af9b005b.png">


https://user-images.githubusercontent.com/89661904/227099362-dccafeb7-628a-4f11-a96d-a255cc2154f0.MOV


My windup control can be seen in the photo of my PID function above and is seen to be working since I do not have to change the values when I change floor surfaces. Here is a video on another surface: 



https://user-images.githubusercontent.com/89661904/227099384-aa4d14c1-f7ff-4cb8-a8e5-000152406462.MOV



ToF sensor wires broke (yes simultaneously on both ToF sensors) when I went to record these values. so no graphs yet - must fix hardware! :(
I also took all the data I sent over in the form of graphs. Here is a graph of the ToF data vs time: ___Graph here___
Here is a graph of the Motor input vs time __graph here__ To make this graph I also had the motor input sent over bluetooth.
I also sent over my I and P terms for debugging. These graphs can be seen here: __2 graphs here___
