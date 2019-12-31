 ![Alt text](https://raw.githubusercontent.com/littletwany/PICTURE/master/img/pic.png)
 - Sensors: Temperature and Humidity Sensors, Triaxial Accelerometers, Hall Sensors, Light Sensors, Sound Sensors
 - Output module: OLED display, LED lamp, Buzzer
 - Input module: knob, Button

# learning objectives 
- Learn the basics of open source hardware systems.
- Learn basic Arduino software programming methods.
- Learn the basic communication principles and methods of sensor modules.
- Hands-on implementation of basic open source hardware projects.
# Course outline:
## Section 0:  Unlock Your First Open Source Hardware
### 1.Perception of the world: light, sound, interaction, perception, movement, environment.
*Note: once the board is powered on, it is a display of intelligent indoor environmental data detection.*
 - First of all, let's get to know this kit, use USB cable to power the board, we will see the LED screen lit up, the center of the screen will appear a little boy, he is with us to learn the kit partner, call him little seeed.The top left corner of the screen shows the temperature, humidity and light in our current environment, and you can see that little seeed is happy.
 - Ok, now we'll take the kit to a very hot place, where little seeed will be hot and his head will sweat. Then we can choose a place where the temperature is lower, or we can cool the temperature and humidity sensor, or we can take it to the refrigerator, and we can see the little seeed has a cold and falls to the ground. If the ambient light is dim, the LED lights will light up; If you shout at the little seeed, the sound sensor responds, and the little silicon covers its ears because the noise is so loud.
 - Now that you've unlocked all of little seeed's poses, let's see if there are any more cool moves.Take our kit with both hands and tilt it horizontally down to the left or down to the right, and you'll see the little seeed moving in the same direction, thanks to the triaxial accelerometer, which, of course, doesn't go off the screen.If you want to control it more accurately yourself, you can use knobs and buttons to make it move from side to side or jump up.This does not look risky enough. A magnet placed near the hall sensor would drop a large rock from the sky, blocking the movement of the little seeed, and the buzzer would sound an alarm.
 - Above is the first demonstration of the functions of the whole suite. Next, we will learn the basic programming methods of Arduino software and understand the basic communication principles and methods of sensor modules.Realize all kinds of functions by yourself, experience the happiness of creation!
## Section 1: What Is Arduino? 
### 1. The birth of Arduino?
 - Arduino is a kind of convenient, flexible and easy-to-use open source electronic platform, including hardware (Arduino board of various models) and software (arduinoIED). It was designed by Italian teacher Massimo Banzi and Spain traditional engineer David Cuartielles, it solved the problem of the students can't find cheap microprocessors. Massimo Banzi liked to go to a bar called "di Re Arduino", this is according to the Italian king named after about one thousand years ago, to mark the place, they put the circuit board named the Arduino.
 - It is not only suitable for rapid prototyping by engineers, but also for artists, designers, hobbyists and friends who are interested in interaction, and it is almost a must-have tool for modern makers.
### 2. Introduction to seeeduino and & Difference with Arduino
 - Seeeduino is an arduino-compatible board, designed and manufactured by Seeed Studio in shenzhen, China, is fully compatible with Arduino software, shields and IEDs.
 - Based on an early Arduino design from Diecimila, it is available in two models with ATmega168 and ATmega328 microprocessors, compatible with the pin layout and dimensions of Diecimila.Improvements have been made in both auto-sensing USB and external power supply, as well as better power supply circuits on board, significantly improving flexibility and user experience.
### 3. How to get started with the Arduino IDE?
 - Install the Arduino IDE
   - Arduino IDE is an integrated development environment for Arduino, which is used for single-chip microcomputer software programming, downloading, testing and so on.
   - Start with the  [Arduino website](http://www.arduino.org/software) (http://www.arduino.org/software) Download Arduino IED.
 - Install the USB driver
    - Arduino connects to the PC via a USB cable.The USB driver depends on the type of USB chip you're using on your Arduino.USB chips are usually printed on the back of the development board.
    - For the official version of Arduino Nano, the USB chip model on the board is FT232RL, the download link of the driver is as follows: http://www.ftdichip.com/Drivers/VCP.htm.
    - After the driver installation is completed, connect Arduino to the USB port of PC with USB cable, you can see it in " my computer - properties - hardware - device management ". please note its serial port number.
    - If the driver is not installed, or if the driver is installed incorrectly (not matching the chip model), it will appear as an "unknown device" in the device manager. At this point, the driver should be reinstalled.
    - The Arduino IDE installation directory has a drivers directory containing the official version of the Arduino driver.You can select the unknown device, update the driver, and point the search directory to the drivers directory.
  - Start the Arduino IDE
    - Open the Arduino IDE on your PC.
    - Click on "Tool - Board" to select the correct development board model.
    ![Alt text](https://raw.githubusercontent.com/littletwany/PICTURE/master/img/board.png)
    - Click "Tool - Port" to select the correct serial port (the serial port shown in device manager in the previous step)
    ![Alt text](https://raw.githubusercontent.com/littletwany/PICTURE/master/img/port.png)
   -  "Hello , world"
      - Create a new file "hello",then write the following code in the Arduino program:
      ```C
      void setup() {
      Serial.begin(9600); // initializes the serial port with a baud rate of 9600
       }
      void loop() {
       Serial.println("hello, world"); // prints a string to a serial port
       delay(1000); //delay of 1 second
       }
       ```
      - In the upper left corner of the Arduino IDE, there are two buttons. First, press the compile button to compile. After the compilation is successful, press the upload button.
    ![Alt text](https://raw.githubusercontent.com/littletwany/PICTURE/master/img/func.png)
      - Click the "tool-serial monitor" menu, or click the serial monitor in the upper right corner, you can see the program running results
    ![Alt text](https://raw.githubusercontent.com/littletwany/PICTURE/master/img/print.png)
      - Congratulations! Your first Arduino program is running.
    

### 4. How is Seeeduino configured?
 - Connect the Seeeduino board to our computer using a USB cable.Right-click my computer, select control panel, and open device manager.
 - View ports (COM and LPT).We should see an open port called USB serial port, right-click USB serial port, and select the update driver software option.
 - Select the "browse my computer driver software" option and select the drive file "FTDI USB Drivers" in the Drivers folder downloaded by Arduino software.
 - We can check if the driver is installed by opening Windows device manager.Look for USB serial port in the port section.You can also see the serial port in the Arduino environment.

## Section 2: Building The First Open Source Control System 
### 1. The minimum composition of the control system and the composition of the assembly board
 - Start with a simple example, the automatic door, when someone approaches it, the distance sensor senses it, sends a signal, the controller receives the signal, the signal is output to the actuator, the actuator opens the door.
So the control system is made up of three parts:
   - Inputs: obviously, temperature and humidity sensors, triaxial accelerometers, hall sensors, light sensors, and sound sensors can all act as inputs, transmitting the perceived temperature, humidity, acceleration, or light signal data to the controller.
   - Control: the controller, the microprocessor, is the development board module, according to the input signal issued instructions, so that the actuator to make the corresponding action and response.
   - Output: an OLED, LED light or buzzer can be used as an output module that converts electrical energy into sound, sound or light an OLED display screen, for example, can display different patterns, which is its output.
 - How does the controller know to open the door when it receives input from the sensor?This involves the new concept of "code"."Code" is the equivalent of "thought" in our brain. It can process the input signal so that the input system can communicate with the controller, and it can also process the output signal so that the controller can communicate with the output system.
 - In general, the input unit, the control unit, and the output unit are the hardware, the body of our device, and the code is the software.

### 2. Analog signal, Digital signal, Protocol signal (also a kind of digital signal)
We already know that the input system, the controller and the output system communicate by processing the input and output signals in code. The signals here are equivalent to the "nerve impulses" of the brain. They are divided into digital signals and analog signals.
 - Analog signals: signals vary continuously in time and value, and the amplitude, frequency, or phase of the signal changes continuously at any time, such as the current broadcast sound signal, or image signal, etc.The analog signal has sine wave and triangle wave and so on.The analog pins of your microcontroller can have between 0V and 5V is mapped to a range between 0 and 1023.1023 is mapped as 5V and 512 is mapped as 2.5v.
  ![Alt text](https://raw.githubusercontent.com/littletwany/PICTURE/master/img/analog.png)
 - Digital signal: digital signal refers to the value of the amplitude is discrete, the amplitude is limited to a finite number of values. In our controller, the digital signal has two states: LOW (0V) for 0;HIGH level: HIGH (5V), stands for "1".
  ![Alt text](https://raw.githubusercontent.com/littletwany/PICTURE/master/img/digital.png)
 - Protocol signal: the protocol signal we use is I2C, so here is a brief introduction to I2C.I2C bus you just need to two wires in the transmission of information connection between the devices on the bus, the SDA (serial data line) and SCL (serial clock line), these two lines are bidirectional I/O lines, the main component used to start the bus transfer data, and generate the clock to open transmission device, any devices that are addressing at this time is considered from the device.The relationship between master and slave, sender and receiver on the bus is not constant, but depends on the direction of data transmission.If the host wants to send data to the slave device, the host first addresses the slave device, then actively sends data to the slave device, and finally terminates the data transmission by the host.If the host is to receive data from the slave, the slave is first addressed by the master.The host then receives the data sent from the device, and the host terminates the receiving process. In this case.The host is responsible for generating the timing clock and terminating the data transfer.
### 3. Seeeduino's interface distribution
 - Take a look at the seeeduino development board in the middle of the suite, the diagram below gives you an overview.Grove Connectors SeeedStudio has a variety of sensors/devices that can make use of this analog,Digital,I2C and UART connection.
 - In addition, we have separate Grove connectors, and you can also use Grove wiring to connect modules to the corresponding interfaces on the seeeduino development board.
## Section 3: Output Control
### 1. Turn on the LED light
 - Project description: how to light the first LED light
We have completed the output "Hello world" program.Now let's learn how to light the LED module.We know the three basic components of a control system: input, control, and output, but the "light LED" section USES only the output, not the input.Single chip microcomputer is the control unit, LED module is the output unit and the output signal is digital signal.
 - list of materials: Seeeduino Lotus, Grove LED, Grove cable
 - hardware connection:
   - Module connection
      - default onboard interface specification;
      - use a Grove cable to connect the Grove LED to Seeeduino Lotus's digital interface D5.  
   - Connect the microcontroller to the computer through the USB cable.
   - Make sure the power, grounding and signal wires are all connected correctly, or you may damage the boards.
 - hardware analysis:The development board is the control unit and the LED lamp is the output unit
  
 - Software code:
     - Open Arduino IDE. 
     - You can copy the code directly to Arduinoied. Although we encourage you to type the code out by hand to develop your skills.
     - When you're done, click Verify to check for syntax errors.Verify that there are no errors, and you can upload the code.
```C
// Item One —— LED Blink
//The LED will turn on for one second and then turn off for one second
int ledPin = 5;
void setup() {
pinMode(ledPin, OUTPUT);
}
void loop() {
digitalWrite(ledPin, HIGH);
delay(1000);
digitalWrite(ledPin, LOW);
delay(1000);
}
```
 - software analysis:
 **set up ()**<br>It is used primarily to write code that initializes.The setup() function is called only once after the MCU is started.
 **loop ()**<br>A cyclic function.After the setup() function is completed, the MCU will call the loop() function, and the loop() function will be loop called.
 **int ledPin = 5;**<br>Here, we assigned the variable name "ledPin" to pin5, that is to say, ledPin stands for pin5 on the microcontroller.
 **pinMode(ledPin, OUTPUT);**<br>Set ledPin to output mode.
**digitalWrite(ledPin, HIGH);**<br>When we set the ledPin as output, HIGH means sending high level to the pin, LED on.
**digitalWrite(ledPin, LOW);**<br>When we set the led as output, low stands for sending low level to the pin, LED off.
**delay(1000);**<br>The number in parentheses represents the number of milliseconds of delay.1000 milliseconds is 1 second, which means the delay is 1 second.

- Practice: adjust how quickly led flashing of lights.
   - Functional: By modifying the software code to adjust LED lights flicker frequency and the light and shade.
   - The hardware list: Seeeduino Lotus, Grove LED, Grove cable
   - The hardware connection and the analysis of hardware are the same as the above.
   - Try adjusting the Numbers in brackets to change the frequency at which the bulb flashes.
   Such as "delay(500);",turn the LED on for 500ms and off for 500ms.
   
## Section 4: Input Control 

After the study of the third section, we should have a great understanding of both the control module and the output module. In this section, we try to add the input module to realize the control of the output through the control module. Doesn't it sound very interesting?Try it now!

### 1. Press the button - digital signal input

The first thing we need to know is that the input of the button is a digital signal, and there are only two states, 0 or 1, so we can control the output based on those two states.
 - Practice: control led lighting by pushing button.
 - Hardware listings: Seeeduino Lotus, Grove LED, Grove Button
 - Hardware connection:
   - Module connection:
     - The default onboard interface specifies:
     - Use a Grove cable to connect the Grove LED to Seeeduino Lotus's digital interface D5,connect the Grove Button to digital interface D2.
   - The microcontroller is then connected to the computer via a USB cable.
 - Hardware analysis: 
   - Input unit: Bbutton 
   - Control unit：microcontroller
   - Output unit：LED module
   Both the sensor and the LED use digital signals, so they should be connected to digital interfaces.
 - Software code: 
   - Open Arduino IDE. 
   - You can copy the code directly to Arduinoied. Although we encourage you to type the code out by hand to develop your skills.
   - When you're done, click Verify to check for syntax errors.Verify that there are no errors, and you can upload the code.
```c
// Item Two —— Button ControlS LED
// constants won't change. They're used here to set pin numbers:
const int buttonPin = 2;     // the number of the pushbutton pin
const int ledPin =  5;      // the number of the LED pin

// variables will change:
int buttonState = 0;         // variable for reading the pushbutton status

void setup() {
  // initialize the LED pin as an output:
  pinMode(ledPin, OUTPUT);
  // initialize the pushbutton pin as an input:
  pinMode(buttonPin, INPUT);
}

void loop() {
  // read the state of the pushbutton value:
  buttonState = digitalRead(buttonPin);

  // check if the pushbutton is pressed. If it is, the buttonState is HIGH:
  if (buttonState == HIGH) {
    // turn LED on:
    digitalWrite(ledPin, HIGH);
  } else {
    // turn LED off:
    digitalWrite(ledPin, LOW);
  }
}
```
 - Code analysis:
 **pinMode(ledPin, OUTPUT);**<br>Define LED as the output unit.
 **pinMode(buttonPin, INPUT);**<br>Define button as the input unit.
 **buttonState = digitalRead(buttonPin);**<br>This function is used to read the states of digital pins, either HIGH or LOW. When the button is pressed, the
state is HIGH, otherwise is lOW.
 **if (buttonState == HIGH) {**<br>  **digitalWrite(ledPin, HIGH);**<br>**} else {**<br>  **digitalWrite(ledPin, LOW);**  <br> **}**<br>The usage of the statement is: if the logical expression in parentheses is true, execute the statement in curly braces after **if**, if not, execute the statement in curly braces after the **else**.  
  If the state of the button is high, the LED pin outputs a high level and turn the LED  on, else turn LED off.

 ### 2. Rotary potentiometer -- analog signal input

 - Practice: Turn the knob to control the frequency of LED flashing.
Unlike buttons, the signals entered by knobs are analog.Unlike digital signals, analog signals range in value from 0 to 1023.We can control the frequency of led flashing based on this signal.
 - Hardware listings: Seeeduino Lotus, Grove LED, Grove Rotary Switch
 - Hardware connection:
   - Module connection:
     - The default onboard interface specifies:
     - use a Grove cable to connect LED to Seeeduino Lotus's digital interface D5, and a Grove cable to connect the Grove Rotary Switch to analog signal interface A1.
   - The microcontroller is then connected to the computer via a USB cable.
- Hardware analysis:
  - Input unit: knob
  - Control unit: microcontroller
  - Output unit: LED module    
The input is an analog signal, so it is connected to the analog signal interface, the LED module is connected to the digital signal interface.
 - Software code: 
   - Open Arduino IDE. 
   - You can copy the code directly to Arduinoied. Although we encourage you to type the code out by hand to develop your skills.
   - When you're done, click Verify to check for syntax errors.Verify that there are no errors, and you can upload the code.

```c
// Item Three —— Rotary controls LED
int rotaryPin = A1;    // select the input pin for the rotary
int ledPin = 5;      // select the pin for the LED
int rotaryValue = 0;  // variable to store the value coming from the rotary

void setup() {
  // declare the ledPin as an OUTPUT:
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // read the value from the sensor:
  rotaryValue = analogRead(rotaryPin);
  // turn the ledPin on
  digitalWrite(ledPin, HIGH);
  // stop the program for <sensorValue> milliseconds:
  delay(rotaryValue);
  // turn the ledPin off:
  digitalWrite(ledPin, LOW);
  // stop the program for for <sensorValue> milliseconds:
  delay(rotaryValue);
}
```

 - Code analysis:

   **rotaryValue = analogRead(rotaryPin);**<br>This function is used to read the value of Analog  pins, the range of values is: 0 ~ 1023. 
   **delay(rotaryValue);**<br> Realize delay function, The millisecond duration of the delay is the value in parentheses. Because the value is the value of the analog signal of the knob pin being read, so the delay time can be controlled by the knob.


## Section 5: First Knowledge Sensor

In the previous section, we have used buttons and knobs as control modules, but there are still many sensors that have not been used, so let's take a look at each one.

### 1. Light Sensor - photoswitch

The light sensor contains a photosensitive resistor to measure the intensity of light. The resistance of the photosensitive resistor decreases with the increase of light intensity. The output signal is the analog value, the brighter the light source, the larger the analog value. Based on this property, you can use it to make a light switch.
- exercise: as the environment slowly brightens, the LED lights will lighten. As the light slowly dimmed, the LED dimmed. The LED will go from dark to light or from light to dark. To achieve this, we will use pulse width modulation.
 - List of materials: Seeeduino Lotus, Grove LED, Grove cable, Grove Light Sensor
 - Hardware connection:
   - Module connection:
     - The default onboard interface specifies:
     - Use Grove wire: Connect the Grove LED to Seeeduino Lotus's digital signal interface D5,connect the Grove Light Sensor to Seeeduino Lotus's analog signal interface A2.
   - The microcontroller is then connected to the computer via a USB cable.
 - Hardware analysis: like the knob, the light sensor is an input device, and its output signal is also an analog signal. The LED is an output device, but unlike project 1, we are using an analog output. See the code analysis section for details.
 - Software code: 
   - Open Arduino IDE. 
   - You can copy the code directly to Arduinoied. Although we encourage you to type the code out by hand to develop your skills.
   - When you're done, click Verify to check for syntax errors.Verify that there are no errors, and you can upload the code.
   ```c
   // Item Four —— Photoswitch
   int sensorpin = A2; // Analog input pin that the sensor is attached to
   int ledPin = 5;    // LED connected to digital pin 9
   int sensorValue = 0;        // value read from the pot
   int outputValue = 0;        // value output to the PWM (analog out)

   void setup() {
   pinMode(ledPin,OUTPUT);
   }

   void loop() {
   // read the analog in value:
   sensorValue = analogRead(sensorpin);
   // map it to the range of the analog out:
   outputValue = map(sensorValue, 0, 1023, 0, 255);
   // change the analog out value:
   analogWrite(ledPin, outputValue);
   delay(30);
   }
   ```
 - Code analysis:
   **PFM( Pulse Width Modulation)**
   - It is based on a series of Pulse Width Modulation, the equivalent of the required waveform (including shape and amplitude), the analog signal level for digital encoding, that is to say, by adjusting the duty ratio of the change to the change of the signal to adjust, and energy, duty cycle is to point to in a cycle, the signal at a high level of the percentage of the time to occupy the whole signal cycle, for example, the square wave duty ratio is 50%.
   - There are six digital pins on your microcontroller that are marked with the symbol “~”, which means they can send out a PWM signal : 3,5,6,9,10,11. They are celled PWM pins.   

   **outputValue = map(sensorValue, 0, 1023, 0, 255);**

   **outputValue** keep equal and potentiometer after mapping the value of the time. **map** has five parameters, which in turn is: to map the original value, the original value of the minimum value, original value maximum, minimum value after the mapping, mapping the maximum. In this way, the data returned by the sensor can be mapped from its original value of 0-1023 to 0-255.

   **analogWrite(ledPin,outputvalue)**

   The function is used to write an analog value between 0 - 255 a PWM pin. analogWrite() can only be used for PWM pins. The new mapping data in the previous statement can be output to ledPin to lighten / dim the LED.

### 2. Sound Sensor - voice-activated sensor light 

The sound sensor can detect the sound intensity of the environment, and its output is also simulated.I'm sure you've all been exposed to the sound control lights, but now we can do one ourselves, and with the basics, this experiment will be easy for you.
 - Practice: The LED lights light up when the sound is made. When there is no sound and it is very quiet, the LED lights go off.
 - List of materials: Seeeduino Lotus, Grove LED, Grove cable, Grove Sound Sensor
 - Hardware connection:
   - Module connection:
     - The default onboard interface specifies:
     - Use Grove wire: Connect the Grove LED to Seeeduino Lotus's digital signal interface D5, Connect the Grove Sound Sensor to Seeeduino Lotus's analog signal interface A0.
   - The microcontroller is then connected to the computer via a USB cable.
- Software code: 
   - Open Arduino IDE. 
   - You can copy the code directly to Arduinoied. Although we encourage you to type the code out by hand to develop your skills.
   - When you're done, click Verify to check for syntax errors.Verify that there are no errors, and you can upload the code.
   ```c
  // Item Five — Sound Control Light
  int soundPin = 0; // Analog sound sensor is to be attached to analog
  int ledPin = 5; // Digital LED is to be attached to digital
  void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
  }
  void loop(){
  int soundState = analogRead(soundPin); // Read sound sensor’s value
  Serial.println(soundState);
  // if the sound sensor’s value is greater than 20, the light will be on for 5 seconds.
  //Otherwise, the light will be turned off
  if (soundState > 20) {
  digitalWrite(ledPin, HIGH);
  delay(5000);
  }else{
  digitalWrite(ledPin, LOW);
  }
  }

  ```
 - Code analysis:
 **Serial.begin(9600);**
 The software running on the computer communicates with the development board, and the baud rate is 9600.
 **Serial.print(" ");**
 This function is used to output data from the serial port, the output is what is contained in the double quotation marks.
 **Serial.println( );**
 This statement is similar to the one above, except that **serial.println** has a newline return.
 **Serial.println(soundState);**
 Serial port print the sound sensor’s value.  So you open the **serial monitor** on the IED interface, and you see the value of the output sensor.

### 3. Temperature and Humidity Sensor - sensing weather

Have you ever wondered about the temperature and humidity of your surroundings?Want to know the exact number?Want to wear a skirt or coat today depending on the temperature?Let's make a hygrometer!
 - Practice: Let your OLED display display the current ambient temperature and humidity.
 - List of materials: Seeeduino Lotus, Grove OLED, Grove cable, Grove Temperature and Temperature Sensor
 - Hardware connection:
   - Module connection:
     - The default onboard interface specifies:
     - Use Grove wire: Connect the OLED to Seeeduino Lotus's I2C interface (note: IIC's default address is 0x78). Connect the Grove Temperature and Humidity Sensor to Seeeduino Lotus's digital signal interface D4.
   - The microcontroller is then connected to the computer via a USB cable.
 - Software code: 
   - Open Arduino IDE. 
   - Download the  [ Seeed DHT library](https://github.com/Seeed-StudioGrove_Temperature_And_Humidity_Sensor)  from Github. Clink on **Sketch** > **Include library** > **Add .ZIP library**, import the library into the IED.
   - You can copy the code directly to Arduinoied. Although we encourage you to type the code out by hand to develop your skills.
   - When you're done, click Verify to check for syntax errors.Verify that there are no errors, and you can upload the code.
 - Code analysis:
### 4. Hall Sensor - the mystery of the magnetic field
   The Hall sensor is based on Hall Effect, which is the production of a voltage difference across an electrical conductor, transverse to an electric current in the conductor and a magnetic field perpendicular to the current. There is a continuous-time switch on this Grove. The output of these devices switches low (turns on) when a magnetic field (south polarity) perpendicular to the Hall sensor exceeds the operate point threshold BOP, and it switches high (turn off) when the magnetic field disappears. The twig can be used to measure RPM.The Hall Sensor is used by utilizing the external interrupts available on the arduino/seeeduino. In this example we are using interrupt 0, found on digital pin 7. 
 - Practice: When a magnet whose south pole is facing up is approaching to the onboard sensor, the Buzzer will be turned on. Otherwise, the Buzzer will be turned off.
 - List of materials: Seeeduino Lotus, Grove Buzzer, Grove cable, Hall sensor
 - Module connection:
     - The default onboard interface specifies:
     - Use Grove wire: Connect the Grove Buzzer to Seeeduino Lotus's digital signal interface D6, Connect the Hall sensor to Seeeduino Lotus's digital signal interface D7. 
   - The microcontroller is then connected to the computer via a USB cable.
- Software code: 
   - Open Arduino IDE. 
   - You can copy the code directly to Arduinoied. Although we encourage you to type the code out by hand to develop your skills.
   - When you're done, click Verify to check for syntax errors.Verify that there are no errors, and you can upload the code.
   ```c
  // Item Seven — Hall Sensor
  // constants won't change. They're used here to set pin numbers:
  const int HallPin = 7;     // the number of the Hall Sensor pin
  const int BuzzerPin =  6;      // the number of the Buzzer pin

  // variables will change:
  int HallState = 0;         // variable for reading the Sensor status

  void setup() {
  // initialize the Buzzer pin as an output:
  pinMode(BuzzerPin, OUTPUT);
  // initialize the Sensor pin as an input:
  pinMode(HallPin, INPUT);
  }

  void loop() {
  // read the state of the Sensor value:
  HallState = digitalRead(HallPin);

  if (HallState == LOW) {
    // the buzzer sounded:
    digitalWrite(BuzzerPin, HIGH);
  } else {
    // the buzzer doesn't make a sound:
    digitalWrite(BuzzerPin, LOW);
  }
  }
   ```
 - Code analysis:
 **if (HallState == LOW){ }**
 This is a judgment statement to see if there is a magnet near the Hall sensor, if so, the output signal of the hall sensor is LOW, the Buzzer sounded a warning.

### 5. Charm of triaxial accelerometer - gravity Acceleration

This is the last sensor, the triaxial accelerometer, and with this module, you can easily add motion monitoring to your design. So we can do a lot of interesting little experiments on the basis of motion.
 - Practice: when motion is detected, the buzzer gives an alarm indicating that the object is in motion.
 - List of materials: Seeeduino Lotus, Grove cable, Grove 3-axis Accelerometer
 - Hardware connection:
   - Module connection:
     - The default onboard interface specifies:
     - Use Grove wire: Connect Grove 3-axis Accelerometer to Seeeduino Lotus's I2C interface using a Grove cable (note: IIC default address is 0x4c).
   - The microcontroller is then connected to the computer via a USB cable.
- Open Arduino IDE. 
   - Download the  [Repository for 3-Axis Digital Accelerometer(±1.5g)](https://github.com/Seeed-Studio/Accelerometer_MMA7660)  from Github. Clink on **Sketch** > **Include library** > **Add .ZIP library**, import the library into the IED.
   - You can copy the code directly to Arduinoied. Although we encourage you to type the code out by hand to develop your skills.
   - When you're done, click Verify to check for syntax errors.Verify that there are no errors, and you can upload the code.
   - In this program, acceleration information are sent from the sensor to Seeeduino via I2C bus and then Seeeduino printed them onto the serial monitor. Open the **serial monitor** to check the result.
   ```c
   // Item Eight — Gravity Acceleration
   #include <Wire.h>
   #include "MMA7660.h"
   MMA7660 accelemeter;
   void setup()
  {
	accelemeter.init();  
	Serial.begin(9600);
  }
  void loop()
  {
	int8_t x;
	int8_t y;
	int8_t z;
	float ax,ay,az;
	accelemeter.getXYZ(&x,&y,&z);
	
  Serial.print("x = ");
  Serial.println(x); 
  Serial.print("y = ");
  Serial.println(y);   
  Serial.print("z = ");
  Serial.println(z);
	
	accelemeter.getAcceleration(&ax,&ay,&az);
  Serial.println("accleration of X/Y/Z: ");
	Serial.print(ax);
	Serial.println(" g");
	Serial.print(ay);
	Serial.println(" g");
	Serial.print(az);
	Serial.println(" g");
	Serial.println("*************");
	delay(1000);
  }
   ```
 - Code analysis:
 **#include <Wire.h>**
 **#include** is an instruction that introduces a header file.
 Here we use the <Wire.h> library, this library is included in Arduino IDE. 
 **#include "MMA7660.h"**
 Represents the MMA766O.h header file that introduces the current path.
 **MMA7660 accelemeter;**
 Once the object is declared, you can use functions from the library.
 **accelemeter.getXYZ(&x,&y,&z);**
 It is a function from the library, call this function, and you get the raw data of x,y and z.
 **accelemeter.getAcceleration(&ax,&ay,&az);**
 By calling this function, you get the triaxial acceleration information converted to the unit gravity "g".




## Section 6: Colorful Experimental Projects


### 1. Music dynamic rhythm lamp
 - Project description: In this experiment, we will make the buzzer play pleasant music and the led lights flash according to the music frequency and beat.
 - Materials: Seeeduino Lotus, Grove LED, Grove cable, Buzzer, Button
 - Hardware connection:
   - Module connection:
     - The default onboard interface specifies:
     - Connect Grove LED to Seeeduino Lotus's digital signal interface D5, connect Buzzer to Seeeduino Lotus's digital signal interface D6.
   - The microcontroller is then connected to the computer via a USB cable.
 - Software code: 
   - Open Arduino IDE. 
   - You can copy the code directly to Arduinoied. Although we encourage you to type the code out by hand to develop your skills.
   - When you're done, click Verify to check for syntax errors.Verify that there are no errors, and you can upload the code.

  ```c
  // Item Nine — Music Dynamic Rhythm Lamp
  #define NTD0 -1
  #define NTD1 294
  #define NTD2 330
  #define NTD3 350
  #define NTD4 393
  #define NTD5 441
  #define NTD6 495
  #define NTD7 556

  #define NTDL1 147
  #define NTDL2 165
  #define NTDL3 175
  #define NTDL4 196
  #define NTDL5 221
  #define NTDL6 248
  #define NTDL7 278

  #define NTDH1 589
  #define NTDH2 661
  #define NTDH3 700
  #define NTDH4 786
  #define NTDH5 882
  #define NTDH6 990
  #define NTDH7 112
 
  #define WHOLE 1
  #define HALF 0.5
  #define QUARTER 0.25
  #define EIGHTH 0.25
  #define SIXTEENTH 0.625

  int tune[]=
  {
  NTD3,NTD3,NTD4,NTD5,
  NTD5,NTD4,NTD3,NTD2,
  NTD1,NTD1,NTD2,NTD3,
  NTD3,NTD2,NTD2,
  NTD3,NTD3,NTD4,NTD5,
  NTD5,NTD4,NTD3,NTD2,
  NTD1,NTD1,NTD2,NTD3,
  NTD2,NTD1,NTD1,
  NTD2,NTD2,NTD3,NTD1,
  NTD2,NTD3,NTD4,NTD3,NTD1,
  NTD2,NTD3,NTD4,NTD3,NTD2,
  NTD1,NTD2,NTDL5,NTD0,
  NTD3,NTD3,NTD4,NTD5,
  NTD5,NTD4,NTD3,NTD4,NTD2,
  NTD1,NTD1,NTD2,NTD3,
  NTD2,NTD1,NTD1
};

 float durt[]=
{
  1,1,1,1,
  1,1,1,1,
  1,1,1,1,
  1+0.5,0.5,1+1,
  1,1,1,1,
  1,1,1,1,
  1,1,1,1,
  1+0.5,0.5,1+1,
  1,1,1,1,
  1,0.5,0.5,1,1,
  1,0.5,0.5,1,1,
  1,1,1,1,
  1,1,1,1,
  1,1,1,0.5,0.5,
  1,1,1,1,
  1+0.5,0.5,1+1,
};

  int length;
  int tonepin=6;
  int ledp=5;

void setup()
{
  pinMode(tonepin,OUTPUT);
  pinMode(ledp,OUTPUT);
  length=sizeof(tune)/sizeof(tune[0]);
}

void loop()
{
  for(int x=0;x<length;x++)
  {
    tone(tonepin,tune[x]);
    digitalWrite(ledp, HIGH); 
    delay(400*durt[x]);
    digitalWrite(ledp, LOW);
    delay(100*durt[x]);
    noTone(tonepin);
    
  }
  delay(4000);
}
 ```

 - Code analysis:
  
   **#define NTD**
   Here is the definition of the frequency of the D key, which is divided into bass, alto, and treble.
   **#define WHOLE 1**
   **#define HALF 0.5**
   **#define QUARTER 0.25**
   **#define EIGHTH 0.25**
   **#define SIXTEENTH 0.625**
   Note rhythm is divided into one beat, half beat, 1/4 beat, 1/8 beat, we specify a beat note time is 1;Half beat is 0.5;1/4 beat is 0.25;1/8 of 0.125.
   **int tune[]=**
   List the frequencies according to the spectrum.
   **float durt[]=**
   List the beats according to the spectrum.
   **delay(400*durt[x]);**
   **delay(100*durt[x]);**
   Control LED lights on and off respectively.


### 2. Make an intelligent sound-light induction desk lamp
 - Project description: as the name implies, this project is to make a small lamp controlled by Sound and Light. We need to use LED module. Of course, Light Sensor and Sound Sensor are also indispensable. In this way, you can achieve the function of the smart desk lamp: when the sound, the lamp will light up;If the environment turns dark, the lamp will automatically turn brighter.
 - Materials: Seeeduino Lotus, Grove LED, Grove cable, Light Sensor, Sound Sensor
  - Hardware connection:
    - Module connection:
      - The default onboard interface specifies:
      - Connect the Grove LED to Seeeduino Lotus's digital signal interface D5, Connect the Light Sensor to Seeeduino Lotus's analog signal interface A2. Connect the Sound Sensor to Seeeduino Lotus's analog signal interface A0 using a Grove cable.
    - The microcontroller is then connected to the computer via a USB cable.
 - Software code: 
   - Open Arduino IDE. 
   - You can copy the code directly to Arduinoied. Although we encourage you to type the code out by hand to develop your skills.
   - When you're done, click Verify to check for syntax errors.Verify that there are no errors, and you can upload the code.

   ```c
   // Item Ten — light Induction Desk Lamp
   int soundPin = 0; // Analog sound sensor is to be attached to analog
   int lightPin = A2; //Analog light sensor is to be attached to analog
   int ledPin = 5; // Digital LED is to be attached to digital

   void setup() {
   pinMode(ledPin, OUTPUT);
   }
   void loop(){
   int soundState = analogRead(soundPin); // Read sound sensor’s value
   int lightState = analogRead(lightPin); // Read light sensor’s value
   // if the sound sensor's value is greater than 50 or the sound sensor's is less than 10, the light will be on.
   //Otherwise, the light will be turned off
   if (soundState > 50 || lightState < 10) {
   digitalWrite(ledPin, HIGH);
   //delay(5000); //You can delete the "//" to make the LED on for five seconds
   }else{
   digitalWrite(ledPin, LOW);
   }
   }
   ```
  - The code analysis:
 **if (soundState > 50 || lightState < 10) { }**
 In parentheses is a logical expression.
 Both **&&** and **||** are commonly used in logical expressions. The common usage is **if (expression 1 || expression 2)** and **if (expression 1 && expression 2)**.
 **||** represents "**or**", satisfies one of them, the whole expression is true, and satisfies the condition of the if judgment.
 **&&** means "**and**", the statement in if{} is executed only if all expressions in parentheses are true.