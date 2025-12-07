# Introduction to Walking Gaits

## Learning Objectives

- Understand the concept of a walking gait and the phases of a step.
- Program a sequence of servo movements to create a basic walking motion.
- Troubleshoot and fine-tune the walking sequence for better stability.

## Prerequisites

- Lesson 1.2: Making it Move: Basic Servo Control

## Materials Needed

- Assembled bipedal robot from Lesson 1.1
- Microcontroller (e.g., Arduino Uno/Nano, ESP32, Raspberry Pi Pico)
- USB cable
- IDE with servo control setup from Lesson 1.2

## Introduction

Walking is arguably the most fundamental and complex movement for a bipedal robot. It requires precise coordination of multiple joints and careful balance. In this lesson, we'll dive into the concept of walking gaits – the rhythmic patterns of limb movement – and implement a simple, pre-programmed walking sequence for your robot. This will be a challenging but rewarding step towards autonomous bipedal locomotion.

## Step-by-Step Tutorial: Implementing a Basic Gait

A simple bipedal walking gait often involves a few key phases for each leg: lift, swing forward, lower, and push back. We'll simplify this for our small robot.

### 1. Identify Key Servos for Walking

For a basic bipedal robot, you'll typically have at least two servos per leg: one for hip (forward/backward swing) and one for ankle (lifting/lowering the foot). Some robots also have a hip servo for side-to-side motion. Let's assume you have hip (forward/backward) and ankle (up/down) for each leg.

-   **Right Leg Hip (RLH)**: connected to pin X
-   **Right Leg Ankle (RLA)**: connected to pin Y
-   **Left Leg Hip (LLH)**: connected to pin A
-   **Left Leg Ankle (LLA)**: connected to pin B

Adjust pin numbers and servo objects accordingly in your code.

### 2. Define Servo Home Positions

Before starting any motion, it's good practice to set all servos to a known "home" or "neutral" position where the robot stands stable.

### 3. Program a Simple "Shift and Step" Gait

This basic gait involves shifting weight to one leg, lifting the other, swinging it forward, putting it down, and then repeating on the other side.

```cpp
// Arduino Example for a basic walking gait
#include <Servo.h>

// Define servo objects
Servo rightHip; // Hip servo for right leg
Servo rightAnkle; // Ankle servo for right leg
Servo leftHip;  // Hip servo for left leg
Servo leftAnkle;  // Ankle servo for left leg

// Define servo pins (ADJUST THESE TO YOUR ROBOT'S WIRING)
const int RIGHT_HIP_PIN = 9;
const int RIGHT_ANKLE_PIN = 8;
const int LEFT_HIP_PIN = 10;
const int LEFT_ANKLE_PIN = 11;

// Define servo angles for home position (ADJUST FOR YOUR ROBOT)
const int RH_HOME = 90;
const int RA_HOME = 90;
const int LH_HOME = 90;
const int LA_HOME = 90;

// Define movement angles (ADJUST FOR YOUR ROBOT)
const int STEP_FORWARD = 120; // Example: 30 degrees forward from home
const int STEP_BACKWARD = 60;  // Example: 30 degrees backward from home
const int ANKLE_LIFT = 110;    // Example: 20 degrees up from home
const int ANKLE_LOWER = 90;    // Example: Back to home position

void setup() {
  rightHip.attach(RIGHT_HIP_PIN);
  rightAnkle.attach(RIGHT_ANKLE_PIN);
  leftHip.attach(LEFT_HIP_PIN);
  leftAnkle.attach(LEFT_ANKLE_PIN);

  // Set all servos to home position
  setHomePosition();
  delay(1000); // Wait for robot to stabilize
}

void setHomePosition() {
  rightHip.write(RH_HOME);
  rightAnkle.write(RA_HOME);
  leftHip.write(LH_HOME);
  leftAnkle.write(LA_HOME);
}

void loop() {
  // Step Right Leg Forward
  stepRightForward();
  delay(500); // Pause between steps

  // Step Left Leg Forward
  stepLeftForward();
  delay(500); // Pause between steps
}

void stepRightForward() {
  // 1. Shift weight to Left (optional, often done with hip sway)
  // For simplicity, we'll just lift and swing

  // 2. Lift Right Ankle
  rightAnkle.write(ANKLE_LIFT);
  delay(200);

  // 3. Swing Right Leg Forward
  rightHip.write(STEP_FORWARD);
  delay(300);

  // 4. Lower Right Ankle
  rightAnkle.write(ANKLE_LOWER);
  delay(200);

  // 5. Shift weight to Right / Push Left Back (optional, often combined)
  leftHip.write(STEP_BACKWARD); // Move left hip back to compensate
  delay(300);
  
  rightHip.write(RH_HOME); // Bring right hip back to home
  leftHip.write(LH_HOME); // Bring left hip back to home
  delay(200);
}

void stepLeftForward() {
  // 1. Shift weight to Right (optional)

  // 2. Lift Left Ankle
  leftAnkle.write(ANKLE_LIFT);
  delay(200);

  // 3. Swing Left Leg Forward
  leftHip.write(STEP_FORWARD);
  delay(300);

  // 4. Lower Left Ankle
  leftAnkle.write(ANKLE_LOWER);
  delay(200);

  // 5. Shift weight to Left / Push Right Back (optional)
  rightHip.write(STEP_BACKWARD); // Move right hip back to compensate
  delay(300);
  
  leftHip.write(LH_HOME); // Bring left hip back to home
  rightHip.write(RH_HOME); // Bring right hip back to home
  delay(200);
}
```

