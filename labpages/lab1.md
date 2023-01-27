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

This program blinks the built-in LED by writing the value High, delaying for a second, writing Low, delaying for a second, and looping forever. As a result, the blue built-in LED can be seen to turn off and on every second.

### Serial

This program combines Serial.write and Serial.read capabilities. The user can enter a message into the top bar of the serial output, and this message is then printed to the serial monitor.

### Analog Read

The Artemis Nano includes an onboard ADC that reads analog voltage on the ADCPIN (external), raw analog temperature (temp), VCC across a 1/3 voltage divider (vcc/3), and a value vss that is ideally 0. I tested the functionality by holding my hand on the Artemis board to increase the temperature reading. Tture reading gradually increased from around 33000 to 34000.

### Microphone Output

This section tested the functionality of Pulse Density Microphone (PDM). I tested a range of frequencies, playing YouTube videos of 500Hz, 1000Hz, and 1500Hz. Using FFT computation, the calculated maximum frequencies were 503Hz, 1007Hz, and 1499Hz, respectively. While these frequencies were not being played, a frequency of around 16000Hz is detected in the room, background noise potentially caused by the surrounding walls and devices.

[Back to Homepage](../)
