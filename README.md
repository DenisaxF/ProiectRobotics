# Fire Fighting Robot

## Introduction
The goal of this project is to build an autonomous firetruck equipped with fire sensors, capable of detecting a flame, moving towards it on its own, and extinguishing it by spraying water, without the need for a controller or any external input.

## General Description
TBD

## Hardware Design
### Components:
- Arduino uno
- Breadboard
- Wires
- Wheels(x4)
- DC motors(x4)
- IR Flame sensors(x3)
- Servomotor
- L298N Motor Driver
- Water Pump + pipe + bottle
- 1k Resistor
- Tip122 Transistor
- 104pf capacitor
- 1.5V Alcaline batteries(x4)

### Their roles:

#### 1) Microcontroller - Arduino Uno
It is the brain of the project. It receives signals from the sensors, processes data, and controls the motors, water pump, and servo motor.
Operates at 5V and provides digital and analog pins for interfacing with the other components.

#### 2) IR Sensors (x3)
Used to detect fire. These sensors emit an analog signal based on the intensity of infrared light detected.
Pins Used:
A0 - Right sensor
A1 - Front sensor
A2 - Left sensor

#### 3) L298N Motor Driver Module
Controls the movement motors of the robot (4 DC motors). It allows motors to rotate in both directions (forward/backward).
Pins Used:
enA (pin 10) and enB (pin 5) for speed control.
in1 (pin 9), in2 (pin 8), in3 (pin 7), in4 (pin 6) for rotation direction.

#### 4) DC Motors (x4)
Ensure the robot moves forward, backward, and rotates left/right. Powered through the L298N module.
Power Supply: 6-12V (from the battery).

#### 5) Water Pump
Activated to extinguish fire once the IR sensors detect flames.
Controlled through pin A5, activated using a transistor to handle the higher current.
If you don’t have a transistor, the pump can be connected to the motor driver (L298N) as an additional motor.

#### 6) Servo Motor
Moves the water pump in a specific direction (left-right) to target the fire.
Pin Used: A4
Controlled using PWM signals to adjust the angle of movement.

#### 7) External Battery
Supplies power to the robot and components with the required voltage (6-12V).

