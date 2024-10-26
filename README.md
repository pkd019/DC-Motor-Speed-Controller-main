# DC Motor Speed Control System

This repository contains the code and resources for a DC Motor Speed Control System that leverages an ESP8266 module, motor driver IC, and a rotary potentiometer to achieve precise control over the speed of a DC motor.

## Table of Contents

- [Introduction](#introduction)
- [Demo](#demo)
- [Circuit Diagram](#circuit-diagram)
- [Simulation](#simulation)
- [Setup Instructions](#setup-instructions)
- [Contributing](#contributing)

## Introduction

The DC Motor Speed Control System enables dynamic and accurate manipulation of the rotational speed of a DC motor. By integrating an ESP8266 module, motor driver IC, and a rotary potentiometer, the system offers versatile control options for various applications requiring varying motor speeds.

## Components
|  Name  | Quantity |      Component       |
|:------:|:--------:|:-------------------:|
|   U1   |    1     |   Arduino Uno R3    |
|  Rpot1 |    1     | 250 kΩ Potentiometer |
|  BAT1  |    1     |     9V Battery      |
|   M1   |    1     |      DC Motor       |
|   U2   |    1     | H-bridge Motor Driver|


## Demo

[Will upload the demo of the project on youtube soon]

## Circuit Diagram

![DC Motor Speed Control.png](https://github.com/adityakanu/DC-Motor-Speed-Controller/blob/1ac5bb0daf33675a4b12b25ef59dfe2687ae771b/DC%20Motor%20Speed%20Control.png)

Also Look upon: [Schematic View](https://github.com/adityakanu/DC-Motor-Speed-Controller/blob/db0a11e33d6380ee50a626cfbe1fb06d776e3463/DC%20Motor%20Speed%20Control.pdf)

In the circuit diagram, we have an intricate arrangement of components that collaborate to achieve precise control over the motor speed. The key components involved are the ESP8266 module, motor driver IC, and rotary potentiometer. Let's break down their roles and connections in detail:

  - ESP8266 Module (U1):
    The ESP8266 acts as the brain of the system, providing connectivity and programmability. It is connected to the motor driver IC and the rotary potentiometer to facilitate communication and control.

  - Motor Driver IC (U2):
    The motor driver IC serves as the interface between the ESP8266 and the DC motor (M1). It allows the microcontroller (ESP8266) to control the motor's speed and direction.

  - Rotary Potentiometer (Rpot1):
    The rotary potentiometer is a variable resistor that provides an analog input to the ESP8266. Its shaft can be rotated to change its resistance, effectively altering the voltage input to the ESP8266.

Connections:

  - ESP8266 to Motor Driver IC (U2):
        Digital pins from the ESP8266 are connected to the motor driver IC's control inputs. These pins enable the microcontroller to send control signals to the motor driver.
        By toggling these pins, the ESP8266 can specify the direction of motor rotation (clockwise or counterclockwise) and control the motor speed.

  - ESP8266 to Rotary Potentiometer (Rpot1):
        One terminal of the rotary potentiometer is connected to the ESP8266's analog input pin. This pin reads the voltage level produced by the potentiometer.
        The other terminal of the potentiometer is connected to ground (GND) to create a voltage divider circuit.
        As the potentiometer's shaft is turned, its resistance changes, causing the voltage at the analog pin to vary.

  - Motor Driver IC to DC Motor (M1):
        The motor driver IC has output pins (typically labeled as "OUTA" and "OUTB") that are connected to the DC motor's terminals.
        These output pins control the voltage and direction applied to the motor, determining its speed and rotation.

  Working Together:

  - The ESP8266 reads the analog input from the rotary potentiometer, which corresponds to the desired motor speed. The potentiometer effectively acts as a speed control dial.

  - Based on the potentiometer's reading, the ESP8266 calculates the appropriate control signals to send to the motor driver IC.

  - The motor driver IC interprets the control signals from the ESP8266 and adjusts the voltage and direction applied to the DC motor.

  - The DC motor responds to the motor driver's output, causing it to rotate at the desired speed and direction as indicated by the potentiometer setting.

## Simulation

You can simulate the DC Motor Speed Control System using [Tinkercad](https://www.tinkercad.com/). Click [here](https://www.tinkercad.com/things/aMfq4ZoMnF4) to access the simulation.

1. Start the simulation
2. Rotate the potentiometer and observe the speed mentioned on the Motor in RPM.

Note: We have used Arduino UNO in the simulation since Tinkercad lacks the ESP8266 board for simulation.

## Setup Instructions

Follow these steps to set up and run the DC Motor Speed Control System:

1. Hardware Connections and Initial Setup:

    - Connect the ESP8266 to your computer using a USB cable and open your preferred Arduino development environment.
    - Connect the motor driver IC to the ESP8266 using digital pins for control inputs (e.g., IN1, IN2) and analog pins (e.g., A0) for reading the potentiometer value.
    - Attach the DC motor to the motor driver IC's output pins (OUTA and OUTB).
    - Supply power to the motor driver IC and the ESP8266. This may involve connecting a power source, such as a battery or power supply, to appropriate pins on the motor driver IC and ESP8266.
    - Make sure all ground (GND) connections are properly connected to create a common ground reference.

2. ESP8266 Communication and Speed Control:

   - Upload the relevant code to the ESP8266, which includes libraries for communication and motor control.
   - Initialize the necessary pins on the ESP8266 for communication with the motor driver IC (e.g., IN1, IN2) and for reading the potentiometer (e.g., A0).
   - Set up the ESP8266 to read the analog value from the potentiometer using the analogRead() function.
   - Map the analog potentiometer reading to a motor speed range that corresponds to the motor driver's control signals. For example, map the potentiometer's value (0-1023) to a motor speed value (0-255).
   - Send appropriate control signals to the motor driver IC based on the mapped motor speed value. For instance, if the mapped value is greater than a certain threshold, set one control input pin high and the other low to rotate the motor clockwise, and vice versa for counterclockwise rotation.

3. Configuration Settings and Calibration:

    - Fine-tune the mapping between potentiometer values and motor speed to achieve desired speed ranges and responsiveness.
    - Adjust the threshold value that determines the direction of motor rotation based on potentiometer readings.
    - Test the system by turning the potentiometer and observing the motor's speed changes. Make necessary adjustments to ensure smooth and accurate speed control.
    - Consider implementing safety measures, such as setting speed limits or incorporating emergency stop functionality.
  
4. Code:
    - Include Libraries: The code includes a library called "Servo" that helps control a servo motor.
    - Define Constants: It sets up some constants, such as pin numbers for the LDRs, a desired ratio ("setpoint") for sunlight, and some tuning parameters for a control algorithm (PID).
    - Initialize Servo: It attaches a servo motor to pin 9 and reads the initial LDR values.
    - Initial Servo Position: It checks if the LDR values are balanced (within a tolerance).It initializes the servo angle to 120 degrees. If not, it sets the servo angle based on which LDR has more light.
    - Setup Serial Communication: It starts serial communication for debugging.
    - Main Loop (loop()):
        It continuously reads the LDR values.
        Calculates the current ratio of LDR values.
        Computes an "error" which is the difference between the desired ratio and the current ratio.
        Initializes some variables for a control algorithm (PID).
    - PID Control:
        It adjusts the control parameters (Kp) based on the current position of the servo.
        Calculates proportional, integral, and derivative terms for the control.
        The integral term is constrained to prevent excessive accumulation.
        The servo angle (Spoint) is calculated using these control terms and constraints.

    - Update Servo: It sets the servo angle to Spoint based on the control calculations.
    - Debugging: It prints out information like the current ratio, error, and servo angle for debugging.
    - Delay: A small delay is added to stabilize the system.

In summary, this code uses LDR sensors and a servo motor to adjust the solar panel's angle, keeping it aligned with the sun for optimal energy capture. It employs a control algorithm (PID) to calculate the right angle based on the ratio of light detected by the LDRs and adjusts the solar panel accordingly. This ensures that the solar panel generates more energy by continuously facing the sun.

## Contributing

Contributions are welcome! If you'd like to contribute to the project via documentation or better circuit design and improvements, please follow these steps:

1. Fork the repository.

2. Create a new branch for your feature or enhancement: `git checkout -b feature-name`.

3. Make your changes and commit them: `git commit -m 'Description of your changes'`.

4. Push to the branch: `git push origin feature-name`.

5. Open a pull request.


