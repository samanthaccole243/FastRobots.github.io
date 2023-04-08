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
<img width="378" alt="image" src="https://user-images.githubusercontent.com/89661904/230701696-af622116-9ed5-4c84-a0be-85652d9d3e37.png">
I have some print statements commented and uncommented throughout for debugging purposes as I was writing the notification handler.
The velocity calculation can be seen here:
<img width="179" alt="image" src="https://user-images.githubusercontent.com/89661904/230701720-d0ab113a-90a6-47c7-999c-eac483a55b66.png">

How I plotted the three graphs can be seen here:
<img width="136" alt="image" src="https://user-images.githubusercontent.com/89661904/230701735-b443bfd9-7876-47bd-baa6-8c00ea692347.png">

<img width="157" alt="image" src="https://user-images.githubusercontent.com/89661904/230701750-fc5e7a9c-a84c-4492-a3ad-ff4f05e702af.png">

<img width="142" alt="image" src="https://user-images.githubusercontent.com/89661904/230701784-3223fdc0-a42a-4444-867f-cdf6f387b4ad.png">

I append a zero in the velocity since How I calculate the data makes me have one less data point compared to time.
