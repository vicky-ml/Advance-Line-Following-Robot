# Advance-Line-Following-Robot

YEAR-1 Project

Advance Line Following Robot Using Arduino UNO
1.0	 INTRODUCTION:

1.1	OVERVIEW:

Robots are widely used in industries as they became more affordable and efficient. However, robots still tend to make some errors and their task won’t be perfectly accurate. To overcome this a better controller can be implemented which allows the robot to perform efficiently and make fewer errors. A line following robot is an autonomous vehicle which is capable of following a given path. We made a traditional line following robot which consists of a chassis, IR sensors, microcontrollers, DC motors and motor driver. This project tries to implement PID controller on the prebuilt line following robot and thus trying to reduce the errors made by the line following robot while moving. The robot consists of a sunfounder line following module which consists of array of 8 IR sensors through which the robot detects the black line and follows the path. The PID is implemented so that the robot will be able to follow the given black line effectively and smoothly. 
The control system used here senses the black line and maneuvers the robot to stay on course while constantly correcting the wrong moves using PID control. 

1.2	 OBJECTIVES:

•	Learn how to use the I2C interface and process data from sensors to achieve simple navigation.
•	Design an advance line following robot which works on PID control system.
•	Learn how to use the MPU-6050 gyro accelerometer sensor module and allow the robot to navigate a simple path that leads to the ramp and measure its gradient and also, to make a 360 degrees turn over the ramp using the yow value of the MPU-6050 value after a 3 seconds delay after reaching the top of the ramp.
•	Implement a weighted average algorithm and demonstrate its operating principle for a range of reference points by recording the reflectivity value profiles as the sensor is moved over a black line on a white background.
•	 Learn to tune the values of PID constants to get the best possible performance.

2.0 MPU-6050 Gyro Accelerometer Sensor Module:
It is the world’s first integrated 6-axis MotionTracking device.
                          

The InvenSense MPU-6050 sensor contains a MEMS accelerometer and a MEMS gyro in a single chip which is processed by the Digital Motion Processor. It is very accurate, as it contains 16-bits analog to digital conversion hardware for each channel. Therefore, it captures the x, y, and z channel at the same time. The sensor uses the standard I2C bus for data transmission. The MPU-6050 always acts as a slave to the Arduino with the SDA and SCL pins connected to the I2C-bus. The connection layout of MPU-6050 to the Arduino is given below.
 

The primary use of the MPU-6050 module in our project is to measure the angle of the ramp on either side and print the output on the LCD display. We have also used this module to make a 360 degrees turn by measuring the yaw value. When the robot climbs the ramp, the value is processed by the DMP(Digital Motion Processor). The maximum value processed is then displayed on the LCD screen as ramp angle.

2.1 APPLICATIONS OF MPU-6050 GYROSCOPE:
•	Motion-enabled game and application framework
•	Location-based services, points of interest
•	Handset and portable gaming
•	Motion-based game controllers
•	Wearable sensors for health, fitness, and sports
•	Toys

3.0 INTER-INTEGRATED COMMUNICATION (I2C BUS):
3.1 Overview:
The I2C bus is a very popular mode of communication. Through I2C bus, the communication can be easily implemented between the master and slave devices. The fact that a multiple numbers of master and slave modules can be connected with just two wires makes it more efficient and easy to use. Master is the device that generates the clock, starts communication, sends I2C commands and stops communication. The slave is the device that listens to the bus and is addressed by the master Multi-master I2C can have more than one master and each can send command.
 

