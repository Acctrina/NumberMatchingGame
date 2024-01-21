# Project Overview
A memory-based number matching game to help keep the minds of seniors active through daily use of their cognitive functions to help combat the long-term effects of dementia. This project has been made to be used in active ageing centers around Singapore and has been specifically designed with simplicity in mind to be catered to the elderly for ease of use, as well as to be contactless for hygiene purposes.

# Board Design

**Slave Board:**
The slave board design uses a MAX7219 Dot Matrix LED to display the patterns and HC-SR04 Ultrasonic sensors to trigger the displays to light up when sensed. The slave modules are programmed using a 8-bit microcontroller, the ATMega328p

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/c4f2b396-3dd8-48a7-b5f0-ae9abd4ece87)

**Master Board:**
Likewise, the master board design also uses the ATMega328p microcontroller and works identically to an Arduino Uno. The only difference is that there are dedicated I2C pin connections for communication between Master and Slave boards along with pins for the timer module for neater connections.

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/f4ec0a28-9d5d-49f7-a58d-c33a610909c8)

**Timer Module:**
The timer module is a 4 in 1 MAX7219 Dot Matrix Display Module and is controlled by the master board through SPI. This displays a timer that counts up when the game is started and stops it when it has ended.

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/3678c471-1e97-4023-8fda-ca1d1d344bfc)

**Reset Module:**
The reset module is identical to the slave module, with the difference being only the code used to program it. With its function to reset the game when sensed. It also serves a double function as a display to show the last number sensed by the player.

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/0036f85e-7c0d-4ca1-a1fb-bf9fbda18f40)

# Design Layout

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/47ecc119-1130-4fc3-9355-0b17b7d92e75)

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/5e83c2ea-7a28-40e9-9256-1e3260ff35e1)

# Program Overview #

The master program is responsible for transmitting a random number from a set sequence to each slave board as well as the comparison to see if a pair of numbers that has been sensed are matching or not. In which case, it will then tell the respective slave boards that have been sensed to remain turned ON if it matches or OFF if otherwise. It also controls the Timer module and Reset Module.

The slave board is responsible for lighting up when sensed, showing its assigned digit and to inform the master when it has been sensed.

The timer module is for keeping track of the duration the game lasts for as soon as it starts.

The reset module serves two purposes, one which is to start a new game while the other is to act as a display to show the previously sensed number

### Flow Chart of Respective Programs: ###


![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/53bb8849-5473-4b21-b50d-bf73d94046d7)

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/011318c9-3b5a-4fcb-91ad-2b5e70e12cb5)

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/919cc6ac-404c-4e55-a476-5ba06b3f8d11)

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/2ca6f513-48c4-4f37-933c-5290b4d9802b)

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/02108a42-d5bd-404e-9f86-8631930e7cd8)


# Master Program #

The master program mainly uses 2 libraries, Wire.h to allow communication between I2C devices and Ledcontrol.h to support up to 8 daisy chained MAX72XX drivers for the timer module through SPI.

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/799da873-4258-4ff6-a30d-89ece43d4a14)

## Randomization of Values ##

The randomization of values is done through the use of arrays and the random function. The arrays used are as shown:

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/821fb505-618d-43e6-9390-63af96b059b9)

With the use of the for loop and random function, the values in the according arrays can be randomized.

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/a7a9369a-3985-4bd4-a391-915df113da10)

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/eb98602f-aaec-4d83-8686-705723a3e366)

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/312c1a7c-38a7-4491-869a-e393bfba466d)

### Serial Monitor Output: ###

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/c71dda19-2a9e-40ba-81fa-b4ff93afb6cc)

## Transmission of Values ##

The transmission of the randomized values from master to slave through I2C is done through the use of the Wire.h library. The functions used are Wire.beginTransmission(), Wire.write() and Wire.endTransmission().

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/1af5aeae-a868-41d6-97de-dc79833a9344)

### Serial Monitor Output: ###

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/5908ac6d-03ab-4630-918a-6fefe172700b)

## Comparison of Values ##

When one of the slave modules is sensed, it transmits its assigned value to the master which stores it into an array for comparison on the 2nd Update.

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/0c142b14-eba4-43c9-9506-66c8de4d02eb)

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/053b53a4-5853-455d-818f-1ba5955077c9)

### Comparison of Values (1st Update) ###

When one of the slave modules is sensed, it transmits its assigned value to the master which stores it into an array for comparison on the 2nd Update.

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/cab68000-e5c4-4ad7-8485-24f7784c9093)

### Serial Monitor Output ###

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/0542c711-d597-4ee5-9864-631d7f69239d)

### Comparison of Values (2nd Update) ###

Likewise on the second slave module sensed, the value sent to the master is stored into the same compare array which will then be used to compare the two values.

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/56ae156c-b61e-46ba-b9e8-5849d829181f)

### Serial Monitor Output ###

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/95570de8-61d1-43b7-9c9b-6651268ff136)

### Comparison (Matched) ###

The comparison of values is done by adding the values from the 1st and 2nd Updates respectively and dividing them by 2.

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/02bc40da-ee23-49c8-b7a2-79de78879654)

### Serial Monitor Output ###

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/4c009e2a-e768-410f-a559-0279bc526d4a)

### Comparison (Not Matched) ###

In the case where the compared values are different, the value divided will not be equal to value from the 1st Update as such, the if statement is false and the code will simply reset all values to repeat the process again.

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/aec82fc9-3936-4ede-865a-64508aa108e8)

### Serial Monitor Output ###

![image](https://github.com/Acctrina/Arduino-NumberMatchingGame/assets/126780174/94f3327b-ba84-4945-8d2f-1d641d88e725)


