| Component | Quantity | Description | Link/Datasheet |
| --- | --- | --- | --- |
| Arduino Uno | 1 | Microcontroller for main control | (https://docs.arduino.cc/hardware/uno-rev3/) |
| DC Motors | 4 | 6V DC motors for robot movement | (https://www.contact-evolution.ch/files/DC_motors.pdf) | 
| Motor Driver (L298N) | 1 | motor control | https://www.handsontec.com/dataspecs/L298N%20Motor%20Driver.pdf | 
| IR Sensors | 3 | flame detecting | https://moviltronics.com/wp-content/uploads/2019/10/KY-026.pdf?srsltid=AfmBOorAuu77AL-C2YhF83Awy0Aa1kTbRJ0Hwox2YXZ_Z9UAM80GI-W- | 
| Mini submersible ater pump | 1 |  for extinguishing fire with water | https://5.imimg.com/data5/IQ/GJ/PF/SELLER-1833510/dc-mini-submersible-water-pump.pdf | 
| Servo Motor | 1 | for sensor positioning |  (http://www.ee.ic.ac.uk/pcheung/teaching/DE1_EE/stores/sg90_datasheet.pdf) | 
| Battery Pack| 1 | 6V supply for robot power | |


### Block Diagram
![Screenshot 2024-12-15 194104](https://github.com/user-attachments/assets/5cc37da7-7beb-4c15-9bb8-4f00f39e604f)


### How the Hardware Works
- Fire Detection

The IR sensors detect flames and send analog values to the Arduino. These values are compared to determine the flame’s position (left, right, or front).

- Movement Control

Based on sensor data, the Arduino controls the DC motors via the L298N motor driver to move the robot towards the fire.

- Extinguishing Fire

Once the flame is located, the water pump is activated (pin A5), and the servo motor directs the water stream toward the fire.

- Interfacing

Arduino controls each component using digital/analog pins and generates PWM signals for the servo motor and motors.

### Energy Consumption
- DC Motors: approx. 120-150mA per motor during operation.
- Water Pump: around 200-300mA at startup.
- Arduino Uno: consumes approximately 50mA.
- Servo Motor: variable consumption, between 100-250mA, depending on the load.
- The total power supply must be sufficient for all components, so an external 6-12V battery with enough current (>2A) is recommended.

### Photo and video of the hardware
![WhatsApp Image 2024-12-19 at 13 29 54](https://github.com/user-attachments/assets/10f12fbc-c04f-4372-b6c6-4848c6c141be)

https://github.com/user-attachments/assets/c379b742-689b-42df-9c76-22ce1434192c

### Circuit diagram
![schema_electrica](https://github.com/user-attachments/assets/7654da02-bc1b-4ef6-a6c0-e2fe75982605)
Observations: the software doesn t include an on-off switch button so i used a simple push button instead in this virtual diagram.

## Software Design
### 1. Current Status of Software Implementation
The project is almost complete. The robot can detect fire using IR sensors and move accordingly, heading toward the flame and activating the pump to spray water when necessary. The water jet's direction is controlled by a servomotor. The code has been implemented and functions as expected, with the robot responding correctly in various scenarios.

### 2. Motivation for Choosing Libraries
We used the standard Arduino.h library, which provides all the necessary functions for controlling the motors and the servomotor. No external libraries were used since the functions available in the standard library are sufficient for our needs, allowing us to maintain full control over the code.

### 3. Novelty of the Project
The novelty of this project lies in the integration of IR sensors for fire detection and the use of a servomotor to direct the water jet. The robot is capable of autonomous navigation and applying water based on detected obstacles. This is a significant step toward developing a robot with intelligent reaction capabilities.

### 4. Justification for Using Laboratory Functionalities
We utilized functionalities learned in three labs:

Lab 0: Basic Arduino control, such as using pinMode, digitalWrite, and analogWrite for controlling the motors and servomotor. These functions are essential for interacting with the robot's hardware.
Lab 1: Controlling motors with an H-Bridge using the L298 module. This enables control of the motors' direction and speed for the robot's movement.
Lab 2: Using IR sensors to detect obstacles. In our code, IR sensors are used to read values and make decisions about the robot's movement based on the presence or absence of fire.
These functionalities are crucial for creating an autonomous robot that responds correctly to environmental conditions.

### 5. Explanation of Project Structure and Interaction Between Functionalities
The project is structured as follows:

Motor Control: Using L298 pins, we control the robot's motors to move forward, backward, or turn.
IR Sensors: Front, right, and left sensors are used to detect fire. Depending on the readings, the robot can change direction or stop to spray water.
Water Pump and Servomotor: When an obstacle is detected, the robot stops moving, starts the water pump, and adjusts the servomotor to direct the water jet.
Control Logic: The algorithm continuously checks the IR sensor values and adjusts the robot's behavior accordingly. If no obstacles are detected, the robot moves forward; otherwise, it performs turns and may spray water.
### 6. Sensor Calibration
The IR sensors were calibrated to respond correctly at different distances. Thresholds were set for each sensor (right, front, and left) to ensure the robot could detect nearby obstacles and react accordingly. These values were tested to ensure reliable detection.

### 7. Optimizations Made
Several key optimizations were implemented in the code:

Motor Speed: Two speed levels were used – one normal and one higher for turning. This improves the robot's maneuverability.
Servomotor Control: The servomotor movements were fine-tuned for greater precision, allowing the water jet to be directed more accurately.

### 8. Video with the functionality

https://youtube.com/shorts/N-WnGlNRIIY?feature=share

## Results
TBD

## Conclusions
The Fire Fighting Robot successfully demonstrates how autonomous systems can detect and extinguish flames without external control. This project highlights the potential of robotics in firefighting, providing a foundation for future improvements and innovations.
## Source Code and Other Resources to Include on GitHub
TBD

## Bibliography/Resources
TBD
