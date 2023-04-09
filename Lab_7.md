### Lab 7

The majority of this lab is about setting up and implementing a Kalman filter. The Kalman filter is meant to solve the issue of the slow ToF sampling by creating accurate estimates of the in between states. Because the kalman filter can be quite finicky for students who are a bit tight on time, we can solve all the necessary variables for the Kalman filter then take a shortcut. This shortcut involves extrapolating the ToF sensor data to 'speed up' sampling time for the ToF by estimating the distances in between each sample response using the slope. This option is a less accurate however is much faster to set up since there are not variables that need to be tuned. I solve all of the variables for the Kalman below and then eventually set upt the extrapolation.

To first set up the kalman filter, I took my robot and drove it at a high speed from my previous PID lab (80). I then faced it towards a wall anywhere from 1000 to 1400 milimeters away from the way. I had the ToF sensor measuring data and just drove towards the wall for a couple seconds. I kept looking to find a steady state velocity from this, but unfortunately that was not happening for me. I did many trials. Below are the graphs from four different trials. The Graphs show the motor input vs seconds, the ToF distance in milimeters vs seconds, and the velocity vs seconds. I calculated the Velocity using the distance in mm vs time in seconds data. 
## Trial 1:
<img width="466" alt="motin_t1" src="https://user-images.githubusercontent.com/89661904/230701551-955866bd-38a5-4c33-a2e4-692adfb716e5.png">
<img width="467" alt="distgraph_t1" src="https://user-images.githubusercontent.com/89661904/230701558-9beeb7cc-7004-4bef-91c4-e9ae1b415ec5.png">
<img width="494" alt="velgraph_t1" src="https://user-images.githubusercontent.com/89661904/230701560-87100726-4483-43b8-8a0f-9284ea011431.png">

## Trial 2:
<img width="488" alt="motin_t2" src="https://user-images.githubusercontent.com/89661904/230701574-483029ea-9d1c-4a37-aafb-bf3c5070a9a4.png">
<img width="457" alt="distgraph_t2" src="https://user-images.githubusercontent.com/89661904/230701578-1120c0ef-b359-4e8e-be9a-e214a0075a56.png">
<img width="488" alt="velgraph_t2" src="https://user-images.githubusercontent.com/89661904/230701583-1f326f44-a869-4beb-9470-493b62b2e9ad.png">

## Trial 3:
<img width="495" alt="motin_t3" src="https://user-images.githubusercontent.com/89661904/230701590-88e8242c-ec22-43f5-be4c-a573dbe24cc6.png">
<img width="503" alt="distgraph_t3" src="https://user-images.githubusercontent.com/89661904/230701585-6d31d2c4-bf56-472a-b468-a6c99df28ac6.png">
<img width="487" alt="velgraph_t3" src="https://user-images.githubusercontent.com/89661904/230701595-08ccfe97-f51a-4088-b645-7c109fadc421.png">

## Trial 4:
<img width="486" alt="motin_t4_c" src="https://user-images.githubusercontent.com/89661904/230701600-5510703f-1e27-4156-bf70-fc1d430559f8.png">
<img width="539" alt="distgraph_t4_c" src="https://user-images.githubusercontent.com/89661904/230701603-5cb87379-43b5-4df7-b1c4-b0c58c675f91.png">
<img width="519" alt="velgraph_t4_c" src="https://user-images.githubusercontent.com/89661904/230701605-65e9e24b-d480-45f2-af0b-811156a397ae.png">

I used bluetooth to send the car towards the wall and take the ToF measurements then send them to jupyter lab. I used a notification handler to save all the data in arrays. I then used matplotlib to make the plots. The notification handler can be seen here:
#
<img width="378" alt="image" src="https://user-images.githubusercontent.com/89661904/230701696-af622116-9ed5-4c84-a0be-85652d9d3e37.png">
I have some print statements commented and uncommented throughout for debugging purposes as I was writing the notification handler.
The velocity calculation can be seen here:
#
<img width="179" alt="image" src="https://user-images.githubusercontent.com/89661904/230701720-d0ab113a-90a6-47c7-999c-eac483a55b66.png">

How I plotted the three graphs can be seen here:
#
<img width="136" alt="image" src="https://user-images.githubusercontent.com/89661904/230701735-b443bfd9-7876-47bd-baa6-8c00ea692347.png">

