# Smart-Exam-Hall-Monitoring-and-Management-System-

LPC2148-based Smart Exam Hall Monitoring and Management System that automates examination timing, RTC-based scheduling, temperature monitoring, countdown management, secure configuration, pause/resume control, and visual and audible alerts, reducing manual intervention and improving exam management efficiency.
## Project Overview

The Smart Exam Hall Monitoring and Management System is an LPC2148 ARM7-based embedded system developed using Embedded C to automate examination timing and monitoring.

The system provides RTC-based time management, configurable examination settings, temperature monitoring, countdown display, password-protected configuration, pause/resume control, percentage-based LED status indication, and buzzer alerts.

The project demonstrates practical implementation of microcontroller interfacing, peripheral control, timers, ADC, RTC, external interrupts, and modular Embedded C programming.

## Objectives

Automate examination timing and countdown management, display current time and room temperature on the LCD, Configure examination start time and duration using a 4×4 keypad, provide password-protected access to configuration settings.Display remaining examination time using multiplexed 7-segment displays.Monitor room temperature using the LM35 sensor,provide percentage-based examination status using Green, Yellow, and Red LEDs.Implement pause and resume functionality using an external interrupt,record examination start and end times using the RTC,provide a buzzer indication during the final stage of the examination and reduce manual timing errors and intervention.

## Hardware Requirements

LPC2148 ARM7 Microcontroller 

16×2 LCD

4×4 Matrix Keypad 

RTC 

LM35 Temperature Sensor 

Two 7-Segment Displays

Green, Yellow & Red Led's

Buzzer

Switches

USB-UART / DB-9 interface

5V DC Power Supply

## Software Requirements

Embedded C

Keil µVision

Flash Magic

LPC2148 / ARM7 Development Environment

## System Block Diagram

<img width="2000" height="1150" alt="image" src="https://github.com/user-attachments/assets/693d9fab-b859-4427-9637-ef3b2a441767" />

## System Working 

#### 1. System Initialization

After power ON, the LPC2148 initializes the required peripherals such as LCD, RTC, keypad, ADC, timer, 7-segment display, LEDs, buzzer, and external interrupts.

#### 2. Normal Monitoring

The system continuously reads the RTC and LM35 sensor.

The LCD displays the current time and room temperature while the system waits for examination configuration or the configured examination start time.

#### 3. Examination Configuration

Switch 1 is used to enter the configuration mode through External Interrupt 0.

The administrator must enter the correct password using the keypad.

After successful authentication, the following settings can be configured:

RTC date and time
Examination start time
Examination duration

#### 4. Examination Start

When the configured examination start time is reached, the system records the examination start time and starts the countdown.

The remaining examination time is displayed on the 7-segment displays.

#### 5. Countdown

The examination countdown is continuously updated according to the configured examination duration.

The LCD continues to display system information while the 7-segment displays provide the remaining examination time.

#### 6. Pause and Resume

Switch 2 is connected to External Interrupt 1.

First press → Countdown pauses.
Second press → Countdown resumes.

The examination continues from the remaining time at which it was paused.

#### 7. Examination Completion

When the countdown reaches zero, the examination end time is recorded using the RTC and the examination completion indication is generated.

### LED and Buzzer Status

The system determines the LED and buzzer status based on the percentage of examination time remaining.

More than 50%: Green LED is ON.

More than 30% and up to 50%: Yellow LED is ON.

More than 10% and up to 30%: Red LED is ON.

More than 0% and up to 10%: Red LED blinks and the buzzer turns ON/OFF repeatedly.

At 0%: All LEDs and the buzzer are turned OFF.

This provides a clear visual and audible indication of the remaining examination time.

## Main Modules

#### 1. LPC2148 Microcontroller

Main controller responsible for coordinating the complete system and controlling all connected peripherals.

#### 2. RTC Module

Handles real-time date and time information and supports examination start and end time recording.

#### 3. LCD Module

Displays time, temperature, configuration messages, and other system information.

#### 4. Keypad Module

Provides password input and examination configuration through the 4×4 matrix keypad.

#### 5. LM35 and ADC Module

The LM35 provides the temperature input, which is processed using the ADC and displayed on the LCD.

#### 6. Timer Module

Handles the examination countdown and timing operations.

#### 7. 7-Segment Module

Displays the remaining examination time using two multiplexed 7-segment displays.

#### 8. External Interrupt Module

Handles configuration access and pause/resume operations.

#### 9. LED and Buzzer Module

Provides visual and audible examination status indications based on the remaining examination percentage.

## Project Workflow

The basic project flow is:
<img width="800" height="1000" alt="image" src="https://github.com/user-attachments/assets/dc1513e7-8b5a-4519-840b-f73e05e1630b" />

## Key Features

RTC-based examination timing

Configurable examination duration

Password-protected configuration

Real-time temperature monitoring

Multiplexed countdown display

Percentage-based LED indication

Final-stage buzzer alert

Interrupt-based pause/resume

Examination start/end time recording

## Embedded C Modules

The firmware can be organized into separate modules for better readability and maintainability.

main.c – Main application and system control

lcd.c / lcd.h – LCD functions

keypad.c / keypad.h – Keypad scanning and input

rtc.c / rtc.h – RTC operations

adc.c / adc.h – ADC and temperature measurement

timer.c / timer.h – Timer and countdown operations

seven_segment.c / seven_segment.h – 7-segment display control

interrupt.c / interrupt.h – External interrupt handling

LED/Buzzer functions – Examination status indication

## Technologies Used

Microcontroller: LPC2148 ARM7

Programming Language: Embedded C

Development IDE: Keil µVision

Programming Tool: Flash Magic

Core Concepts: GPIO, ADC, RTC, Timers, External Interrupts, Peripheral Interfacing

## Applications

Schools and Colleges

Universities

Examination Centers

Training and Certification Centers

Competitive Examination Halls

Computer-Based Examination Environments

## Future Scope

The system can be further enhanced with:

Examination data logging using EEPROM/external memory

PC-based monitoring and report generation

Centralized monitoring of multiple examination halls

Remote monitoring through networking/IoT

Attendance system integration

Additional environmental sensors

Enhanced authentication and security

