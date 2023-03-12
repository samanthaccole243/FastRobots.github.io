### Lab 5
This lab task mainly consists of hardware with a bit of software. To start we were supposed to review the datasheets and 
documentation for our hardware. One of the important things to look at was pin functionality. For this lab we are hoping to 
connect motor drivers to the artemis along with working motors. These motors will be given a PWM signal to move them. 
This means short pulses that in theory average out to create a constant speed. When you look at the pinout diagram, 
you can see some pins have tildas next to them. In the documentation, it is made clear that this is to indicate pins capable 
of operating pwm signals. I chose pins A0, A1, A2, and A3, for my two motor drivers respectively. Each motor driver needs to be 
powered from Vin (from battery) and grounded. Each motor driver also has two inputs and two outputs. Technically there are four 
pins for the inputs and four pins for the outputs on the motor driver, but we shorted them to creat two input pins and two 
output pins. This can be seen here:

