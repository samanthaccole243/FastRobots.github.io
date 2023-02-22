### Lab 4

The first task involves setting up the IMY. I ran a basic example that measured accelerometer, gyroscope, and magnetometer data. 
For now we will focus on the first two. The accelerometer measures acceleration while the gyroscope measures rate of angular change.
There is an AD0_val which has to do with the sensor address. This can be zero or 1. If I set mine to zero, data does not appear as expected. If I set the AD0_val to 1, the data seems to reflect how I move the sensor around.
I also added a visual indicator that the board is running which is my LED blinks twice upon the start of the code.

The second task involves the accelerometer. I first added equations to calculate pitch and roll to my code.
<img width="323" alt="pitch_and_roll_calculation" src="https://user-images.githubusercontent.com/89661904/220506122-8714d399-6a0e-4bd4-a9b4-9ad9f214e18f.png">

Below is the output when the IMU is flat:
<img width="313" alt="pitch_roll_0_0" src="https://user-images.githubusercontent.com/89661904/220506666-7d040adf-2534-4f76-b644-4f934b4299fd.png">

Rolling around the Y towards the negative X outputs a pitch of 0 and a roll of -90 as seen below:
<img width="409" alt="roll_90_pitch_0" src="https://user-images.githubusercontent.com/89661904/220506699-cfa5aa44-33c1-41fc-8d18-0afece82bc51.png">


Rolling around the X toward the negative Y outputs a roll of -90 and a pitch of 0 as seen below:
<img width="317" alt="roll_0_pitch_90" src="https://user-images.githubusercontent.com/89661904/220506765-83412dfc-68d1-4ceb-a75a-422146ca0518.png">

It can be seen above that the data is quite noisy. I ran my RC car next to my flat IMU and captured the noise:
