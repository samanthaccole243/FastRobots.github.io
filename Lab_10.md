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

We were also given this _Observation Data_ :

<img width="471" alt="image" src="https://user-images.githubusercontent.com/89661904/234426889-95d5489c-89ff-4c87-9d17-36bcc972ce7d.png">


## Lab




