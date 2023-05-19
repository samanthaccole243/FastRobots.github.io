### Lab 12
 

Lab 12 has very simple instructions with quite a difficult task. The main idea is to use some method which was used throughout the semester to showcase what you have learned by following this path:

<img width="449" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/6a20f9f5-1b40-45f7-9b91-929cf325f396">

The points on this path can be seen in the given list from the lab handout:

<img width="168" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/58e73a15-eff8-4b4a-9718-fb47bc530a86">


If you look at my lab 11, you can see the my localization is quite a bit off. This made me decide to use PID to complete this lab instead. Lab 9-11 It was an option to use angular PID. I opted for the easier options of utilizing increments. For lab 12 I decided to advance and take the step to code this path using Angular speed PID as well as distance PID. This effectively means that I will be using two sensors to attempt to track my speed, angle, and distance from objects. I wrote five functions. The first is a repeat of the PID labs. There is a function 'find_dist' which calls my second function and my third function. It uses the results and feeds the recommended pwm to the motors. It uses the distance to decide whether to apply the result to which motors, and when to stop the car. The second function merely grabs the distance using the ToF sensor. The third function, the pwm pid function is the same as the pid lab. It uses a proportional constant and the error  as well as an integral constant and the integral of the error to add them together (P+I) and determmine the next pwm duty cyle to send to the mosors based on the approach to the goal. The only difference is that in previous labs I had the 'goal' defined. This lab I made the goal a global variable which I changed to match the distances the ToF should see on the map in the different locations. These three functions can be seen below. 

<img width="494" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/efd2a022-3499-4558-a5fe-9b9b8f388ea1">


<img width="596" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/2764e3ba-0e56-42f4-ac3f-9b7013cd5777">

<img width="347" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/8e4e7175-3076-4cdb-a1b9-dd419b5fcdb0">


There are are two more functions. One, 'turn', calls the last function, 'PID angle. The PID_angle function is actually only a P implementation. it uses the current angle as measured from the IMU to compare to the 'degree' which I want the robot to be at. This is the error which was multiplied by the porortional constant. and used to determine the next angle speed.
This 'degree' is again a global fariable just like the goal for the distance PID. In the main loop I set the global variables then call the function and repeat. The turn function takes this next angle speed and uses this, the angle error, and an additional term 'left' to determine which way to divert the speed. 'Left' is also a global variable which I set before I call the function. if 'Left' is 1, then the angular speed will be put tp the motors to turn left if the angular speed its positive and right if negative. If 'Left' is 0 the opposite will take place. These two functions can be seen below.


<img width="550" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/b5e97ae4-f4c4-48a8-ad90-71129221aef2">



<img width="387" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/86630533-85d1-4dfc-89a6-5c807866ade0">
<img width="324" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/ce205310-4a14-4059-8866-b97db6e43a93">


It is also important to note that I have speed maximum and minimum caps on the speeds sent to the motors. The minimum caps make sure the robot can still move. The maximum caps make sure the robot doesnt go so fast that it bumps around a lot into walls unable to slow down fast enough.


My videos (There are many) can be seen here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/esv_dGLrPD0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


If this embedded link does not work please use the link below:

https://www.youtube.com/watch?v=esv_dGLrPD0

I can be seen tapping the robot once or twice. This is mainly because my motors occassionally kind of freeze up and the wheels get stuck. If I give it another nudge, problem solved.


Obviously this is not a perfect execution. I was not expecting one. There are many reasons for the inacuracies.
1. No localization code: I did not use localization. this is because I felt as though my localization was not precise enough for the prupose of the lab to meet the requirements. If localization was more exact. This would be much more accurate, but also very very difficult to code. 
2. Mechanical issues: Every iteration, My robot acted a bit different. Batteries slowly die, sensor readings have noise and error, and the motors definitely do not perform uniformly or in the same manner each time. All these differences can cause the robot to be slightly off.
3. hard coding - software: Since I decided to hardcode the degrees, the direction (left or right), and the distances. The worst part to hardcode was the degree angle. The motors seemed to overshoot the angle occasionally. This brings the last reason for inacuracy.
4. The PID code stops correcting the angle once the exact angle is reached. The toF sensor is very slow. this means that it is more likely the care will reach the desired location and measure above or below this until it is steadily at its desired location. The IMU is extremely fast. The robot may overshoot the angle and take 2-5 measurements that are still within the angle margin of error. This means no angle correction for overshoot is really taking place even though it should be. 
