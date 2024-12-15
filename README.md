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
- Flame sensors(x3)
- Servomotor
- L298N Motor Driver
- Water Pump + pipe + bottle
- 1k Resistor
- Tip122 Transistor
- 104pf capacitor
- 1.5V batteries(x4)

### Their roles:

#### 1) Microcontroller - Arduino Uno
It is the brain of the project. It receives signals from the sensors, processes data, and controls the motors, water pump, and servo motor.
Operates at 5V and provides digital and analog pins for interfacing with the other components.

#### 2) IR Sensors (x3)
Used to detect fire. These sensors emit an analog signal based on the intensity of infrared light detected.
Pins Used:
A0 - Right sensor (IR_R)
A1 - Front sensor (IR_F)
A2 - Left sensor (IR_L)

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


## Software Design
TBD

## Results
TBD

## Conclusions
The Fire Fighting Robot successfully demonstrates how autonomous systems can detect and extinguish flames without external control. This project highlights the potential of robotics in firefighting, providing a foundation for future improvements and innovations.
## Source Code and Other Resources to Include on GitHub
TBD

## Bibliography/Resources
TBD
