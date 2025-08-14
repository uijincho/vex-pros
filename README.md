# Introduction to VEX Robotics Programming with PROS

## About

Welcome to the VEX Robotics curriculum designed to teach students how to program the VEX V5 system using [PROS (Purdue Robotics Operating System)](https://pros.cs.purdue.edu/). This project provides a modular, beginner-friendly path to learning robotics programming in C++ with hands-on examples. This curriculum works best when worked on with a [VEX V5 Clawbot](https://link.vex.com/docs/v5-clawbot-legacy-build-instructions).

### Potential Alternative Pathways

- **VSC or PROS not installed**: Start at Module 0 (Environment set up)
- **Prior programming experience**: Start at Module 2 (Project set up)
- **Prior controller-only/VEXcode blocks or text experience** - Start at Module 4 (Autonomous routines)
- **Prior PROS experience**: Start at Module 5 (Competition setup)

## Curriculum Overview

| **Module**: |  |
| --- | --- |
| 0 | [Setting up Visual Studio Code & PROS](#module-0-setting-up-visual-studio-code--pros) |
| 1 | [Intro to Programming & C++](#module-1-intro-to-programming--c) |
| 2 | [Setting up a Project & Motors in PROS](#module-2-setting-up-a-project--motors-in-pros) |
| 3 | [Tank Drive & Arm/Claw Control for the Clawbot](#module-3-tank-drive--armclaw-control-for-the-clawbot) |
| 4 | [Creating Autonomous Routines](#module-4-creating-autonomous-routines) |
| 5 | [Using Sensors & Competition Preparation](#module-5-using-sensors--competition-preparation) |

## Content

### Module 0: Setting up Visual Studio Code & PROS

### Module 1: Intro to Programming & C++

#### Data Types & Variables

When writing code for robots, it is important to have a way to store and use information for things like motor speeds, sensor readings, and button presses.

In C++, the programming language commonly used in VEX Robotics, this is done using **variables**. A variable is a labeled container where you can store a piece of data to use later.

| Data Type | Example                             | What It Stores                                 | Example Usage                |
| --------- | ----------------------------------- | ---------------------------------------------- | ---------------------------- |
| `int`     | `int motorSpeed = 100;`             | Whole numbers (positive, negative, or zero)    | Motor speed, joystick values |
| `bool`    | `bool clawOpen = true;`             | `true` or `false`                              | Is the claw open?            |
| `double`  | `double wheelCircumference = 25.4;` | Decimal numbers with high precision            | Distance traveled in cm      |
| `float`   | `float armAngle = 90.5;`            | Decimal numbers (less precision than `double`) | Arm angle in degrees         |

To define and initialize variables with a value, you need:

1. **a data type** - what kind of data it stores
2. **a name** - so you can call it later
3. **a value** - to be used later

Example:
```cpp
int motorSpeed = 100;   // Create a variable and give it the value 100
motorSpeed = 50;        // Change the value to 50
```

In PROS, motors need a port value to be created. Because these values stay constant with each program, a C++ concept called a macro is created to store the number. 

```cpp
#define ARM_PORT 8
```

#### Conditional Statements

Robots need to make decisions; for example, deciding whether to open or close the claw or to move forward or stop. 

In C++, **conditional statements** help run different code depending on whether certain conditions are **true** or **false**.

##### `if` Statement

Runs a block of code **only if** a condition is true.

**Format:**

```cpp
if (condition) {
  // Code runs if condition is true
}
```

**Example:**

```cpp
if (buttonPressed) {
  Claw.move_velocity(100); // Open claw
}
```
If `buttonPressed` is `true`, then the claw will open.

##### `else if` Statement

Adds another condition to check **if the first one was false.**

**Format:**

```cpp
if (condition1) {
  // Code runs if condition1 is true
}
else if (condition2) {
  // Runs if condition2 is true AND condition1 was false
}
```

**Example:**

```cpp
if (buttonOpen) {
  Claw.move_velocity(100); // Open claw
}
else if (buttonClose) {
  Claw.move_velocity(-100); // Close claw
}
```
If `buttonOpen` is `true`, then the claw will open. But if that was not true **and** buttonClose is true, then the claw will close.

##### `else` Statement

Runs a block of code if **none of the previous conditions** were true.

**Format:**

```cpp
if (condition1) {
  // ...
}
else if (condition2) {
  // ...
}
else {
  // Runs if all above are false
}
```

**Example:**

```cpp
if (buttonOpen) {
  Claw.move_velocity(100); // Open claw
}
else if (buttonClose) {
  Claw.move_velocity(-100); // Close claw
}
else {
   Claw.move_velocity(0); // Stop claw
}
```
If `buttonOpen` is `true`, then the claw will open. But if that was not true **and** buttonClose is true, then the claw will close. If **none** of those conditions are true, the claw will not move.

> It can be helpful to use a **flowchart** to plan out the logic of your program before you write the code.

> You can use `if`, multiple `else if`s, and `else` together or just `if` and `else`. Typically, when you use an `if`, you will need to use an `else` statement as well.

#### Operators

It is also important to **perform calculations** or **make decisions** based on certain conditions. In C++, this is done with **operators**, symbols that tell the program what action to perform.

| Arithmetic Operator | Example             | Meaning             | Example Usage                    |
| -------- | ------------------- | ------------------- | -------------------------------- |
| `+`      | `speed + 10`        | Addition            | Increase motor speed             |
| `-`      | `speed - 5`         | Subtraction         | Decrease arm position            |
| `*`      | `wheelDiameter * 3` | Multiplication      | Calculate total distance         |
| `/`      | `distance / time`   | Division            | Calculate average speed          |
| `%`      | `count % 2`         | Modulus (remainder) | Check if a number is even or odd |

Example:
```cpp
int leftSpeed = 50;
int rightSpeed = leftSpeed + 10; // rightSpeed is now 60
```

Logical operators are used to combine or modify **true/false** (`bool`) values. These are useful for checking multiple conditions at once.

<table>
  <thead>
    <tr>
      <th>Logical Operator</th>
      <th>Example</th>
      <th>Meaning</th>
      <th>Example Usage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>&amp;&amp;</code></td>
      <td><code>(buttonA &amp;&amp; buttonB)</code></td>
      <td>AND — both must be true</td>
      <td>Only move claw if both buttons are pressed</td>
    </tr>
    <tr>
      <td><code>||</code></td>
      <td><code>(buttonA || buttonB)</code></td>
      <td>OR — one must be true</td>
      <td>Move claw if either button is pressed</td>
    </tr>
    <tr>
      <td><code>!</code></td>
      <td><code>!clawOpen</code></td>
      <td>NOT — reverse the value</td>
      <td>Run code if claw is <strong>not</strong> open</td>
    </tr>
  </tbody>
</table>

Example:
```cpp
bool armUp = true;
bool clawOpen = false;

if (armUp && !clawOpen) {
    // Arm is up AND claw is closed
}
```

Relational operators compare two values and return `true` or `false`.

| Relational Operator | Example       | Meaning      | Example Usage                           |
| -------- | ------------- | ------------ | --------------------------------------- |
| `<`      | `speed < 100` | Less than    | Check if speed is below a limit         |
| `>`      | `speed > 0`   | Greater than | Check if robot is moving forward        |
| `==`     | `count == 5`  | Equal to     | Check if a counter has reached a target |
| `!=`     | `mode != 1`   | Not equal to | Check if the mode is not 1              |

> `==` is to check if two values are equal. `=` is for assigning a value to something.

Example: 
```cpp 
int speed = 80;

if (speed < 100) {
    // Increase speed
}
```

#### Loops

A `while` loop repeats as long as a certain condition is `true`.

**Format:**
```cpp
while (condtion) {
  // code that repeats while a condition is true
}
```

**Example:**
```cpp
int count = 0 {

while (count < 5) {
  count = count + 1;
}
```

This loop will repeat until the `count` variable reaches 5.

Sometimes in robotics, a `while(true)` loop will be used, creating an infinite loop which never ends until the program is stopped or `break` is used. This is common in **robot operator control mode**, because the robot needs to keep responding to the controller until the match ends.

**Example in PROS:**

```cpp
while(true) {
  // Check controller input
  // Move motors
  pros::delay(20); // Prevent CPU overload
}
```

Here, the robot keeps running the code inside the loop forever during driver control.

A `for` loop is used when y ou know exactly how many times you want to repeat something. 

It is often used for counting or going through a sequence of numbers.

**Format:**
```cpp
for (start; condition; update) {
  // Code that repeats
}
```

**Example:**
```cpp
for (int i = 0; i < 5; i++) {
  // Run 5 times, i goes from 0 until it isn't less than 5 (4)
}
```

##### Key Differences
| Feature          | `while` Loop                            | `for` Loop                                              |
| ---------------- | --------------------------------------- | ------------------------------------------------------- |
| Best for         | Repeating until a condition changes     | Repeating a set number of times                         |
| Loop setup style | Condition only                          | Start, condition, and update in one line                |
| Common in PROS   | `while(true)` for continuous robot code | Rare in main control loop, but useful for timed actions |


### Functions

Functions let you put actions that you would use repeatedly (like setting the claw speed, or driving forwards or backwards) into named blocks of code.

#### What is a function?

A function has: 

- **Return Type** (what it gives back; `void` if nothing)
- **Name**
- **Parameters** (inputs)
- **Body** (the code it runs)

#### Format:

```cpp
return_type functionName(parameterType1 param1, parameterType2 param2){
//do something here 
return value;
}
```

#### Example without return:

```cpp
void setClawSpeed(int rpm) {
  Claw.move_velocity(rpm);
}
```

#### Example with return:

```cpp
double average(double a, double b) {
  return (a + b) / 2.0;
}

```

#### Why would we use functions in robotics?

- **Reuse:** Call the same behavior between driver control and autonomous.
- **Clarity:** Give names to actions (e.g. `openClaw()`, `driveStraight()`).
- Testing: You can test small pieces independently.

#### Parameters & Return Types

- **Parameters** are inputs your function needs
- **Return type** is the kind of value the function gives back

```cpp
// Input joystick value, output scaled motor speed
int scaleSpeed(int stick) {
  return stick * 2; // example scaling
}
```

If your function doesn’t need to return anything, use `void`:

```cpp
void stopDrive() {
  LeftDrive.move_velocity(0);
  RightDrive.move_velocity(0);
}

```

#### Pass‑by‑Value vs Pass‑by‑Reference (*advanced*)

By default, parameters are **copied** (pass‑by‑value). For large data or when you want to **modify** the caller’s variable, use a **reference** (`&`).

```cpp
// Pass-by-value (copy):
void setTarget(int target) { /* uses a copy */ }

// Pass-by-reference (can modify original):
void zeroIfSmall(int &value) {
  if (value < 10) value = 0; // changes caller's variable
}
```

Use `const &` when you won’t modify the input but want to avoid copies:

```cpp
void printName(const std::string &name) {
  // name is read-only here
}
```

#### Function Declarations (Prototypes)

If you call a function **before** it’s defined, you need a **prototype** at the top of the file (or in a header).
... (135 lines left)

### Module 2: Setting up a Project & Motors in PROS

### Module 3: Tank Drive & Arm/Claw Control for the Clawbot

### Module 4: Creating Autonomous Routines

### Module 5: Using Sensors & Competition Preparation

## License

[MIT License](LICENSE)

## Team

Created by [Uijin Cho](https://github.com/uijincho), [Dhruv Patel](https://github.com/Dhruv23) 

Suggestions? Create an [issue](https://github.com/uijincho/vex-pros/issues)

Created for [Robolabs | Dublin Robotics Club](https://www.robolabs.org/)
