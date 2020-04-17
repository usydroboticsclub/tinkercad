# TinkerCAD Workshop- 1

## Plan
1. Setting up an account
2. Basic Navigation of the GUI
3. Blinking an LED
4. Fading an LED
5. Using Push Buttons:
6. Your Turn: Create a circuit of an array of LEDs that fade after each other, but blink if a button is pressed
7. Connecting to an RGB LED
8. Connecting a Potentiometer
9. Your Turn: Create a light control by the reading from a potentiometer

## Setting Up an Account
- Log in using Autodesk Account or Google
- Should be free
## Basic Navigation
- When you log in, you’ll be in your main Dashboard. Click on the Circuits tab and “Create new Circuit”.
- You’ll have your workspace in the centre of the screen. On the right hand side, you can find the component selection list. Simply click and drag a component on the workspace to use it. 
- In the top right are two buttons, Code and Start Simulation. The Code button will give you the ability to write code for your Arduino or other programmable elements in the workspace. 
- The Start Simulation button will run any code and circuitry you have designed.
## Blinking an LED
For this tutorial, you’ll need-
- 1x Arduino
- 1x Breadboard
- 1x Resistor
- 1x LED
### Setup-
1. Connect a resistor to pin 13
2. Connect the resistor anode (positive end) of an LED
3. Connect the LED cathode (negative end) to GND

![The setup for blinking a LED](https://github.com/usydroboticsclub/tinkercad/raw/master/blinkingled.png "The setup for blinking a LED")


### Code-
```c
void setup()
{
  pinMode(13, OUTPUT);
}
void loop()
{
  // turn the LED on (HIGH is the voltage level)
  digitalWrite(13, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  // turn the LED off by making the voltage LOW
  digitalWrite(13, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
}
```
## Fading an LED-
For this tutorial, you’ll need-
- 1x Arduino
- 1x Breadboard
- 1x Resistor
- 1x LED
### Setup-
1. Connect the resistor to pin 9
    - Note that it has a ~ in front of it
    - This denotes it as being able to produce a PWM (Pulse Width Modulation) output
2. Connect the other end of the resistor to the anode (positive end) of the LED
3. Connect the cathode (negative end) to GND

![The setup for fading a LED](https://github.com/usydroboticsclub/tinkercad/raw/master/fadingled.png "The setup for fading a LED")

### Code-
```c
int brightness = 0;
void setup()
{
  pinMode(9, OUTPUT);
}
void loop()
{
  for (brightness = 0; brightness <= 255; brightness += 5) {
    analogWrite(9, brightness);
    delay(30); // Wait for 30 millisecond(s)
  }
  for (brightness = 255; brightness >= 0; brightness -= 5) {
    analogWrite(9, brightness);
    delay(30); // Wait for 30 millisecond(s)
  }
}
```
## Using Push Buttons-
For this tutorial, you’ll need-
- 1x Arduino
- 1x Breadboard
- 2x Resistor
- 1x LED
- 1x Push button
### Setup-
1. Place the push button along the middle strip of the breadboard
    - This ensures that a signal can be sent along the whole length of the breadboard
2. Connect one of the terminals to pin 2
3. At the same terminal, connect a resistor to GND
    - This is known as a pull down resistor
    - It gives the Arduino pin a weak connection to GND to ensure that the pin is not floating 
    - Floating pins in physical circuits can be affected by static or other interference, which could negatively affect circuits
4. On the terminal diagonal to the previous terminal, connect it to HIGH
5. Connect the anode of an LED to pin 13
6. Connect the cathode to GND

![The setup for a push button](https://github.com/usydroboticsclub/tinkercad/raw/master/pushbutton.png "The setup for a push button")

### Code-
```c
int buttonState = 0;
void setup()
{
  pinMode(2, INPUT);
  pinMode(13, OUTPUT);
}
void loop()
{
  // read the state of the pushbutton value
  buttonState = digitalRead(2);
  // check if pushbutton is pressed.  if it is, the
  // buttonState is HIGH
  if (buttonState == HIGH) {
    // turn LED on
    digitalWrite(13, HIGH);
  } else {
    // turn LED off
    digitalWrite(13, LOW);
  }
  delay(10); // Delay a little bit to improve simulation performance
}
```
## Your Turn: 
Alright now that the basics are out of the way, your task is to design a circuit that when activated will blink an LED light. But when you press a push button, the LED will fade periodically. Feel free to ask the exec for help. 

## Connecting to an RGB LED-
### Components-
- 1x Arduino
- 1x Breadboard
- 3x Resistors
- 1x RGB LED
## Setup-
1. Connect resistors to the RED, BLUE and GREEN terminals for the LED
    - From the left, they’ll be the 1st, 3rd and 4th
2. Connect each resistor to pins 11, 10 and 9 respectively
3. Connect the cathode of the RGB LED to GND

![The setup for the RGB LED](https://github.com/usydroboticsclub/tinkercad/raw/master/rgbled.png "The setup for the RGB LED")


### Code-
```c
void setup()
{
  pinMode(11, OUTPUT);
  pinMode(10, OUTPUT);
  pinMode(9, OUTPUT);
}
void loop()
{
  analogWrite(11, 255);
  analogWrite(10, 0);
  analogWrite(9, 0);
  delay(1000); // Wait for 1000 millisecond(s)
  analogWrite(11, 255);
  analogWrite(10, 0);
  analogWrite(9, 255);
  delay(1000); // Wait for 1000 millisecond(s)
}
```

## Connecting to a potentiometer-
### Components-
- 1x Arduino
- 1x Breadboard
- 1x Potentiometer
- 1x Resistor
- 1x LED
### Setup-
1. Connect the middle pin of the potentiometer to A0
2. Connect the two outer pins to GND and power 
3. Connect a resistor to pin 13
4. Connect the resistor to the anode of an LED
5. Connect the cathode to GND

![The setup for a potentiometer](https://github.com/usydroboticsclub/tinkercad/raw/master/potentiometer.png "The setup for a potentiometer")

### Code-
```c
int sensorValue = 0;
void setup()
{
  pinMode(A0, INPUT);
  pinMode(13, OUTPUT);
}
void loop()
{
  // read the value from the sensor
  sensorValue = analogRead(A0);
 // turn the LED on
  digitalWrite(13, HIGH);
  // pause the program for <sensorValue> millseconds
  delay(sensorValue); // Wait for sensorValue millisecond(s)
  // turn the LED off
  digitalWrite(13, LOW);
  // pause the program for <sensorValue> millseconds
  delay(sensorValue); // Wait for sensorValue millisecond(s)
}
```

## Your Turn:
Create a circuit that has an RGB LED output RED when a potentiometer has a reading between 0-85, output BLUE when it has a reading between 86-170 and GREEN when it it has a reading of 171-255. 