3.2 Woking of the I2C Bus:
The two wires are called Serial Cloak Line(SCL) and Serial Data Line(SDA). The SCL will synchronize the data transfer between the devices on the I2C bus and it is generated by the master device. The SDA line carries the data. Data are transferred in a sequence of 8-bits which are sent with the most significant bits first. They can have up to 128 devices. Now to communicate with the relevant devices, we first need to find the unique address of that device. Each Slave device has to have its own unique address and both master and slave devices need to take turns communicating over the same data line. 
Now we have to create the relevant code to initiate the I2C bus communication. We can use the Arduino Wire Library. Firstly, we need to define the sensor address and internal register addresses. Then, the Wire.begin() function is used to initiate the Arduino wire library and the serial communication.  
After the addressing, the data transfer sequences begin either from the master or the slave depending on the selected mode at the R/W bit. After the data is completely sent, the transfer will end with a stop condition which occurs when the SDA line goes from low to high while the SCL line is high.
4.0 SUNFOUNDER IR SENSORS:
The robot uses Sunfounder IR sensor module to sense the line. It consists of an array of 8 IR sensors faced towards the ground. The communication between the module and the Arduino is done by I2C bus. The sensor module is fixed to the robot by using a 3-d printed IR sensor holder which is designed using SolidWorks software. 4.1 CALIBRATION OF THE LINE FOLLOWER SENSOR MODULE:
We need to calibrate the output from the sensor array since not every sensor give the same value. Therefore, individual sensors are calibrated to return a maximum and minimum value ranging from 0 to 1000, so that it can find which sensor detects the black line and thus moves and corrects the position of the robot. The calibration process can be done easily, refer the flowchart below to know how calibration process works.
 
Once the values have been noted down, the individual values from the sensors for black and white readings need to be mapped to a common range. The flowchart below shows how to map the acquired readings and get the calibrated values.


An analog signal is obtained in the output based on the amount of reflected light and is fed to the comparator and the digital signal is sent to the microcontroller. Here, the analog signal is converted into digital by the array.
4.2 Weighted Average Algorithm for Line Following:
A weighted average algorithm can provide a measure of error. Each sensor is calibrated to return a maximum and minimum value. The center point of the sensor module forms the reference point. Each sensor point is given a weighting. i.e., distance from the reference point which is given by,
 

Consider the following schematic of the sensor module,
 
Let's assume that when the sensor senses the black line, it reads 0 and when it is off the black line, it reads 1. The microcontroller corresponds to the algorithm and executes the next movement in such a way that the center most sensors(L1 and R1) reads 0 and the rest of the sensors read 1. In this way, we need to do the calibration process and implement the weighted average algorithm.

5.0 The PID CONTROL SYSTEM:
A PID controller is a feedback loop system.
The basic idea is to steer the robot towards the line, and the farther off it is, the more it corrects itself.
The PID algorithm can be described as the following equation.
 
The output from the PID controller is used to change the speed of the motors.
The basic terminology of the PID control system is as follows.
Proportional(P)- The proportional constant directly multiplies the error and should, therefore, set a reasonable motor speed change given the error magnitude.
Integral(I)- The integral component multiplies a running sum of the error, therefore, its effect increases the longer the robot is not on track.
Differential(D)- The differential component multiplies the change in error, therefore, its effect depends on how quickly the line is changing compared to the course of the robot.
The figure below gives an overview of the PID constant and its individual contribution to the control system.
 

 
The process is a feedback loop as shown in the figure 1.8. Such a design allows the maneuver robot on the track with the implementation of PID controller.
5.1 An overview of how PID Control System works in a line following robot:  
5.2 TUNING THE PID CONSTANTS:
 In this project, we used trial and error approach to design the PID controller.
 The first step of creating a PID feedback loop is to define our desired position. We need to calibrate the values by simply moving the robot across the line and note its readings
 We need to add the error value to the output by measuring the center point deviation of the line. If the robot deviates from the black line, a proportional constant is given to bring the robot back to the black line as quick as possible. But, to prevent the robot from overshooting, a derivative constant is given. This corresponds to the rate of change of error. The integral constant is used to improve the accuracy and smoothness of the movement of the robot. It corresponds to the sum of the recent errors.
 The terms in the PID equation namely Kp-pfactor, Ki-ifactor, Kd-dfactor is a constant value used to increase or decrease the impact of the proportion, integral and derivative respectively.

