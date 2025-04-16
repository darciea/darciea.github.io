---
layout: page
title: Energy Saving Automatic Streetlights
description: Implementing a working microprocessor based system to simulate automated streetlights.
img: assets/img/streetlight.jpg
importance: 3
category: previous
---
<div class="container" style="max-width: 100%; margin: 0 auto; margin-bottom: 2rem">
  <div class="row justify-content-center align-items-center">
    <!-- First image (2/3 of the width) -->
    <div class="col-md-6 mt-2 mt-md-0 text-center">
      {% include figure.liquid loading="eager" path="assets/img/streetlight.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <!-- Second image (1/3 of the width) -->
    <div class="col-md-3 mt-2 mt-md-0 text-center">
      {% include figure.liquid loading="eager" path="assets/img/light.png" title="example image" class="img-fluid rounded z-depth-1 w-80" %}
    </div>
  </div>
</div>

#### **Scenario:**
Outside lights that respond to ambient light levels are commonplace (i.e. street lights, porch lights, garden lights etc). These types of lights switch on at dusk and then turn off at dawn. However, energy and money can be saved if these lights are switched off during the small hours of the morning (for example, between 1am and 5am), when there are very few people around. [Many councils in the UK have trialled this idea for street lights.](https://www.bbc.co.uk/news/uk-england-derbyshire-16811386)

#### **Task:**
The challenge is to design and program a device that fulfills the following requirements:

1. Monitors ambient light levels using a Light Dependent Resistor (LDR) and turns on an LED in low-light conditions (i.e., at night) and off in bright conditions (i.e., during the day).
2. Displays the current hour of the day on an LED array in binary.
3. Automatically turns off the light between approximately 1 am and 5 am.
4. Adjusts for daylight savings time.
5. Maintains synchronization with the sun indefinitely, accounting for changes throughout the year.
6. Operates completely automatically, requiring no maintenance after installation.

---
#### **Our Solution**

Our solution relies on the predictable nature of the sun's rise and set times, ensuring that it rises and sets exactly once per day. The program is designed to account for the fact that it is dark at midnight, and sunset occurs before midnight. However, issues may arise if the system's timer is more than two hours out of sync with the solar clock, such as when entering or exiting Daylight Saving Time (DST).

[Watch a demonstration here](https://www.youtube.com/watch?v=prrxO2kyVkE)

#### **Initialization Process:**
To correctly initialize the program, the following parameters must be manually set in the `main.c` file before the system begins:

- Day of the week (0 = Sunday, 6 = Saturday)
- Day of the month
- Month
- Year
- DST status (whether in Daylight Saving Time or not)

Additionally, the hour and minute must be set in the `interrupts.h` file for proper synchronization.
