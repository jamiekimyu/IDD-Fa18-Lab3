# Data Logger (and using cool sensors!)

*A lab report by John Q. Student.*

## In The Report

Include your responses to the bold questions on your own fork of [this lab report template](https://github.com/FAR-Lab/IDD-Fa18-Lab2). Include snippets of code that explain what you did. Deliverables are due next Tuesday. Post your lab reports as README.md pages on your GitHub, and post a link to that on your main class hub page.

For this lab, we will be experimenting with a variety of sensors, sending the data to the Arduino serial monitor, writing data to the EEPROM of the Arduino, and then playing the data back.

## Part A.  Writing to the Serial Monitor
 
**a. Based on the readings from the serial monitor, what is the range of the analog values being read?**
<br/>0 - 1023
 
**b. How many bits of resolution does the analog to digital converter (ADC) on the Arduino have?**
<br/>10 bit resolution

## Part B. RGB LED

**How might you use this with only the parts in your kit? Show us your solution.**
[RGB Led](https://www.youtube.com/watch?v=RAVb8aH5-l4)
<br/> I added resistors to each of the R,G,B legs and Ground. I connected the common anode to 5V and connected to power. The result is shown in the linked video. 

## Part C. Voltage Varying Sensors 
 
### 1. FSR, Flex Sensor, Photo cell, Softpot

**a. What voltage values do you see from your force sensor?**
<br/> The force sensor outputs values ranging from 0 - 950, depending on the applied pressure. 0V - 5V corresponds to 0 - 1023 so a reading of 950 implies that 92% of the 5V total being read. In other words, the voltage values of the sensor range from 0V - 4.64V. 

**b. What kind of relationship does the voltage have as a function of the force applied? (e.g., linear?)**
<br/> The relationship between voltage and the force applied does not have a linear relationship and instead seems to be a logarthmic relationship. This is due to the fact that in the beginning, the force applied has a large effect(minimal force gives a large output) but as more force is applied the effect on output decreases - reflecting a logarthmic relatinship. 

**c. Can you change the LED fading code values so that you get the full range of output voltages from the LED when using your FSR?**
Yes. The FSR outputs values that ranges from 0-1024. However, the LEDs use values that range from 0-255. Therefore, I adjusted the ratio of the FSR output to match the LED ranges and then used those values in the code. 

**d. What resistance do you need to have in series to get a reasonable range of voltages from each sensor?**
The resistors provided in our kit (220 Ohms) seemed to get reasonable ranges of voltages from each sensor. 

**e. What kind of relationship does the resistance have as a function of stimulus? (e.g., linear?)**
As there is more voltage there is less resistance with the 2 variables having a logarithmic relationship. 

### 2. Accelerometer
 
**a. Include your accelerometer read-out code in your write-up.** 
<br/>[Code](https://github.com/jamiekimyu/IDD-Fa18-Lab3/blob/master/accelerometer.ino)

### 3. IR Proximity Sensor

**a. Describe the voltage change over the sensing range of the sensor. A sketch of voltage vs. distance would work also. Does it match up with what you expect from the datasheet?**
As distance decreases from the object to the sensor, proximity increases and ambience decreases. Voltage increases as distance decreases and proximity increases.

**b. Upload your merged code to your lab report repository and link to it here.**
<br/>[Merged Code](https://github.com/jamiekimyu/IDD-Fa18-Lab3/tree/master)

## Optional. Graphic Display

**Take a picture of your screen working insert it here!**

## Part D. Logging values to the EEPROM and reading them back
 
### 1. Reading and writing values to the Arduino EEPROM

**a. Does it matter what actions are assigned to which state? Why?**
Yes the actions assigned to each state matter in order to have the right logical order in the write/read/clear loop. In our case in the lab, the pentiometer controlled the state - in other words if you turned the knob to the right part of the circle a state was activated (i.e. 0 to  (1024/3) is state 1, (1024/3) to (10242/3) is state 2, and 10242/3 to 1023 is state 3). The states have to be in the right order in order to complete a proper loop of writing, reading, and then clearing from the EEPROM. 

**b. Why is the code here all in the setup() functions and not in the loop() functions?**
The code for all the individual states were put in setup() so it could run once at the beginning instead of in a loop. The code in the loop is in the 'master tab' that contains the switch cases for each state. 

**c. How many byte-sized data samples can you store on the Atmega328?**
1024 bytes of memory 

**d. How would you get analog data from the Arduino analog pins to be byte-sized? How about analog data from the I2C devices?**
To send analog data from an I2C device you would need to convert it to byte-size. To do this you can use the highByte() and lowByte() functions to extract the values. 

**e. Alternately, how would we store the data if it were bigger than a byte? (hint: take a look at the [EEPROMPut](https://www.arduino.cc/en/Reference/EEPROMPut) example)**
If the data was bigger than a byte you can convert it into memory (or into EEPROM - Electrically Erasable Programmable Read-Only Memory) .

**Upload your modified code that takes in analog values from your sensors and prints them back out to the Arduino Serial Monitor.**
<br/> [Code](https://github.com/jamiekimyu/IDD-Fa18-Lab3/tree/master)

### 2. Design your logger
 
**a. Insert here a copy of your final state diagram.**
![photo](https://github.com/jamiekimyu/IDD-Fa18-Lab3/blob/master/20180917_204702.jpg)

### 3. Create your data logger!
 
**a. Record and upload a short demo video of your logger in action.**
<br/> [Video](https://www.youtube.com/watch?v=DitWKNQQdy8)
