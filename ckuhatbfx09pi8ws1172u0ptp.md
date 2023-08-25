---
title: "Control 16 servos with Raspberry Pi + PCA9685 Driver"
seoTitle: "How to control 16 servos using a Raspberry Pi + PCA9685 Driver"
seoDescription: "In this post you will learn how to control up to 16 servos using the PCA9685 driver, raspberry pi and python library adafruit-circuitpython-servokit"
datePublished: Thu Oct 07 2021 18:54:00 GMT+0000 (Coordinated Universal Time)
cuid: ckuhatbfx09pi8ws1172u0ptp
slug: control-16-servos-with-raspberry-pi-pca9685-driver
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1633632430551/OuzP28ycS.png
tags: python, python3, robotics, raspberry-pi, python-projects

---

Hello everyone, I recently wanted to build a cool robot, and to do so, I needed to control 8 servos using the `PCA9685` driver and thought I shared my experience with anyone interested in this topic.

## To do this you will need:

1. Raspberry Pi (mine is the 3B+)
2. PCA9685 driver
3. Servos (the driver supports up to 16)
4. 4 female to female jumper cables.
5. External 5v power for the driver
6. Python3

## Connection

![connection.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633556132613/Pev6mGSGX.png)
5v-6v recommended power and you can connect as many servos as you like

## coding with python3

Turn on your Raspberry Pi and open a new terminal, then run the following commands:

```
sudo apt-get install git build-essential python-dev
git clone https://github.com/adafruit/Adafruit_Python_PCA9685.git
cd Adafruit_Python_PCA9685
sudo python setup.py install
cd examples
``` 
Inside the examples folder, you should find the `simplest.py` example code, to run it use the command 

`python3 simplest.py`

However, if we execute this program we get an error

> No such file or directory: '/dev/i2c-1'

To fix this we need to open the raspberry pi software configuration

`sudo raspi-config`

![2021-10-06-194915_1024x768_scrot.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633571528097/DYMdnvc84.png)

Use the down arrow to select interfacing options and press enter, then select P5 I2C and enable the interface ==> ok ==> finish.

Now, if we execute the `simplest.py` file we shouldn't get any errors and our servo should start moving, Nice!, however the code it's unnecessarily complex for what I need. I would like to call a function that passes the target degree as a parameter and nothing else, this way the code would be easier to read and with fewer bugs, to accomplish this I'm going to use the Adafruit Servo Kit library for python

https://github.com/adafruit/Adafruit_CircuitPython_ServoKit

To use this library, open a new terminal on your Raspberry Pi and execute the following command:
`pip3 install adafruit-circuitpython-servokit`

## Usage example
Here we can see a full example:

```
from time import sleep
from adafruit_servokit import ServoKit

# Set channels to the number of servo channels on your kit.
# 8 for FeatherWing, 16 for Shield/HAT/Bonnet.
kit = ServoKit(channels=8)

kit.servo[0].angle = 175
sleep(1)
kit.servo[0].angle = 45
sleep(1)
``` 
We can specify the servo in the`kit.servo[0-15].`

## Result

![resultServos.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1633632215738/cwBnDf2JL.jpeg)


I really hope this post helped you out and feel free to share this with someone that might need it, see you next time!.
