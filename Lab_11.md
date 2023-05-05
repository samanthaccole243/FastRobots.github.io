## Lab 11

For this lab we are given an updated code from lab 10 to go off of. This is within the file lab11_sim.ipynb.
Below is the plot this code creates after running the bayes filter code with a prediction step and an update step.
<img width="546" alt="image" src="https://user-images.githubusercontent.com/89661904/236550661-d1196c70-7546-4d32-881a-8ec6b200abd4.png">

We are also given two additional files: (1) a fully functional localization module that works on the virtual robot and (2) a jupyter notebook with a the skeleton code to implement bayes filter on the physical robot in conjunction with the localization.

The next step will be to implement lab 9 assuring that there are 18 measueremnts. This means we to rotate 360 degrees and take 18 measurements in four different location on the map. Therefore every rotation needs to be about 20 degrees.

Unfortunatley, I would have to completely revamp my code to assure exactly 20 degrees every single time. This would be the most accurate way of doing it to. I am already a bit behind on labs, as most of the class is. So I have decided I will use my current lab 9 code which just turns small increments. I will then count the number of increments it makes to form 360 degrees. I believe it is around 25 to 30. I should be able to increase the timing of each movement between the increments so that I only utilize 18 measurement points. in the 360 degrees. I can then use this in the different location in unison with the localization to complete lab 11.
