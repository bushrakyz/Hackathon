# Making it Move: Basic Servo Control

## Learning Objectives

- Set up the development environment for the microcontroller.
- Write a script to control the position of a servo motor.
- Make the assembled robot perform a simple, pre-programmed movement.

## Prerequisites

- Lesson 1.1: Your First Bipedal Walker: Assembling the Kit

## Materials Needed

- Assembled bipedal robot from Lesson 1.1
- Microcontroller (e.g., Arduino Uno/Nano, ESP32, Raspberry Pi Pico)
- USB cable for connecting the microcontroller to your computer
- Integrated Development Environment (IDE) compatible with your microcontroller (e.g., Arduino IDE, VS Code with PlatformIO, Thonny for MicroPython)

## Introduction

Now that your robot is physically assembled, it's time to bring it to life! In this lesson, you'll learn how to program the microcontroller to send commands to the servo motors, making your robot move. We'll start with controlling a single servo and then expand to make your robot perform a simple action like waving. This is where the "physical AI" journey truly begins!

## Step-by-Step Tutorial: Programming Basic Movements

We'll use a common microcontroller programming approach. Adjust the specifics based on your chosen board (Arduino example provided).

### 1. Set Up Your Development Environment

-   **Install IDE**: If you haven't already, install the appropriate IDE for your microcontroller (e.g., Arduino IDE from [arduino.cc](https://www.arduino.cc/en/software)).
-   **Install Board Support**: Add support for your specific board within the IDE (e.g., ESP32 boards in Arduino IDE, or MicroPython firmware for ESP32/Pico).
-   **Install Servo Library**: Most environments have a built-in or easy-to-install servo library. For Arduino, the `Servo.h` library is standard.

### 2. Connect the Microcontroller

-   Ensure your robot's servos are connected to the microcontroller as per your kit's instructions.
-   Connect the microcontroller to your computer using the USB cable.
-   Select the correct board and port in your IDE.

### 3. Control a Single Servo

Let's start by controlling one servo. Identify a servo connected to a specific digital pin (e.g., pin 9).

```cpp
// Arduino Example for a single servo
#include <Servo.h>

Servo myServo; // Create a servo object

void setup() {
  myServo.attach(9); // Attaches the servo on pin 9 to the servo object
  Serial.begin(9600); // Initialize serial communication for debugging
  Serial.println("Servo test started");
}

void loop() {
  // Move servo to 0 degrees
  myServo.write(0);
  Serial.println("Moving to 0 degrees");
  delay(1000); // Wait for 1 second

  // Move servo to 90 degrees
  myServo.write(90);
  Serial.println("Moving to 90 degrees");
  delay(1000); // Wait for 1 second

  // Move servo to 180 degrees
  myServo.write(180);
  Serial.println("Moving to 180 degrees");
  delay(1000); // Wait for 1 second
}
```

-   Upload this code to your microcontroller.
-   Observe the connected servo motor. It should move through 0, 90, and 180 degrees.

### 4. Make Your Robot Wave (Multiple Servos)

Now, let's use multiple servos to create a simple waving motion. You'll need to know which pins control the "shoulder" and "elbow" servos of one of your robot's arms. Let's assume pin 9 for shoulder and pin 10 for elbow.

```cpp
// Arduino Example for waving motion
#include <Servo.h>

Servo shoulderServo;
Servo elbowServo;

void setup() {
  shoulderServo.attach(9); // Attach shoulder servo to pin 9
  elbowServo.attach(10); // Attach elbow servo to pin 10

  // Set initial position (e.g., arm down)
  shoulderServo.write(90); // Mid-range
  elbowServo.write(90);    // Mid-range
  delay(1000);
}

void loop() {
  // Wave motion: Lift arm, bend elbow, straighten, lower arm
  
  // Lift arm up
  for (int pos = 90; pos >= 45; pos -= 1) { // Move from 90 to 45 degrees
    shoulderServo.write(pos);
    delay(15);
  }
  delay(500);

  // Bend elbow (waving action)
  for (int i = 0; i < 3; i++) { // Wave 3 times
    elbowServo.write(120); // Bend
    delay(300);
    elbowServo.write(60);  // Straighten
    delay(300);
  }
  delay(500);

  // Lower arm
  for (int pos = 45; pos <= 90; pos += 1) { // Move from 45 to 90 degrees
    shoulderServo.write(pos);
    delay(15);
  }
  delay(1000); // Pause before repeating
}
```

-   Modify the pin numbers and servo angles (`myServo.write(angle)`) to match your robot's configuration and desired motion.
-   Upload the code and watch your robot wave!

:::info Tip
Experiment with different `delay()` values to change the speed of movements, and different `myServo.write()` angles to adjust the range of motion.
:::

## How it Works: Servo Principles

-   **Pulse Width Modulation (PWM)**: Servo motors are controlled using PWM signals. The microcontroller sends a series of pulses, and the width of each pulse determines the angle the servo moves to. Typically, a pulse width between 1000 and 2000 microseconds corresponds to a range of 0 to 180 degrees.
-   **Servo Libraries**: These libraries simplify servo control by abstracting away the low-level PWM details, allowing you to simply specify an angle (e.g., `myServo.write(90)`).
-   **Range of Motion**: Most standard hobby servos have a 180-degree range. Some continuous rotation servos exist, but for precise joint control, position-limited servos are used.

## Challenge (Optional)

-   Can you make your robot perform a different simple gesture, like a bow or a salute?
-   Try to incorporate a button: when the button is pressed, the robot waves; otherwise, it stays still.

## Conclusion & Next Steps

You've successfully programmed your robot to perform its first movements! You now understand the basics of controlling servo motors and orchestrating simple actions. This is a crucial step towards creating more complex and intelligent behaviors. In the next lesson, we'll delve into the theory of walking gaits and attempt to make your robot take its first steps!
