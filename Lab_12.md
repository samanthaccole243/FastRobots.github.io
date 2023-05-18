Lab 12 has very simple instructions with quite a difficult task. The main idea is to use some method which was used throughout the semester to showcase what you have learned by following this path:

<img width="449" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/6a20f9f5-1b40-45f7-9b91-929cf325f396">

The points on this path can be seen in the given list from the lab handout:

<img width="168" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/58e73a15-eff8-4b4a-9718-fb47bc530a86">


If you look at my lab 11, you can see the my localization is quite a bit off. This made me decide to use PID to complete this lab instead. Lab 9-11 It was an option to use angular PID. I opted for the easier options of utilizing increments. For lab 12 I decided to advance and take the step to code this path using Angular speed PID as well as distance PID. This effectively means that I will be using two sensors to attempt to track my speed, angle, and distance from objects. I wrote five functions. The first is a repeat of the PID labs. There is a function 'find_dist' which calls my second function and my third function. It uses the results and feeds the recommended pwm to the motors. It uses the distance to decide whether to apply the result to which motors, and when to stop the car. The second function merely grabs the distance using the ToF sensor. The third function, the pwm pid function is the same as the pid lab. It uses a proportional constant and the error  as well as an integral constant and the integral of the error to add them together (P+I) and determmine the next pwm duty cyle to send to the mosors based on the approach to the goal. The only difference is that in previous labs I had the 'goal' defined. This lab I made the goal a global variable which I changed to match the distances the ToF should see on the map in the different locations. These three functions can be seen below. 

<img width="494" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/efd2a022-3499-4558-a5fe-9b9b8f388ea1">


<img width="596" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/2764e3ba-0e56-42f4-ac3f-9b7013cd5777">



There are are two more functions. One, 'turn', calls the





<img width="387" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/86630533-85d1-4dfc-89a6-5c807866ade0">
<img width="324" alt="image" src="https://github.com/samanthaccole243/FastRobots.github.io/assets/89661904/ce205310-4a14-4059-8866-b97db6e43a93">
