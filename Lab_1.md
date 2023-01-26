## Lab 1

This lab Was relatively simple. We were asked to download the latest arduino IDE and install the SparkFun Apollo3 Boards. As you can see below I did this. This is also evident by the fact that I was able to choose the correct board to upload to (RedBoard Artemis Nano) as seen in the other photo below.


*Spark FunApollo3 Board Installed*

<img width="140" alt="spark installedpng" src="https://user-images.githubusercontent.com/89661904/214734151-92a7946a-5dd6-49c3-9cf5-a6f022f13194.png">



*Correct Board Chosen*


<img width="272" alt="board" src="https://user-images.githubusercontent.com/89661904/214734731-ecbf085a-6e89-43e3-8784-fc8480f2d6fb.png">


I then plugged in the RedBoard Artemis Nano and ran the blink code from the examples. 


*Artemis Board Plugged in*
![](https://user-images.githubusercontent.com/89661904/214735930-b352260d-d1ac-4031-9c57-06db4b2dc1f8.jpg)

*Video of the Light Blinking*

https://user-images.githubusercontent.com/89661904/214737368-16a09cff-1476-4e5e-bf80-f415c7d8b30f.MOV

![Blinking LED](https://www.youtube.com/shorts/dIMhkwiaZEY)

(622) Blinking light - YouTube

Next I ran the Example code for echoing text on the serial monitor.
A video of this can be seen below. I type "serial" and press enter and the serail monitor echoes this text.


Next we Ran the Analog Read example. This code reads the temperature of the chip. In the video you can see the 3 leftmost digits of the total 6 bounce between 331 and 332. Once I put my finger on the chip, the temperature increases and the temperature 3 leftmost digits bounce between 332 and 333. Clearly the temperature and relative increase is being noted on the serial monitor.


The last part of the lab was to run the Microphone output example. This code basically measured frequencies near the chip and printed the loudest frequncy Hz value on the Serial Monitor. In the video below, you can see that when I whistle the frequency jumps into the thousands!


There was an additional section for MENG students in this Lab, since I am in the 5000 level version I completed this section too. This asked us to write a code where the board would blink the LED when an A note was played. I used the example code from the microphone output example and edited it to complete this task. First, I initiated the LED in void setup using the line below. 
<img width="200" alt="setupLED" src="https://user-images.githubusercontent.com/89661904/214743903-058a29e7-2850-4d52-afe3-ac75fafcaf96.png">

I also initiated my own variable, MyFreq, so I could search for the A note frequency range. Here is how I initialized my variable.
<img width="107" alt="initializemyvariable" src="https://user-images.githubusercontent.com/89661904/214743984-a2acfee5-1da3-44e1-976f-47df4e68a9d9.png">

Next, I found the portion of the code which finds the loudest frequency then prints it to the serial monitor and set that value found to MyFreq, as seen here.
<img width="446" alt="myvariable" src="https://user-images.githubusercontent.com/89661904/214744172-ca3f3f99-212e-48a7-a287-6519675de884.png">

I then added an if statement searching for the MyFreq to be between the Hz ranges of an A note (440Hz to 880Hz). Once this was found, I printed "Note A Found" onto the Serial Monitor and blinked the LED. This code can be seen below. 
<img width="513" alt="myifstatement" src="https://user-images.githubusercontent.com/89661904/214744072-3e5daa37-ddaa-47db-9160-26edaa0f5759.png">


Unfotunately, for my video, I did not add the \n as seen above in the code, so the Note A Found is actually for the line and frequency above, not the frequency it is aligned with. Here is a video of the code working and below that is a photo of the serial monitor output.

![serialmonitornotea](https://user-images.githubusercontent.com/89661904/214744200-5132b109-bd7d-4015-a1ae-a2610bb4d83f.png)