-   **Adjust Servo Pins and Angles**: This code is a template. You MUST adjust `RIGHT_HIP_PIN`, `RIGHT_ANKLE_PIN`, `LEFT_HIP_PIN`, `LEFT_ANKLE_PIN` to match your robot's wiring. You will also need to experiment with `RH_HOME`, `RA_HOME`, `LH_HOME`, `LA_HOME`, `STEP_FORWARD`, `STEP_BACKWARD`, `ANKLE_LIFT`, and `ANKLE_LOWER` values to find the stable range for your robot.
-   **Observe and Troubleshoot**: Upload the code. Your robot might wobble or fall initially. Observe its movements carefully. Which leg is off? Is it lifting enough? Is it swinging too far?

### 4. Fine-Tuning for Stability

-   **Small Steps First**: Start with very small `STEP_FORWARD` and `STEP_BACKWARD` angles.
-   **Slow Motion**: Increase `delay()` values to make movements slower, making it easier to observe and debug.
-   **Weight Distribution**: Ensure the robot's center of gravity is well-balanced. Adjust component placement if necessary.
-   **Trial and Error**: Walking gaits are complex. Expect many iterations of adjusting angles and delays.

:::warning Important
Always ensure your robot has enough power. Low battery can lead to erratic servo behavior and unstable walking.
:::

## How it Works: Bipedal Gaits

-   **Center of Mass (CoM)**: For stable walking, a bipedal robot must keep its CoM over its support polygon (the area on the ground defined by its feet).
-   **Support Phase**: When the robot has one or both feet on the ground.
-   **Swing Phase**: When one foot is lifted and moved forward.
-   **Zero Moment Point (ZMP)**: A concept used in advanced robotics to ensure dynamic stability. For simpler robots, we approximate this by shifting weight and carefully coordinating joint movements.
-   **Kinematics**: The study of motion of points, bodies, and systems of bodies without considering the forces that cause the motion. Understanding your robot's kinematics helps in determining appropriate joint angles.

## Challenge (Optional)

-   Can you modify the gait to make your robot turn slightly while walking?
-   Implement a "backwards" step.
-   Try to make your robot recover its balance if it starts to lean too much (this is advanced and might require sensors!).

## Conclusion & Next Steps

You've just programmed your robot to walk! This is a significant achievement in robotics. You've touched upon core concepts of locomotion and stability. While simple, this gait lays the foundation for more complex and intelligent movements. Keep experimenting with angles and timings. As you progress, you'll find that coordinating more joints and integrating sensor feedback will lead to even more impressive bipedal behaviors!
