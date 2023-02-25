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

It can be seen above that the data is quite noisy. I ran my RC car next to my flat IMU and captured the noise for both pitch and roll then I took an fft of both data. Below are these graphs. It can be seen that there are no frequencies where the noise is predominantly present. I took this to mean that I did not need to make an RC filter.
<img width="401" alt="pitch noise and fft" src="https://user-images.githubusercontent.com/89661904/221075351-6a3ed319-18e7-425d-9fb6-588be0504c8b.png">
<img width="388" alt="roll noise and fft" src="https://user-images.githubusercontent.com/89661904/221075358-43fd4018-ce98-4f63-9b40-76bc4aaecea2.png">

The next part of lab was regarding the gyroscope. The same process was performed. I measured the data near the RC while it was running and tried to do an fft to see if there was a frequency that I should attempt to filter. Below are my results:
<img width="397" alt="fft_gryo_pitch" src="https://user-images.githubusercontent.com/89661904/221371203-205344ad-3df0-4237-83f5-0fd9b50a7f70.png">
<img width="400" alt="fft_gryo_roll" src="https://user-images.githubusercontent.com/89661904/221371206-30c7dae4-b691-425c-bb69-8635b2e1dd27.png">
<img width="388" alt="fft_gryo_yaw" src="https://user-images.githubusercontent.com/89661904/221371209-7ecf0dfd-da8c-42c3-9674-bdc6d71dca40.png">

I performed an fft the same way I did on the accelerometer data but somehow the fft for the gyro data doesnt even seem like an fft.
This level of noise informs me I again do not need a filter to "clean" my data.

The Fourth portion of the lab was regarding speeding up data collection. Unlike lab 3, this data is not set on a loop waiting for new data, it instead uses an if statement to check for data. This is not blocking like the previous code was. This code does however send you to an else that has you delay and print "waiting for new data". Since, I no longer want to wait, I commented out this portion. Now do calculations on the raw data if it is ready otherwise my code runs through the rest of the currently empty void loop. Later I can have other things in the void loop. This fix allows my code to not be "hung" checking for new data. I also commented out all delay statements to speed up the process.
Lastly, I took the time at the beginning of each void loop and the time at the end of my data calculation which only performs if new data is ready. I then take the difference of these two and print it. I added a flag within the if and else portion so that I did not reset my start time at the beginning of the loop if new data was not yet found. The start time is reset only if data was just collected. You can see the time being collected based on this flag which is set to 1 initially in the setup loop below:
<img width="150" alt="image" src="https://user-images.githubusercontent.com/89661904/221372128-472debf1-f3d6-485d-a866-e8f32a5e746f.png">
if new data is not ready, the code enters the else portion of the if statement and data_collected is set to 0. This means as the code runs through the void loop again it will now not reset the start time when checking for new data. Once new data is seen to be ready, the if statement is entered all calculations are made, then the data_collected is set to 1. This means on the next loop the start time will reset since I am now starting the timer for the next measurement.
Using this method, I collected data every blank_________________milliseconds.


