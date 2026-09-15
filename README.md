# Smart-Exam-Hall-Monitoring-and-Management-System-

LPC2148-based Smart Exam Hall Monitoring and Management System that automates examination timing, RTC-based scheduling, temperature monitoring, countdown management, secure configuration, pause/resume control, and visual and audible alerts, reducing manual intervention and improving exam management efficiency.
## Project Overview

The Smart Exam Hall Monitoring and Management System is an LPC2148 ARM7-based embedded system developed using Embedded C to automate examination timing and monitoring. The system provides RTC-based time management, configurable examination settings, temperature monitoring, countdown display, password-protected configuration, pause/resume control, percentage-based LED status indication, and buzzer alerts. The project demonstrates practical implementation of microcontroller interfacing, peripheral control, timers, ADC, RTC, external interrupts, and modular Embedded C programming.

## Features

- **RTC-Based Examination Timing** : Accurate start-time and countdown management.
- **Password-Protected Configuration** : Secure access to examination settings.
- **Real-Time Temperature Monitoring** : LM35-based room temperature monitoring.
- **Multiplexed Countdown & LED Indication** : Remaining time displayed with percentage-based Green, Yellow, and Red status LEDs.
- **Pause/Resume with Buzzer Alert** : Interrupt-based timer control with a buzzer alert during the final stage.

## Hardware Requirements

- LPC2148 ARM7 Microcontroller
- 16×2 LCD
- 4×4 Matrix Keypad
- RTC
- LM35 Temperature Sensor
- Two 7-Segment Displays
- Green, Yellow & Red LEDs
- Buzzer
- Switches
- USB-UART / DB-9 Interface
- 5V DC Power Supply

## System Block Diagram
<img width="2000" height="1150" alt="image" src="https://github.com/user-attachments/assets/693d9fab-b859-4427-9637-ef3b2a441767" />

## Pin Configuration
| Signal           | Pin                | Description          |
| ---------------- | ------------------ | -------------------- |
| LCD Data         | P0.8 – P0.15       | 8-bit data           |
| LCD RS / EN      | P0.16 / P0.17      | LCD control          |
| Keypad           | P1.16 – P1.23      | 4×4 key input        |
| 7-Segment Data   | P1.24 – P1.31      | Segment data         |
| 7-Segment Select | P0.20 / P0.21      | Digit 1 / Digit 2    |
| Status LEDs      | P0.2 / P0.3 / P0.4 | Green / Yellow / Red |
| Pause LED        | P0.25              | Pause indication     |
| Buzzer           | P0.23              | Final-stage alert    |
| LM35             | P0.28              | Temperature input    |
| Interrupts       | P0.1 / P0.7        | Admin / Pause-Resume | 

## System Architecture

The firmware is organized into modular source and header files, with each module handling a specific system function.
```
├── main_pro.c              # Main program and system initialization
├── interrupt_p.c/h         # External interrupt handling
├── rtc_mpt.c/h             # RTC initialization and operation
├── rtc_edit.c              # RTC configuration
├── kpm_mp.c/h              # 4×4 keypad scanning and input handling
├── lcd_t.c/h               # LCD driver
├── lcd_defines_t.h         # LCD definitions
├── adc_mpt.c/h             # ADC driver
├── adc_defines_mpt.h       # ADC definitions
├── lm35_mpt.c/h            # LM35 temperature measurement
├── led_mpt.c/h             # LED status control
├── buzzer_mpt.c/h          # Buzzer control
├── 7seg_mpt.c/h            # Multiplexed 7-segment display
├── timer.c/h               # Countdown timer control
├── delay.c/h               # Delay routines
├── types_t.h               # Type definitions
└── defines.h               # Common bit definitions and macros
```
## System Working

#### 1. System Initialization
After power ON, the LPC2148 initializes the required peripherals such as LCD, RTC, keypad, ADC, timer, 7-segment display, LEDs, buzzer, and external interrupts.

#### 2. Normal Monitoring
The system continuously reads the RTC and LM35 sensor.
The LCD displays the current time and room temperature while the system waits for examination configuration or the configured examination start time.

#### 3. Examination Configuration
Switch 1 is used to enter configuration mode through External Interrupt 0.
The administrator must enter the correct password using the keypad.
After successful authentication, the following settings can be configured:
-RTC date and time
-Examination start time
-Examination duration

#### 4. Examination Start
When the configured examination start time is reached, the examination countdown begins.
The remaining examination time is displayed on the multiplexed 2-digit 7-segment display.

#### 5. Countdown
The examination countdown is continuously updated according to the configured examination duration.
The LCD continues to display system information while the 7-segment display provides the remaining examination time.

#### 6. Pause and Resume
Switch 2 is connected to External Interrupt 1.
-First press → Countdown pauses.
-Second press → Countdown resumes.
The examination continues from the remaining time at which it was paused.

#### 7. Examination Completion
When the countdown reaches zero, the LEDs and buzzer are turned OFF and the examination is completed.
LED and Buzzer Status
The LED and buzzer status is determined based on the percentage of examination time remaining.

-More than 50%: Green LED ON

-More than 30% and up to 50%: Yellow LED ON

-More than 10% and up to 30%: Red LED ON

-More than 0% and up to 10%: Red LED blinks and buzzer operates intermittently

-0%: All LEDs and buzzer OFF

This provides a clear visual and audible indication of the remaining examination time.

## Project Workflow

The basic project flow is:
```
Power ON
   ↓
Initialize LPC2148 Peripherals
   ↓
Display RTC Time & Temperature
   ↓
Normal Monitoring
   ↓
External Interrupt 0
   ↓
Enter Password
   ↓
Password Correct?
   ├── No → Wrong Password → Normal Monitoring
   │
   └── Yes → Access Granted
              ↓
       Set RTC Date & Time
              ↓
       Set Exam Start Time & Duration
              ↓
       Wait for Start Time
              ↓
       Examination Starts
              ↓
       Start Countdown
              ↓
       Display Remaining Time
              ↓
       LED Status Based on Time %
              ↓
       Pause / Resume if Required
              ↓
       Countdown Reaches Zero
              ↓
       Buzzer & LEDs OFF
              ↓
       Examination Complete
```
## Development Tools & Environment

- **Microcontroller**: LPC2148 ARM7
- **Programming Language**: Embedded C
- **Development IDE**: Keil µVision
- **Programming Tool**: Flash Magic
- **Core Concepts**: GPIO, ADC, RTC, Timers, External Interrupts, Peripheral Interfacing

## Future Enhancements

The system can be further enhanced with:

- Examination Data Logging 
- PC-Based Monitoring & Reporting 
- Multi-Hall Monitoring 
- IoT-Based Remote Monitoring 
- Enhanced Security & Attendance 
