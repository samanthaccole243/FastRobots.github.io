### Lab 2
We had a prelab to complete ahead of time for lab 2. Unfortunately, I did not get very far into this prelab. I was able to install python, pip, and the virtual environment, but could not activate the FastRobots_ble Virtual environment due to settings regarding scripts within my PC. I couldn't figure out how to woirk around this. I tried posting on ed (the class discussion forum) to ask for help or guidance, but I got no response. This means I went into Lab 2 without my prelab completed. In lab, I was relatively quickly helped to find a work around with my issue. I downloaded and unziped the appropriate codebase files we were given, installed everything necessary to set connect the artmenis board, and attempted to connect. Unfortunately after quite a long time of attempting to connect with the help of TA's and many other students struggling, it became evident that PCs running windows 11 were not going to support bluetooth on the Artemis board.

This means I had to start the lab from the beginning (before prelab) on the desktop computer. After redownloading the codebase and activating the FastRobots_ble virtual environment, I was able to launch jupyter lab and connect to the artmeis board!
To do this, I launched the ble_arduino.ino c code and uploaded it to the board. This output my board's mac address. I copied this mac address and pasted it into my connection.yaml file.
Next I ran the lines 
               from uuid import uuid4
               uuid4()
This gave me a UUID to use with my board to help me avoid connecting to other boards when using the mac address and uuid together. I also added this to my connection.yaml file. You can see my artemis mac address on line 1 of the file and my generated uuid on line 3 of the file. Below is the photo of my connection.yaml file.
<img width="480" alt="connection yaml_pic" src="https://user-images.githubusercontent.com/89661904/218335662-336f130c-9250-4026-a4e9-1c86c395db5f.png">
I also went and put this UUID into the arduino.ble. This can be seen on line 8 of the ble_arduino.ino file below.
file<img width="490" alt="arduino_lin8" src="https://user-images.githubusercontent.com/89661904/218335788-2ec58598-e89a-4550-bd64-53b6fcc3833f.png">
I then re-uploaded this file.
After this step, I launched demo.ipynb from my jupyter notebook and followed all of the steps. The first cell involved importing appropriate libraries. The third cell attempts to connect your artemis via bluetooth. When successful, it looks like this:
![demo 2](https://user-images.githubusercontent.com/89661904/218336094-bf3d0a1d-b19b-4bfc-a124-0d4d5f6682ff.PNG)

A few of the next cells just tested very simple functions written by the course instructors to assure the bluetooth on the board is behaving apporopriately. An important test within was the send command ping function. The function can be seen below in the ble_arduino.ino file:
<img width="429" alt="ping" src="https://user-images.githubusercontent.com/89661904/218336508-2996c9ab-5e67-4ef2-afaa-f44f68887059.png">
In jupyter lab, using python, we send the command "PING" and as can bee seen in the code above, we expect to receive a "PONG" response. This took place as can be seen below.
![demo 67](https://user-images.githubusercontent.com/89661904/218336601-cd100b43-9dfb-4f31-9152-285fc033521e.PNG)
The second cell in the photo is used to receive any strings sent to the computer and print the for my viewing. The function in the ble_arduino.ino you can also see that there should be a serialmonitor output of "Sent back: PONG" which as shown below did take place. 
![demoserialmonitor](https://user-images.githubusercontent.com/89661904/218336938-2ff6ee8c-cb7b-49f8-b52a-3aa40ddedba2.PNG)

There were othe cells and tests like the two integers serial output response you can see in the photo above, but I do not think it is neccessary to review every single one since I did not write them and in retrospect they are testing similar things as the explained one above.

The main portion of lab 2 had us writing code in the ble_arduino.ino and the demo file to interact with the bluetooth on the artemis and the computer. I will now address each task individually.

## Task 1
The first Task asked us to "Send an echo command with a string value from the computer to the Artemis board, and recieve an augmented string on the computer."
This means using jupyter lab, I can send the ECHO command with a string. This is the computer sending this to my artemis board. I wrote the ECHO command in the ble_arduin.ino in c and uploaded that to my board. This can be seen below:
<img width="424" alt="echocode" src="https://user-images.githubusercontent.com/89661904/218337914-b4f9b7c9-af32-450e-bbae-e97f83078ce0.png">
 This code makes the artemis board take the string and send back "Robot says --> ___ :) " , where the blank is the string. Here is proof of it working:
 ![echopythoncode](https://user-images.githubusercontent.com/89661904/218337990-b2f11508-5496-4960-836c-b84d710cc9e9.PNG). 
 The code also stipulates that be shown on the serial monitor. This is the Serial monitor output.
 ![echoserialmonitor proof](https://user-images.githubusercontent.com/89661904/218338032-4678364c-881e-4a60-acff-3a6d46de0859.PNG)

## Task 2
The second task asked that we "Add a command GET_TIME_MILLIS which makes the robot reply write a string such as "T:123456" to the string characteristic."
Here is my c code in the ble_arduino.ino file, which I uploaded to my artemis board.
<img width="397" alt="get_time_millis" src="https://user-images.githubusercontent.com/89661904/218338380-ff3006bd-b497-4994-b4a6-894bfdd7bec0.png">
This code initializes an integer, clears the string value and adds "T: " to it. I then use the function millis() to save the time into my set integer and then I append this value to the string and send this back to the computer from the artemis board. Here is Task 2 functioning below. I used the receive function to check for the string sent to the computer which as you can see outputs the time in milliseconds.
![Task2](https://user-images.githubusercontent.com/89661904/218338541-ca84cd6c-a8f2-452e-90a2-7ec81794b372.PNG)


## Task 3
So far I have been using the receive function to check for the string sent to the computer. Instead of running this everytime I send a command which sends a string back to the computer, it would be nice to have the computer automatically print a received string when a new one arrives. Task 3 addresses this. It asks students to "Setup a notification handler in Python to receive the string value (BLEStringCharacteristic in Arduino) from the Artemis board."
My notification handler can be seen written here:
![task3 code](https://user-images.githubusercontent.com/89661904/218338811-e928c3e5-b240-400e-922a-df2f2d819dc8.PNG)


After running the notification handler, I reran lab task 2 and instead of needing to run the receive function, the string response was automatically printed right after running the send command. This can be seen here:
![t3-now t2 prints immediately](https://user-images.githubusercontent.com/89661904/218338818-1e787f20-0030-4aa5-936e-2eefd7525513.PNG)


## Task 4
 
 
