## Lab 2
We had a prelab to complete ahead of time for lab 2. Unfortunately, I did not get very far into this prelab. I was able to install python, pip, and the virtual environment, but could not activate the FastRobots_ble Virtual environment due to settings regarding scripts within my PC. I tried posting on ed (the class discussion forum) to ask for help or guidance, but I got no response. This means I went into Lab 2 without my prelab completed. In lab, I was relatively quickly helped to find a work around with my issue. I downloaded and unziped the appropriate codebase files we were given, installed everything necessary to set connect the artmenis board, and attempted to connect. Unfortunately after quite a long time of attempting to connect with the help of TA's and many other students struggling, it became evident that PCs running windows 11 were not going to support bluetooth on the Artemis board.

This means I had to start the lab from the beginning (before prelab) on the desktop computer. After redownloading the codebase and activating the FastRobots_ble virtual environment, I was able to launch jupyter lab and connect to the artmeis board!
To do this, I launched the ble_arduino.ino c code and uploaded it to the board. This output my board's mac address. I copied this mac address and pasted it into my connection.yaml file.
Next I ran the lines 
               from uuid import uuid4
               uuid4()
This gave me a UUID to use with my board to help me avoid connecting to other boards when using the mac address and uuid together. I also added this to my connection.yaml file. You can see my artemis mac address on line 1 of the file and my generated uuid on line 3 of the file seen below. 
<img width="480" alt="connection yaml_pic" src="https://user-images.githubusercontent.com/89661904/218335662-336f130c-9250-4026-a4e9-1c86c395db5f.png">
I also went and put this UUID into the arduino.ble seen below.
file<img width="490" alt="arduino_lin8" src="https://user-images.githubusercontent.com/89661904/218335788-2ec58598-e89a-4550-bd64-53b6fcc3833f.png">
I then re-uploaded this file to the artemis.
After this step, I launched demo.ipynb from my jupyter notebook and followed all of the steps. The first cell involved importing appropriate libraries. The third cell attempts to connect your artemis via bluetooth. When successful, it looks like this:
![demo 2](https://user-images.githubusercontent.com/89661904/218336094-bf3d0a1d-b19b-4bfc-a124-0d4d5f6682ff.PNG)

A few of the next cells just tested very simple functions written by the course instructors to assure the bluetooth on the board is behaving apporopriately. I will not discuss all the cells since in my opinion they were testing similar things. An important test within was the send command ping function. The function can be seen below in the ble_arduino.ino file:
<img width="429" alt="ping" src="https://user-images.githubusercontent.com/89661904/218336508-2996c9ab-5e67-4ef2-afaa-f44f68887059.png">
In jupyter lab, using python, we send the command "PING" and as can bee seen in the code above, we expect to receive a "PONG" response. This took place as can be seen below.
![demo 67](https://user-images.githubusercontent.com/89661904/218336601-cd100b43-9dfb-4f31-9152-285fc033521e.PNG)
The second cell in the photo is used to receive any strings sent to the computer and print the for my viewing. The function in the ble_arduino.ino you can also see that there should be a serialmonitor output of "Sent back: PONG" which as shown below did take place. 
![demoserialmonitor](https://user-images.githubusercontent.com/89661904/218336938-2ff6ee8c-cb7b-49f8-b52a-3aa40ddedba2.PNG)
The two integers are from a different test and can be ignored.

The main portion of lab 2 had us writing code in the ble_arduino.ino and the demo file to interact with the bluetooth on the artemis and the computer. I will now address each task individually.

### Task 1
The first Task asked us to write a command ECHO which repeats the string sent from the computer to the board back to the computer with the result "Robot says --> string sent".
This means using jupyter lab, I can send the ECHO command with a string. This is the computer sending this to my artemis board. I wrote the ECHO command in the ble_arduin.ino in c and uploaded that to my board. This can be seen below:
<img width="424" alt="echocode" src="https://user-images.githubusercontent.com/89661904/218337914-b4f9b7c9-af32-450e-bbae-e97f83078ce0.png">
 This code makes the artemis board take the string and send back "Robot says --> ___ :) " , where the blank is the string. Here is proof of it working:
 ![echopythoncode](https://user-images.githubusercontent.com/89661904/218337990-b2f11508-5496-4960-836c-b84d710cc9e9.PNG). 
 The code also stipulates that be shown on the serial monitor. This is the Serial monitor output.
 ![echoserialmonitor proof](https://user-images.githubusercontent.com/89661904/218338032-4678364c-881e-4a60-acff-3a6d46de0859.PNG)

## Task 2
The second task asked that we write the command GET_TIME_MILLIS, which makes the artemis board send the time in millis to the computer as a string with added context.
Here is my c code in the ble_arduino.ino file, which I uploaded to my artemis board.
<img width="397" alt="get_time_millis" src="https://user-images.githubusercontent.com/89661904/218338380-ff3006bd-b497-4994-b4a6-894bfdd7bec0.png">
This code initializes an integer, clears the string value and adds "T: " to it. I then use the function millis() to save the time into my set integer and then I append this value to the string and send this back to the computer from the artemis board. Here is Task 2 functioning below. I used the receive function to check for the string sent to the computer which as you can see outputs the time in milliseconds.
![Task2](https://user-images.githubusercontent.com/89661904/218338541-ca84cd6c-a8f2-452e-90a2-7ec81794b372.PNG)


### Task 3
So far I have been using the receive function to check for the string sent to the computer. Instead of running this everytime I send a command which sends a string back to the computer, it would be nice to have the computer automatically print a received string when a new one arrives. Task 3 addresses this.
My notification handler can be seen written here:
![task3 code](https://user-images.githubusercontent.com/89661904/218338811-e928c3e5-b240-400e-922a-df2f2d819dc8.PNG)

After running the notification handler, I reran lab task 2 and instead of needing to run the receive function, the string response was automatically printed right after running the send command. This can be seen here:
![t3-now t2 prints immediately](https://user-images.githubusercontent.com/89661904/218338818-1e787f20-0030-4aa5-936e-2eefd7525513.PNG)


### Task 4
 This task asks that we write a command which asks the artmeis to measure and send the temperature every second for 5 seconds. The expectation was for the artemis to timestamp this data and give context to clarify which is the time and which is the temperature. I decided to do this without adding more proccessing code to my notification handler and instead by having the artemis board order my data with context before it sent it as a string. My ble_arduino.ino GET_TEMP_5s code can be seen below:
 <img width="582" alt="temp" src="https://user-images.githubusercontent.com/89661904/218339521-6069257d-d197-4c38-ac4d-ac34eb5c2e76.png">

Here is proof of me sending the command and it working
![Get_TEMP_5s](https://user-images.githubusercontent.com/89661904/218339632-5666f200-4563-4b1e-bde5-e6ba1c736a81.PNG)

### Task 5
Task 5 is the same as 4 expect we wanted at least 50 sets of data in the 5 second period.
As the code gets longer and more difficult, I will not include full code snippets. The code here is similar to the code above, but instead of gathering and sending every second, I gathered the 50 data sets of time and temperature of 5 seconds in an array first, then after all my data was entered into my array, I used a loop to send each set of data as a string from the artemis to the computer. Here is proof of this command in action.
![task5_1](https://user-images.githubusercontent.com/89661904/218339812-5075726f-6e43-4ca7-b69f-c4c32d17a840.PNG)
![task5_2](https://user-images.githubusercontent.com/89661904/218339816-29bafaa8-5d8a-470b-b528-dbc0a01905c1.PNG)
Saving data in the array before sending and sending in packets of each data set may take slightly longer but it makes sure that all my data gets sent and nothing is missed.

### Task 6
This was not actually a task but more of a question. It asks us to discuss how much data the artemis board can store before running out of memory using 150 samples of 16 bit values in 5 seconds. I simply multiplied 5 by 16 by 150. In this instance the board would have to handle 12,000 bits. 1kB is 8,000 bits and the board can hold 384 kB. This means the board can hold 3,072,000 bits. So we can run this scenario above 256 times, before running out of memory space.

### MENG TASK
This task asked us to compare time between sending 5byte data and 120byte data.
Also I wanted to compare 120Bytes of data sent as packets of 5Bytes to answer if shorter packets reduce overhead. I did this by sending strings since each character is a byte. In python I also created a new notification handler to help me record the times each of these took. My notification handler and functions that send 5Bytes, 120Bytes and packets of 5Bytes 24 times can be seen below:
![MENG_notification_handler](https://user-images.githubusercontent.com/89661904/218341117-a77e76bd-9848-47cd-b9b3-e1d5da921bd4.PNG)
![MENG_5B](https://user-images.githubusercontent.com/89661904/218341124-a617ce46-0567-4757-a3c0-cd52aaec8a83.PNG)
![MENG_120B](https://user-images.githubusercontent.com/89661904/218341125-7cbf84d5-2c90-48f4-b7e8-57e04eabb79e.PNG)
![MENG_5B_sets_1](https://user-images.githubusercontent.com/89661904/218341128-c47d4ebb-dcd4-42c6-9ad3-3dc3fe4e299e.PNG)
![MENG_5B_sets_2](https://user-images.githubusercontent.com/89661904/218341133-e20c75aa-0078-4f65-9767-c8f5e02cb9e9.PNG)
I ran the first functions 24 times and created plots to compare all of these.
Analyze plots.
Answer reliability question.

