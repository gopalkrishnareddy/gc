Project Overview
================
The project consists of building a device to monitor and log night-time bruxism as well as associated sleep data. More background here: https://github.com/lucwastiaux/gc/edit/master/README.md

Diagrams
========
How the device will be worn on the head. A couple of notes:
* The PCB will be enclosed in a custom case and placed inside a sleeve which will be stiched to the headband.
* The left and right side of the PCB will be accessible, as well as the center bottom, to plug-in the cable going to the EMG/muscle sensor.
![Head Diagram](https://raw.githubusercontent.com/lucwastiaux/gc/dev/gc2_specs/head_diagram.jpg)

What the PCB should look like:
* I am not yet 100% set on which side the connectors will need to be on, I need to experiment with placement.
![PCB Diagram](https://raw.githubusercontent.com/lucwastiaux/gc/dev/gc2_specs/pcb_diagram.jpg)

Board Components
================
* Particle Photon board https://www.particle.io/. There seem to be two options, either include the SMT (headerless) version of the Photon dev board, or use the P1 chip, which requires a voltage regulator, some buttons and LEDs. 
* All components of this battery shield: https://www.sparkfun.com/products/13626. 
  * I don't need the bottom pads for the barrel connector.
  * I don't need the Alert Interrupt Jumper (https://learn.sparkfun.com/tutorials/photon-battery-shield-hookup-guide?_ga=1.30882105.781200154.1443956391) 
  * I am not clear in what position the I2C pull up jumper needs to be (will try to clarify)
  * If you are using the Photon P1 chip, then we need an additional micro-USB port for charging.
* All components of this IMU shield: https://www.sparkfun.com/products/13629
* A 3-pole connector for connecting to the EMG sensor https://www.kickstarter.com/projects/312488939/myowaretm-harness-the-power-of-your-muscle-signals
  * The 3 poles are Ground, +3.3V regulated, and signal from the EMG
  * The signal from the EMG will be read by an analog input pin on the Photon using analogRead()
* A switch to close/open the battery circuit and turn the device off.
* A side-mounted 2-position switch which sets one of the digital input pins on the Photon to either high or low
  * This will be used to configure an "offline mode" in the software as the Photon expects full time internet connectivity by default
  * The value of the switch will be read using digitalRead()
* 2 side-mounted push-buttons (not sure i'm using the right word) which will be connected to 2 respective digital pins on the Photon.
  * These will be used to interact with the software.
  * The wiring will be similar to this https://www.arduino.cc/en/Tutorial/Button
  * The value of the switch will be read using digitalRead()
* An mono audio circuit with a 3.5mm jack
  * This will be used to output audio tones using the tone() function. The quality of the audio output is not important, it'll just be used to wake the user up.
* A piezo buzzer. This will be used to acknowledge button presses when the user is not wearing headphones. Having the audio feedback is important because the device will be worn on the side of the head, and used in the dark (night time), so the only form of feedback that would work is audio.
  * I would like the tone volume to be software-configurable. Some of the simpler circuits here look like they should work: https://www.maximintegrated.com/en/app-notes/index.mvp/id/1828
  * The board should have small mounting holes on each corner 
  
Proposed Pin Layout
===================
* D0 and D1 are reserved for the I2C bus
* A0: EMG signal
* D2: push button 1 (used to interact with software on photon)
* D3: push button 2 (used to interact with software on photon)
* D4: 2-position switch (used to interact with software on photon)
* D5: for MAX5160 INC pin
* D6: for MAX5160 U/D pin
* D7: headphone jack insertion detection
* A1: audio output
* A2: audio amplifier shutdown pin
* A4: piezo buzzer

Connector Placement Constraints
===============================
* EMG connector must be on the bottom (facing down, but can be off to the left / off to the right / centered)
* 3.5mm audio jack must be on the left
* 2 side mounted push buttons must be on the right, side by side
* battery JST connector must be on the right (the battery will either be mounted under the PCB, or "forward" of the PCB, more towards the forehead of the user. I haven't decided yet)
* side-mounted on/off slide switch can be anywhere (left,right,top,bottom)
* side-mounted offline mode slide switch can be anywhere (left,right,top,bottom)
* micro USB port for charging can be anywhere (left,right,top,bottom)

Current State of Prototyping
============================
At this stage the prototype only exists in my head, I have not started putting anything on the breadboard yet, and i'm still waiting for my Photon boards. For example, I don't know what pins I will connect the EMG, offline switch and 2 pushbuttons to. The exact pin numbers will depend on what constraints that exist on analog/digital input on the Photon.

However, the schematics of (Photon + LIPO charging/gauge circuit + IMU circuit) are already set in stone as they are a simple replica of the Sparkfun shields. So you could start by putting together those schematics.
