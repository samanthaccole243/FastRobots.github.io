## Lab 10

Before lab we were asked to set up the simulator and run the starting instructions. This imported all necessary libraries and set up the simulator. Next,  we started the simulator using these lines:

<img width="465" alt="image" src="https://user-images.githubusercontent.com/89661904/234406582-f12be59d-9280-4395-bd99-2e4753f440a1.png">

The images below show that the simulator and plotter are running:

<img width="224" alt="image" src="https://user-images.githubusercontent.com/89661904/234406538-c2e49197-3ce4-4cae-9e6a-1910a5b975ec.png">

<img width="652" alt="image" src="https://user-images.githubusercontent.com/89661904/234406472-18c91e10-a5d7-45b7-a979-2de1c0e7426e.png">


Next we run these lines:


<img width="405" alt="image" src="https://user-images.githubusercontent.com/89661904/234408857-3ae9c6df-b320-46f7-8365-2ae6e8479d2c.png">

This starts the plotter functioning. I maneuvered the little care around the main box in the room using the right and left arrow to change the angel, the up and down arrow to move forwards and backwards, and the space bar to pause. The plotter after this can be seen below where green is the ground truth and red is the odometry.

<img width="304" alt="image" src="https://user-images.githubusercontent.com/89661904/234407147-7e818c8f-3635-4717-9eeb-94a76bfdde84.png">

I then used these lines to stop the plotter and simulator:

<img width="352" alt="image" src="https://user-images.githubusercontent.com/89661904/234407255-effbe9bc-e38f-44b3-8b49-7e8894f79ad5.png">

I then started them back up again and ran the following lines of code. These print the sensor values as the car maneuvers.

<img width="440" alt="image" src="https://user-images.githubusercontent.com/89661904/234407522-272bdae8-4e32-49ab-add0-cab969fbea3c.png">

We were also asked to review many topics which I will reiterate:

## Review Topics
_Ground Truth_ : The actual real location of the robot

_Odometry_ : The process of a robot using the ToF sensors to estimate their location.

_Robot Localization_ : Using odometry

_Grid Localization_ : approximate 3-dimentional location: (x,y,theta). There are too many possible states so this is minimized into a grid of (.3048m, .3804m, and 20 degrees) and the location is estimated according to the states in the grid. We were given a visual of this grid in lab. This can be seen here: 

<img width="479" alt="image" src="https://user-images.githubusercontent.com/89661904/234425170-080be26c-e95e-4aa7-9601-04c776b99817.png">

_Sensor Model_ : using a Gaussian distribution to estimate and iradicate measurement noise.

_Motion Model_ : using odometry to determine a control input.

_Bayes Filter Algorithm_ : This uses a prediction and then an update. The prediction guesses where the robot moves using movement data (uncertainty added) and the update uses measurement data to decrease the uncertainty.

_Prior Belief_ : belief calculated after the prediction step

## Lab Task 
Perform Grid localization with the given sample directory and attach a video of the best results along the trajectory.

_Given Trajectory_ : 

<img width="432" alt="image" src="https://user-images.githubusercontent.com/89661904/234426732-673159e0-cdb4-49c3-8f6e-408d65018318.png">

We were also given this _Observation Data_ setup:


<img width="471" alt="image" src="https://user-images.githubusercontent.com/89661904/234426889-95d5489c-89ff-4c87-9d17-36bcc972ce7d.png">


## Lab Procedure

### Helpful Tips

pyton math module and associated functions were recommended, as well as the gaussian function of the BaseLocalization class. Th gaussian function can be helpful for modeling noise.
We were also given this line of code to help prevent ploating point underflow: <img width="248" alt="image" src="https://user-images.githubusercontent.com/89661904/236052963-8c256bf0-5935-4a9e-9115-effb5e112f4e.png">

### Lab

 The first function to write is called compute_control. This takes two inputs, curr pose which is the pose now at time t and prev pose which is the pose at time t-1. It then returns the control input u expressed as delta_rot_1, delta_trans, delta_rot_2. My code for this can be seen here:

<img width="533" alt="image" src="https://user-images.githubusercontent.com/89661904/236059740-7da3ad6a-b5ec-477f-b0e7-d49cb9c9470e.png">


The second function is the probability that the motion model is correct. This can be determined using the given lab formula seen here:

<img width="357" alt="image" src="https://user-images.githubusercontent.com/89661904/236059980-cbc492c3-8e9f-419a-9f88-1deffe876ce0.png">


The code I wrote for this can be seen here:

<img width="664" alt="image" src="https://user-images.githubusercontent.com/89661904/236059686-1fcf7319-5128-42ec-8633-b33c0de4ef5d.png">


The next function goes through the every possible location the robot could be to try to zero in on where the robot might actually be. This is the prediction step and choose the one with the highest probability to be correct. This function can be seen here:

<img width="676" alt="image" src="https://user-images.githubusercontent.com/89661904/236060442-a5dcb540-19b5-4936-8bd2-350bfe0e978c.png">

The next function goes through the different 18 observed robot poses that should be passed in using an array. The function then goes through each of these and calculates the probability that that data was actually taken from the thought location. This uses this given probability function.

<img width="242" alt="image" src="https://user-images.githubusercontent.com/89661904/236060994-b55e4cd8-53d9-4359-8b4a-a0fae7285003.png">

My implementation of this function can be seen here:
<img width="699" alt="image" src="https://user-images.githubusercontent.com/89661904/236061081-98daa68d-ead1-493b-85e1-00fade6b0fd1.png">

Lastly we needed to implement the update step for the Bayes Filter. This uses the above probability and the bel bar (multiplying each all together to get the total) to update the belief of the robots pose.
My code can be seen here:
<img width="507" alt="image" src="https://user-images.githubusercontent.com/89661904/236061379-9b2cca8e-4fc4-4dda-acb3-3d3daecba78a.png">

I want to Thank many past student pages I looked at as well as Anya Prabowo and Jack Defay in particular. Their pages really helped me understand the scope of the project and understand how to write some of the code. 

Below is a link to my video. In this video, I show the code being run in the necessary order and the actual implemenation on the simulator and plotter. Thank you!

https://youtu.be/VC09A3fGqiY
