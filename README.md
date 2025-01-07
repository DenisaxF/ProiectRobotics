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
### 1. Stadiul actual al implementării software
Proiectul este aproape finalizat. Robotul poate detecta focul prin senzorii IR și se poate deplasa în consecință, indreptandu-se spre flacara și activând pompa pentru a stropi cu apă atunci când este nevoie. Direcția jetului de apă este controlată de un servomotor. Codul este deja implementat și funcționează conform așteptărilor, iar robotul răspunde corect în diferite situații.

### 2. Motivația alegerii bibliotecilor
Am folosit biblioteca standard Arduino.h, care oferă toate funcțiile necesare pentru controlul motoarelor și al servomotorului. Nu am folosit biblioteci externe, deoarece funcțiile disponibile în biblioteca standard sunt suficiente pentru ceea ce aveam nevoie, iar astfel am păstrat controlul total asupra codului.

### 3. Elementul de noutate al proiectului
Elementul de noutate al acestui proiect este integrarea senzorilor IR pentru detecția focului și utilizarea unui servomotor pentru direcționarea jetului de apă. Robotul este capabil să navigheze autonom și să aplice apă în funcție de obstacolele detectate. Acesta reprezintă un pas important în dezvoltarea unui robot cu funcționalități inteligente de reacție.

### 4. Justificarea utilizării funcționalităților din laborator
Am folosit funcționalitățile învățate în trei laboratoare:

Laboratorul 0: Controlul de bază al Arduino-ului, cum ar fi utilizarea funcțiilor pinMode, digitalWrite, și analogWrite pentru controlul motoarelor și servomotorului. Aceste funcții sunt esențiale pentru a putea controla hardware-ul robotului.

Laboratorul 1: Controlul motoarelor cu ajutorul unui H-Bridge, folosind modulul L298. Aceasta permite controlul direcției și vitezei motoarelor pentru mișcarea robotului.

Laboratorul 2: Utilizarea senzorilor IR pentru detectarea obstacolelor. În codul meu, senzorii IR sunt folosiți pentru a citi valorile și a lua decizii despre mișcarea robotului în funcție de prezența sau absența focului.

Aceste funcționalități sunt esențiale pentru a crea un robot autonom care să răspundă corect la condițiile de mediu.

### 5. Explicația scheletului proiectului și interacțiunea dintre funcționalități
Proiectul este structurat astfel:

Controlul motoarelor: Folosind pinii de pe L298, controlăm motoarele robotului pentru a-l face să se miște înainte, înapoi sau să vireze.
Senzorii IR: Senzorii din față, dreapta și stânga sunt folosiți pentru a detecta focul. În funcție de valorile citite, robotul poate schimba direcția sau poate opri pentru a stropi cu apă.
Pompa de apă și servomotorul: Când un obstacol este detectat, robotul oprește mișcarea, pornește pompa de apă și ajustează servomotorul pentru a direcționa jetul de apă.
Logica de control: Algoritmul verifică în mod constant valorile senzorilor IR și ajustează comportamentul robotului pe baza acestora. Dacă nu sunt obstacole, robotul se mișcă înainte, iar în caz contrar, efectuează viraje și poate stropi cu apă.

### 6. Calibrarea senzorilor
Senzorii IR au fost calibrați pentru a reacționa corect la diferite distanțe. Am stabilit praguri pentru fiecare senzor (dreapta, față și stânga) astfel încât robotul să poată detecta apropierea unui obstacol și să reacționeze corespunzător. Aceste valori au fost testate pentru a asigura o detecție fiabilă.

### 7. Optimizările realizate
Am realizat câteva optimizări importante în cod:

Viteza motoarelor: Am folosit două nivele de viteză – una normală și una mai mare pentru viraje. Aceasta îmbunătățește manevrabilitatea robotului.
Controlul servomotorului: Mișcările servomotorului au fost reglate pentru a fi mai precise, astfel încât jetul de apă să poată fi direcționat cu mai multă acuratețe.

## Results
TBD

## Conclusions
The Fire Fighting Robot successfully demonstrates how autonomous systems can detect and extinguish flames without external control. This project highlights the potential of robotics in firefighting, providing a foundation for future improvements and innovations.
## Source Code and Other Resources to Include on GitHub
TBD

## Bibliography/Resources
TBD
