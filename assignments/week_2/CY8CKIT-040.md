# Week 2 Exercise: Investigate Project Boards
1. Investigate the board intended for your final project. 
2. Investigate the board assigned to you. 

For each board, look at the datasheet and getting started information for the board. 
Draw the hardware block diagram for the board.

## CY8CKIT-040

### Dev board: Hardware block diagram
![](assets/hw_bd_cy8ckit-040.png)


For peripherals, note the communication paths (SPI, I2C, etc).
### Dev board: Peripherals
|Peripheral      |Communication with MCU|
|:-------------|:--------------------------|
|PSoC 5LP Debugger/Programmer|    SWD|
|Reset button|    GPIO|
|Status/Power LEDs|            GPIO|
|F-RAM|   I2C      |
|RGB LED|     PWM          |
|ST MEMS Gyroscope (I3G4250D)|    I2C/SPI|
|2.4" QVGA TFT LCD|       Parallel interface|

Look through the datasheet for the processor and other documents. Answer these questions: 
### Processor related:
* What kind of processor is it? 
    * CY8C4014LQI-422

* How much Flash and RAM does it have? Any other memory types? 
    * 2MB Flash and 256KB RAM
    * 4KB backup SRAM

* Does it have any special peripherals? (List 3-5 that you find interesting.
    * ADC, DAC, CAN, TIMERS, USART, SDIO, SAI, DCMI 

* If it has an ADC, what are the features?
### ADC features
![ADC features](assets/ADC_features.png)
