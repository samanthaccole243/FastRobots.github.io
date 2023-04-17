### Lab 8
This lab is all about stunts. For my stunt I decided to do Task A, which starts at a starting point more than 4m from the wall. The robot then should go as fast as is possible for the stunt, towards a sticky matt located .5 m from the wall. Once on the matt, the car performs a flip then heads back across the starting point. 

Currently I am able to run the car at 150 pwm speed toward the sticky matt, do a half flip, and then kind of zig zag back to the starting line. To decide when it is on the sticky matt, I currently have a variable set as stopping which is the distance I stop advancing at, and I am using my ToF sensors as well as my extrapolated code in combination. My stopping distance is defined at 2.5 ft.

To perform the flip, I am reversing the direction of pwm at 255 once I hit the matt. 
This code can be seen here: 
<img width="498" alt="image" src="https://user-images.githubusercontent.com/89661904/232555288-43f884b4-00eb-494b-80be-b1657996d62f.png">
<img width="432" alt="image" src="https://user-images.githubusercontent.com/89661904/232555311-5fd2e98b-09e7-493f-b486-53f289ba6cdf.png">

I have spent quite a bit of time debugging because it seems as though my motors change functioning every like 1-2 runs. This makes it very hard to keep up with. Unfortunately, I am at the point where I have replaced and re-done a large amount of circuitry and components, and I have the same issue the car started with before then. The car moves really slow, and one of the motors seems to move much much slower than the other - often times not moving at all. If I physically hold the running motors wheels, the other motor begins to run. The course staff and I have not come up with a solution to this as of yet. A video of the closest I came to a flip before my robot became less functional can be seen here. 



https://user-images.githubusercontent.com/89661904/232557193-edd57b2d-63cc-4403-8aef-e34e01b643da.MOV


The data for that run can be seen here:
![image](https://user-images.githubusercontent.com/89661904/232556216-a3bf34d7-50d1-4a73-8e87-c7d6c425ab3b.png)

