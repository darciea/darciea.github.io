---
layout: page
title: Energy Saving Automatic Streetlights
description: Implementing a working microprocessor based system to simulate automated streetlights.
img: assets/img/streetlight.jpg
importance: 3
category: previous
---

## Learning outcomes

The principal learning objectives for this project are:

- Implement a working microprocessor based system to achieve a more complex real world task
- Develop ability to independently plan, organise and structure your code
- Improve grasp of the C language and writing your own functions

## Brief

Outside lights that respond to ambient light levels are commonplace (i.e. street lights, porch lights, garden lights etc). These types of lights switch on at dusk and then turn off at dawn. However, energy and money can be saved if these lights are switched off during the small hours of the morning (for example, between 1am and 5am), when there are very few people around. Many councils in the UK have implemented/trialled this idea for street lights (https://www.bbc.co.uk/news/uk-england-derbyshire-16811386). Your task is to use the knowledge of microcontrollers and hardware that you have gained in labs 1-3 from this module to develop a fully automated solution.

## Specification

Design and program a device that meets the following requirements:

1. Monitors light level with the LDR and turns on an LED in low light conditions (i.e. night-time) and off in bright conditions (i.e. daytime)
1. Displays the current hour of day on the LED array in binary
1. Turns the light off between approx. 1am and 5am
1. Adjusts for daylight savings time
1. Maintain synchronicity with the sun indefinitely
1. Be fully automatic (requires zero maintenance after installation)

## Our solution

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/prrxO2kyVkE/0.jpg)](https://www.youtube.com/watch?v=prrxO2kyVkE)

This program relies on the fact that the sun rises and sets exactly once a day (ie a major eclipse may cause problems), and that it is dark at midnight (ie sunset occurs before midnight). This program should be initiated before the sun rises on the day to avoid difficulties. Potential issues may also arise if the timer is 2 hours or more out of sync with the solar clock on the day when the clocks are changing due to entering or exiting DST.

To correctly start the program, you must first manually initialise the day (0 = Sunday, 6 = Saturday), the day of the month, the month and the year, and whether we are in DST or not in the main.c file, and the hour and minute should be set in the interrupts.h file.
