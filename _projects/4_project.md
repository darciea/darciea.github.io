---
layout: page
title: Autonomous Mine Navigating Robot
description: Programming a robot to navigate a maze using the PIC18F microcontroller.
img: assets/img/nicemaze.jpg
importance: 3
category: previous
---

<div class="text-center mb-4">
    <div class="col-sm mt-0 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/mazegif.gif" title="Autonomous Robot Navigating Maze" class="img-fluid rounded z-depth-1 w-50" %}
    </div>
</div>

#### **Scenario:**
Operations are underway to map an abandoned mine for safety and possible future use. A team of workers has entered the mine as part of initial exploration, but one member of the team became separated and is currently missing. All explorers were instructed to place flags at specific intervals along their paths inside the mine. It is too dangerous to send another person to search the area where the explorer went missing, and the mine's communications are too unstable for remote-controlled robots. 

#### **Task:**
Design a control system for an autonomous robot to locate the flags laid by the explorer and determine their location. The robot must then return to its starting point, leaving behind a trace of its route so that a larger robot, or even a manned team, can locate and extract the explorer. The robot must be able to:

1. Navigate towards a colored card and stop before impacting it.
2. Read the card’s color.
3. Interpret the card color using a predefined code and execute the navigation command.
4. Upon reaching the final card, return to the starting point.
5. Handle exceptions and navigate back if the final card is not found.

---

### **Our Solution**

<div class="container" style="max-width: 80%; margin: 0 auto;">
  <div class="row">
    <!-- First image (2/3 of the width) -->
    <div class="col-md-7 mt-3 mt-md-0 text-center">
      {% include figure.liquid loading="eager" path="assets/img/buggy.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>

    <!-- Second image (1/3 of the width) -->
    <div class="col-md-4 mt-3 mt-md-0 text-center">
      {% include figure.liquid loading="eager" path="assets/img/maze.png" title="example image" class="img-fluid rounded z-depth-1 w-100" %}
    </div>
  </div>
  <div class="caption text-center mt-2"> PIC18F Buggy navigating the hard maze. </div>
</div>

To start the robot within the maze, press the RF2 button when the robot is in the correct position. Once the button is pressed, the robot will move forward, recording the time taken and continuously reading the clear sensor. When the sensor reading exceeds a specific threshold, the robot enters the card reading sequence. The robot records the time to reach the card, reads the color of the card in front of it, and responds accordingly. Each card's color is stored in an array, and the robot repeats this process until it reads the white card. At this point, the robot enters the *ReturnHome* sequence, reversing its course by following the recorded times and executing the opposite commands for each card.

---

### **Color Detection and Response Methodology**

The robot is initialized with a calibration routine to populate a 4x9 array with the expected readings for each color sensor (RGBC) corresponding to each colored card. After a button press, the robot collects three readings from each sensor, calculating the average for each. The calibration sequence follows this order: red, green, blue, yellow, pink, orange, light blue, white, and black. The RF2 button triggers the reading of each card.

Once calibration is complete, the robot continuously monitors the clear sensor, and when its reading exceeds a predetermined threshold, the color detection sequence is activated. The robot compares the new readings to the expected values in the array. The card with the closest match is identified, and the corresponding action is performed.

---

### **Returning Home Methodology**

Two arrays are introduced in the main function: `ReturnHomeTimes` and `ReturnHomeCards`. The `ReturnHomeTimes` array stores the time taken to reach each card, while `ReturnHomeCards` stores the corresponding cards. A timer interrupt overflows every 1/10th of a second, incrementing the `timerCount` each time the interrupt occurs. The robot counts the time it moves forward until a card is detected and responds to the color. As the robot navigates, the arrays are populated with the time and card information.

Upon detecting the white card, the *ReturnHome* sequence is triggered. The robot turns around 180 degrees and iterates through the arrays in reverse order, moving forward for the time stored in the corresponding `ReturnHomeTimes` array. The robot then executes the opposite navigation commands based on the `ReturnHomeCards` array. This process continues until the robot reaches the start.

Note: Each entry in `ReturnHomeTimes` corresponds to the same index in `ReturnHomeCards`, ensuring that the robot performs the correct reverse actions.

---

### **Videos**

- [Buggy Running the Test Maze](https://youtu.be/ieVXnOMHYYI)
- [Buggy Running the Easy Maze](https://youtube.com/shorts/kAJKZJEhZO8?feature=share)
- [Buggy Running the Hard Maze](https://youtu.be/YRGQFnze7Yo)