CONTROL VARIANT	DESCRIPTION	FINAL COEFFICIENT VALUE
PROPORTIONAL	Kp*error: The constant of proportionality is the gain of Kp. The proportional value determines the reaction to the current error. It reduces the large part of the error based on present time error.	20
INTEGRAL	Ki*integral: The integral improves the steady state performance of the robot. It determines the reaction based on the sum of the recent errors. It eliminates the steady state error. It reduces the final error in the system based on the log of the previous errors over time.	10
DERIVATIVE	Kd*(error-lasterror): The derivative corresponds to the rate of change of error. Has an element of prediction of future errors. React to rapid rate of change before error grows to big. It stabilizes the system and thus prevents overshoot. It conteracts the Kp and Ki values quickly when the output changes	100

5.3 The overall program flow:
 
6.0 Conclusion:
 In our project we implemented the PID control system and used the microcontroller to build a line following robot. Our expectation for this project is to make the car move with PID controller and use the MPU-6050 module to display the angle of the ramp kept in the track, climb down the track and move for certain distance and show the angle of the other side of the ramp. Though we achieved the ultimate goal of the project, we faced many challenges during the making of the bot.
 One main challenge was the MPU-6050 library crashed whenever new codes are added to it. To overcome that issue, we edited the library code so that it gets executed in a loop. Therefore, the code gets looped back to be reset until the desired sensor value is obtained.
 There are many flaws in the design and operation of our robot. The movement of our robot was not smooth as there was high degree of oscillation in the movement of the robot. That was because the PID constants that we used were not so accurate. Also, the initial placement of the robot has to be at the center of the black line. If not, the initial error will not be accurate and the robot may fail to follow the track smoothly.

The output on the LCD screen is given below.
 


Here are some methods that can improve the performance of our line following robot.
•	Fine tune of Kp and Kd parameters used in the PID controller.
•	Implementing PID constants by using Zeigler-Nichols tuning method as this would give better accuracy.
•	Better placement of sunfounder line follower sensor module.
•	Use of fully charged battery to get a better output in the motors.
Thus, our advance line following robot was able to complete the track more smoothly and accurately, unlike the last project week where we used normally if statements to move the. 

7.0 References:
1.	Jamie. PID Control. Arduino Platforms. [Online][cited: 1yr ago] https:// car www.mvcode.com/lessons/pid-control-jamie.
2.	Arduino official. MPU-6050 Arduino platforms.[Online] https://playground.arduino.cc/Main/MPU-6050.
3.	MTaylor. Line Follower Array Hookup Guide. [Online] https://learn.sparkfun.com/tutorials/sparkfun-line-follower-array-hookup-guide/introduction.
4.	Peter Harison. Simpler Line follower sensors. [Online][Cited: April 15, 2011] http://www.micromouseonline.com/2011/04/15/simpler-line-follower-sensors/.
5.	 Dejen Nedelkovski. Arduino Tutorial. [Online] http://howtomechatronics.com/tutorials/arduino/how-i2c-communication-works-and-how-to-use-it-with-arduino/.
6.	Enigmerald. PID Tutorials for Line Following. [Online] [cited: January 6, 2014] https://www.robotshop.com/letsmakerobots/pid-tutorials-line-following.
 
Appendix:

What is a control system?
A control system is an interconnection of components forming a system configuration that will provide the desired system response. It can be generally classified into two types.
•	Open loop control system
•	Closed loop control system
In this project, we used closed loop control system. The characteristics of closed loop control system are:
•	Needs a measurement element at plant output.
•	Control is error driven.
•	Responds to unmeasured disturbances.
A key element of the closed loop system is that the controller works based on an error signal – the difference between the desired output (setpoint) and the actual output. It attempts to minimise the error.
A detailed explanation of how PID control system works.
The error is a measure of how far the cart is from the track. The further the car is off the track, the larger the error.
More specifically we can say that error is the difference between the current position and the target position.
 
The error will be negative when the car is on the right side of the black line. Similarly, the error will be positive when the car in on the left side. 
 

The Fig.     shows how the speed of the wheel is changed based on the error value obtained