<img width="157" alt="image" src="https://user-images.githubusercontent.com/89661904/230701750-fc5e7a9c-a84c-4492-a3ad-ff4f05e702af.png">

<img width="142" alt="image" src="https://user-images.githubusercontent.com/89661904/230701784-3223fdc0-a42a-4444-867f-cdf6f387b4ad.png">

I append a zero in the velocity since How I calculate the data makes me have one less data point compared to time.

To continue with the Kalman filter calculations I moved to my ipad. I took what seemed to be the average steady state of the velocity at 1300mm/s. This is the equation for drag:
<img width="88" alt="image" src="https://user-images.githubusercontent.com/89661904/230702310-44aec496-9f6d-44c8-a0a9-f9497bfc161a.png">
We assume u to be 1 and as previously stated the steady state velocity is 1300mm/s. So,
<img width="125" alt="image" src="https://user-images.githubusercontent.com/89661904/230702339-f93c40e6-b502-4bbc-b00f-af9db0a1d13e.png">

Next, we need to find the 90% rise time:
<img width="260" alt="image" src="https://user-images.githubusercontent.com/89661904/230702465-93d1e6e9-f293-4adb-b6f6-7f1b24f15d01.png">

To solve for this, I took two of the trials where my distance measuring seemed most smooth (no excessive spikes in the movement towards the wall). Here was my process:
![IMG_1173](https://user-images.githubusercontent.com/89661904/230702484-07cfc534-c7fc-47e1-8f59-1d47f2168e30.jpg)
![IMG_1176](https://user-images.githubusercontent.com/89661904/230702605-58b98ca6-f777-4108-bf75-f90379cf4d7a.jpg)

I then averaged the time I got for both of these (.9 and 1.1) and ended up with an estimated 90% rise time of 1 second.
I then used this to solve for mass:
#
<img width="234" alt="image" src="https://user-images.githubusercontent.com/89661904/230702514-4a8cf846-79b3-40f7-9cce-436eec7d75b4.png">


Now I could make the A and B matrices for the Kalman filter:
#
<img width="222" alt="image" src="https://user-images.githubusercontent.com/89661904/230702534-e945ffbb-afd8-4730-a4d8-65473a5d5cf0.png">

These can be seen rewritten in the python code below with the C matrix as given in the lab handout.

<img width="256" alt="image" src="https://user-images.githubusercontent.com/89661904/230738429-73ddebd2-78e3-4dd7-af54-8521ce19ffba.png">

The next part of lab asked us to Discretize our A and B matrices and evaluate the process and sensor noise. I can be seen discretizing the matrices here:
<img width="201" alt="image" src="https://user-images.githubusercontent.com/89661904/230738780-226439c7-19cc-4e5a-a792-abbf625c0724.png">
I used dt to be the average amount of time taken in between sensor readings from the Tof. This came out to be 0.13299999999999992 seconds.
I then account for sensor noise here:
<img width="248" alt="image" src="https://user-images.githubusercontent.com/89661904/230738866-b1693fe6-52d8-472b-9798-b3b86339851c.png">

I first set all the covariances to 10 since they represent trust in the sensors (sig1 and sig2) or trust in the model (sig3).

Next I implement the Kalman filter in Jupyter Lab. We are given the kalman filter in the handout, but I just made slight edits to match my variable names. The given function can be seen here:
<img width="385" alt="image" src="https://user-images.githubusercontent.com/89661904/230738923-500e7dad-cc85-4382-97e3-2c5b82728f03.png">

next I ran the code with my data from a run trial earlier. This can be seen here
<img width="219" alt="image" src="https://user-images.githubusercontent.com/89661904/230739079-9b5087d7-0619-4b01-9b64-172a84f8a0d8.png">

I then plotted the results as seen here:
<img width="211" alt="image" src="https://user-images.githubusercontent.com/89661904/230739095-f657e0c7-a037-4c87-a2d2-95dddb91dca2.png">

I did this multiple times just to messaorund with the covariances and see how it changes. Below are all of my results:
# sig1=10, sig2=10, sig3=10:
<img width="437" alt="Lab7_kfvsToF_sig101010" src="https://user-images.githubusercontent.com/89661904/230739148-e59524e1-3007-450e-acfa-d53da093487b.png">

# sig1=10, sig2=10, sig3=20:
<img width="424" alt="Lab7_kfvsToF_sig101020" src="https://user-images.githubusercontent.com/89661904/230739160-5d4cd45c-f0ca-4681-b394-9ba7aca7cf48.png">

# sig1=100, sig2=10, sig3=20:
<img width="417" alt="Lab7_kfvsToF_sig1001020" src="https://user-images.githubusercontent.com/89661904/230739164-b6f8c8d8-880a-4824-a63d-b210329d9755.png">

# sig1=10, sig2=100, sig3=20:
<img width="422" alt="Lab7_kfvsToF_sig1010020" src="https://user-images.githubusercontent.com/89661904/230739180-2a1c6788-2647-4a58-a411-9f05dd97c3c6.png">

# sig1=200, sig2=10, sig3=20:
<img width="434" alt="Lab7_kfvsToF_sig2001020" src="https://user-images.githubusercontent.com/89661904/230739190-fa418fae-676f-45c6-a4ec-b00ba6db2ca8.png">

# sig1=200, sig2=10, sig3=10:
<img width="432" alt="Lab7_kfvsToF_sig2001010" src="https://user-images.githubusercontent.com/89661904/230739195-0b8442c6-f2ac-4e44-bbd5-17d7a29a9138.png">

As you can see as the sig 1 value increases the plot matches the data more since we are placing more trust on the sensor values. As the sigma 3 increases my data gets more far off - placing less trust on the sensor values. Unfortunately the noisiness when it is far off, and how off it is makes me think my kalma filter model is pretty bad and maybe my initial measurements were not correct or effective for the filter purposes.

#
The next portion of this lab is the extrapolation. Once demonstrated an understanding of the Kalman Filter and played around a bit with the covariances. I wrote code in the arduino ide. I first cellect the distances from the sensor in an array tof. I then have ann array estimate which estimates the next point that would be read by the ToF if it were fast enough. The estimate array logs the tof entries and the next estimate and then the tof entry again and so on. This code can be seen written here:
<img width="597" alt="image" src="https://user-images.githubusercontent.com/89661904/230790897-843c2d62-7927-4fbf-afce-a52cab39a489.png">
<img width="418" alt="image" src="https://user-images.githubusercontent.com/89661904/230790911-ac9b3791-a4f3-442e-a12b-b0d20d0d9006.png">
<img width="586" alt="image" src="https://user-images.githubusercontent.com/89661904/230790924-72c9d17b-dc27-4097-a591-58ee15f49259.png">
<img width="409" alt="image" src="https://user-images.githubusercontent.com/89661904/230790938-0f1f8a54-e5f4-4923-80fc-d9d1d4d73bf9.png">

after this code I just send the stores arrays
where the time is 50 cells, the tof values are 50 cells, and the estimates are 100.
I then wrote a code in jupyter lab to handle the notifications sent individually. This is seen here:
<img width="464" alt="image" src="https://user-images.githubusercontent.com/89661904/230791042-c3d2e335-0b13-4efe-bb25-6100f9173a69.png">

I then wrote code to send the command, edit the seconds to 100 cells for the estimate plotting, and then plot both the Tof and the Estimates on a graph vs time. The tof is plotted as dots and the estimates are plotted in a line.
This code can be seen here:
<img width="465" alt="image" src="https://user-images.githubusercontent.com/89661904/230791102-e8fdf360-6c8b-4e2f-ae8e-2cac91de2196.png">

The video of my robot running this code can be seen vial these youtube links below:
https://www.youtube.com/shorts/Q1t3B-JW4N4
https://www.youtube.com/shorts/X3HxCu4QG5Y
https://www.youtube.com/shorts/wjbWt--EBpQ


I ran a few trials. Two of the graphs are below:

<img width="499" alt="ToFvsextrap" src="https://user-images.githubusercontent.com/89661904/230791129-2becc457-14f2-42a8-b9c7-523e614b8102.png">

<img width="483" alt="ToFvsextrap2" src="https://user-images.githubusercontent.com/89661904/230791132-f7638604-2072-44f5-83cc-cb77a8f35e1a.png">

As you can see and here in the video and see in the graphs, the movement is a bit jumpy. I believe that is due to some jumpiness from the tof, which causes jumpiness from the estimates. Also if they dont agree on a distance range from one of my categories in the if statement that can also cause jultiness. I could widen the range to fix the range but then I wouldnt back up to 1 ft as accurately. Also I do overshoot quite a bit, but there is nothing other than my code slowing the robot down as it reaches 1 ft.
