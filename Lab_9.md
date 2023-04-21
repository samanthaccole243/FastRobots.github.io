### Lab 9: Mapping (Real)
This lab consists of writing a code to rotate your robate in different locations in a set room and map the area in the lab. The room had 4 different locations for the robot to map. There were # options for rotating around these locations: open loop control, orientation contrl, and angular speed control. I chose open loop control since this is the best option for students behind on labs and as can be seen in Lab 8, my robot broke and was not able to perform its stunt. I had to get a new robot base and re-solder the circuitry on the new robot. 
To perform this task, I needed to have a non blocking way of having my robot move and stop.I also decided I only wanted to record ToF values when stopped to avoid any misread values. The difficulty arises whith the IMU yaw measurement. Yaw is the measurement around the z-axis. The IMU measures angular speed. To get just degrees, we need to integrate this term. This is done in a Reimmans sum type manner, where the numbers are added times the time difference. This should be done as often as possible with no pauses in between to be the most accurate. Therefore I had to keep integrating over the IMU while waiting for the ToF to be ready and while timing my stops and moves without any blocking. 
This code can be seen here:
<img width="396" alt="image" src="https://user-images.githubusercontent.com/89661904/233531570-d2d69c52-999d-433b-9171-030cd5c2fd5f.png">

<img width="511" alt="image" src="https://user-images.githubusercontent.com/89661904/233531603-8418f731-d5d9-41d3-a5fa-2a250c8bf9ab.png">

<img width="430" alt="image" src="https://user-images.githubusercontent.com/89661904/233531624-096208f5-e1aa-48d1-ab30-fe62dadb8e43.png">

There are a lot of print statements that were used for debugging. Also, I sent additional data over bluetooth for debugging purposes.

I had a notification handler on the python side to handle the incoming data. This can be seen here:
<img width="387" alt="image" src="https://user-images.githubusercontent.com/89661904/233532500-d0c1f81d-1ff9-4162-9712-1531024eb2d1.png">
 
 I would then send the command for the case above over bluetooth like this:
 <img width="222" alt="image" src="https://user-images.githubusercontent.com/89661904/233532732-b5214116-df51-41d5-9b0e-8233d4b55d20.png">

My robot would then perform a slowly incremented turn seen here:

___Video here___

From this video I did cut down the time of movement and the overturn. Because my robot differed a bit how many increments it took to rotate 360 degrees due to mechanical instability I did decide to leave in a slight over rotation which can be seen in all plots below. Next it was time to test this lady in pink robot out on the taped sections in the room. To graph each location on polar plots, I had to ater the deg of the yaw to radians, which you can see being done in the notification handler above. I decided to both graph a line and the actual point dots for more information on these plots. I also added an adjustment term to rotate each reading since the robot has no ide what degree it actually started at only where it has moved from then.
 
