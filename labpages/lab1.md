---
layout: default
---

# Lab 1: Artemis

## The Artemis Board

In this lab, I setup the Arduino IDE and the SparkFun Redboard Artemis Nano. Tasks included using the board LED, reading/writing serial messages over USB, and using the onboard temperature sensor and Pulse Density Microphone.

All code was from the Examples section in the Arduino IDE and tested some basic functions of the RedBoard Artemis Nano mentioned above.

Below is a video of the functions:

<iframe width="560" height="315" src="https://www.youtube.com/embed/FYA2UyBvi20" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


### Blink

This program blinks the built-in LED by writing the value High, delaying for a second, writing Low, delaying for a second, and looping forever.

### Serial

This program combines Serial.write and Serial.read capabilities. The user can enter a message into the top bar of the serial output, and this message is then printed to the screen.

### Analog Read

The Artemis Nano includes an onboard ADC that reads analog voltage on the ADCPIN (external), raw analog temperature (temp), VCC across a 1/3 voltage divider (vcc/3), and a value vss that is ideally 0.

### Microphone Output



[Back to Homepage](../)
