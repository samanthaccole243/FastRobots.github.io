### Lab 6

For this lab I did things a bit out of order for how the lab suggested.
I wrote and tested the PID on a non-bluetooth code. I used the PID formula as discussed in class. The P stands for proportional. This is basically a scaling factor for the error. The I stands for integral. A poitive error gives a positive integral under the curve. This will have the output increase. A negative error has a negative integral under the curve. This will make the output decrease. The D stands for derivative. The derivative of the error or change in error. Basically you want to see the error changing in the correct direction and how quickly. There exists only P controls, only I, PI, PD, and PID. As an MENG student I had to choose between PI and PID control. I chose to start with PID, then if I found this too challenging reduce it to PI if neccessary. My PID control code can be seen implemented here:
__photo here__ ___Did I reduce to PI? if so, photo here___
to choose my constant values for PID I used the method as described on ___whatever site___ ___discuss PID method here__  
Here are the parameters I ended up with: ___photo of ending numbers here___
You can also see in my code I attempted to use a wind-up pretection. This means if the error stays the same for too long my I term will not indefinitely build up or 'wind up' unnecessarily affecting the output in the same way. To protect against this, I created a limit for my i term, if it goes over the limit it gets returned back to that limit. This prevents the I term from increasing indefinitely.
To make sure the data sending works I implemented and tested sending IMU and TOF data over the bluetooth for a period of time. __enter time here__.
I basically used the send IMU cases and send ToF data cases from previous labs and combined them into one case statement. I basically measured all the data for the time period and save it into arrays, after all my measurement is complete, I then send the data over bluetooth in small sets. I tested this and received all my data as expected.
I also rewrote my bluetooth file and the demo file so that it only has statements for a test of the bluetooth sending data, the sending of TOF and IMU data, and the PID/PWM motor stuff with data sending. I also edited my PID code to run at full speed and keep looking to see if my distance was less than 1 ft. When this happens I hault any calculations and immediately stop the motors. 
___here is a video of this being implemented__
My windup control can be seen to be working since I do not have to change the values when I change floor surfaces. Here is a video on another surface: __video here___
I also took all the data I sent over in the form of graphs. Here is a graph of the ToF data vs time: ___Graph here___
Here is a graph of the Motor input vs time __graph here__ To make this graph I also had the motor input sent over bluetooth.
