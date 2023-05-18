## Lab 11

For this lab we are given an updated code from lab 10 to go off of. This is within the file lab11_sim.ipynb.
Below is the plot this code creates after running the bayes filter code with a prediction step and an update step.
<img width="546" alt="image" src="https://user-images.githubusercontent.com/89661904/236550661-d1196c70-7546-4d32-881a-8ec6b200abd4.png">

We are also given two additional files: (1) a fully functional localization module that works on the virtual robot and (2) a jupyter notebook with a the skeleton code to implement bayes filter on the physical robot in conjunction with the localization.

The next step will be to implement lab 9 assuring that there are 18 measueremnts. This means we to rotate 360 degrees and take 18 measurements in four different location on the map. Therefore every rotation needs to be about 20 degrees.

Unfortunatley, I would have to completely revamp my code to assure exactly 20 degrees every single time. This would be the most accurate way of doing it to. I am already a bit behind on labs, as most of the class is. So I have decided I will use my current lab 9 code which just turns small increments. I will then count the number of increments it makes to form 360 degrees. I believe it is around 25 to 30. I should be able to increase the timing of each movement between the increments so that I only utilize 18 measurement points. in the 360 degrees. I can then use this in the different location in unison with the localization to complete lab 11.

I decided that I wanted to have my first reading start before the turning stops to get a solid read on the location. I used this arduino.ide code to get a single measurement point of the ToF:

<img width="572" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/449de429-d526-4e3d-b3e1-117d8a93e349">

I then used another arduino code to make the 20 degree turns. I make sure to wait till I get a good ToF measurement stationary before making each subsequent 20 degrees. This code can be seen here:

<img width="632" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/83abfdeb-59d7-4eec-b8dc-b97428222a6a">


I send the the toF readings for those measurements to my pc via bluetooth.

I use a notification handler on the python jupyter lab to gather this data including the first measurement and formulate the data into a python list, dist. My notification handler can be seen here:

<img width="394" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/9310662c-2155-4318-a213-d9382dce5655">

As stated previously, for this lab we are given everything else as well as a recreated lab 10 and the rest of the code we might need to write for lab 11. We are only expected to write code to collect those 18 measurements that would feed into the functions we wrote in lab 10 (or their recreation) where we had written code that intakes 18 tof measurements and performs bayes filter to localize the robot. My code to get the robot to take these measurements using the two commands seen above, can be seen here:

<img width="680" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/57ea4779-acfa-42a4-82d9-26b8b59b819f">

You can see that there is a coded out hardcoded array. I used this to test my function. I couldnt seem to get the localization to be slightly close. Everytime I took a measurement, even in different locations, it placed me in the same spot in the box. After a long time trying to solve this, I realized the code requires that the robot turn anti-clockwise. This was not stated in the lab handout and it is not able to be seen in the code since they did not want to give us the answers to lab 10 by seeing lab 11. It turns out thayt the robot also had to start in a set direction. this was also not clearly stateed in the lab handout. I had tried to get help from other TAs regarding my code and why the localization wasnt working and two TAs did not know, but finally a third TA told me the secret that the code requires anti-clockwise turning and the robot to start in a certain direction.
