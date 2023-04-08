### Lab 7

The majority of this lab is about setting up and implementing a Kalman filter. Because the kalman filter can be quite finicky for students who are a bit tight on time, we can solve all the necessary variables for the Kalman filter then take a shortcut. This shortcut involves extrapolating the ToF sensor data to 'speed up' sampling time for the ToF by estimating the distances in between each sample response.

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
<img width="234" alt="image" src="https://user-images.githubusercontent.com/89661904/230702514-4a8cf846-79b3-40f7-9cce-436eec7d75b4.png">

Now I could make the A and B matrices for the Kalman filter:
<img width="222" alt="image" src="https://user-images.githubusercontent.com/89661904/230702534-e945ffbb-afd8-4730-a4d8-65473a5d5cf0.png">


