# Your First Bipedal Walker: Assembling the Kit

## Learning Objectives

- Identify the key components of a simple humanoid robot (servos, microcontroller, chassis, power source).
- Assemble the robot kit following a detailed guide.
- Understand the function of each component.

## Prerequisites

- None. This is your very first step!

## Materials Needed

- A bipedal robot kit (e.g., a simple Arduino-compatible kit)
- Basic tools (small screwdrivers, pliers, wire cutters if needed)
- A clear, well-lit workspace

## Introduction

Welcome to the exciting world of physical AI and humanoid robotics! In this first lesson, we'll get our hands dirty by assembling a simple bipedal (two-legged) robot. This hands-on experience will introduce you to the fundamental physical components that make up a robot and how they interact. Don't worry if you're new to this; we'll guide you through every step. By the end of this lesson, you'll have a physically built robot ready for its first movements!

## Step-by-Step Tutorial: Assembling Your Robot

Follow the instructions provided with your specific robot kit. The general steps usually involve:

### 1. Unpacking and Identifying Components

- Lay out all the components from your kit.
- Identify the main parts:
    - **Chassis/Frame**: The main body structure of your robot.
    - **Servo Motors**: These are the "muscles" that will move your robot's joints. Note their size and type (e.g., micro servos, standard servos).
    - **Microcontroller Board**: The "brain" of your robot (e.g., Arduino Nano, ESP32).
    - **Battery Holder/Power Source**: To supply power to your robot.
    - **Wires/Cables**: For connecting components.
    - **Fasteners**: Screws, nuts, standoffs.

### 2. Assembling the Legs and Joints

- Attach the servo motors to the leg segments. Pay attention to the orientation as indicated in your kit's manual.
- Securely fasten all screws. Ensure joints can move freely without excessive wobble.

### 3. Mounting the Chassis

- Attach the assembled legs to the main chassis or body of the robot.
- Ensure the robot can stand upright with support before proceeding.

### 4. Wiring the Servos to the Microcontroller

- Connect each servo motor to the designated pins on your microcontroller board.
- Refer to your kit's wiring diagram carefully. Typically, each servo has three wires: Power (VCC, red), Ground (GND, brown/black), and Signal (yellow/orange).

### 5. Connecting the Power Source

- Connect the battery holder or power source to the microcontroller.
- **Double-check polarity** (+ to +, - to -) to avoid damaging components.

:::info Tip
Take your time with assembly. Rushing can lead to errors that are hard to troubleshoot later. Refer to your kit's manual constantly!
:::

## How it Works: The Anatomy of a Simple Robot

A simple bipedal robot, like the one you're assembling, relies on a few key principles:

-   **Structure (Chassis/Frame)**: Provides the physical form and support, defining the robot's kinematics (how its parts move relative to each other).
-   **Actuators (Servo Motors)**: These are responsible for movement. Servos take an electrical signal and convert it into precise angular motion, allowing the robot to change joint positions.
-   **Control (Microcontroller)**: The microcontroller (like an Arduino) is a small computer that reads instructions (your code) and sends commands to the servos to tell them how to move.
-   **Power (Battery)**: Supplies the necessary electrical energy to all components.

## Challenge (Optional)

-   Can you identify any parts in your kit that you didn't use? Research their purpose and think about how they might enhance your robot's capabilities in the future.
-   Try to draw a simple diagram of your assembled robot, labeling its main components and how they are connected.

## Conclusion & Next Steps

Congratulations! You've successfully assembled your first bipedal robot. You now have a tangible platform to start experimenting with physical AI. In the next lesson, we'll bring this robot to life by learning how to program its servo motors to make it move. Get ready to write your first lines of code for your robot!
