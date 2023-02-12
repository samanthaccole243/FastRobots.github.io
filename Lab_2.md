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



