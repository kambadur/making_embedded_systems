# Week 2 Exercise: Investigate Project Boards
1. Investigate the board intended for your final project. 
2. Investigate the board assigned to you. 

For each board, look at the datasheet and getting started information for the board. 
Draw the hardware block diagram for the board.

![Dev board: Hardware block diagram](assets/hw_bd_stm32f4discovery.png)


For peripherals, note the communication paths (SPI, I2C, etc).
|Peripheral      |Communication with MCU|
|:-------------|:--------------------------|
|Embedded ST-LINK/V2-B|    JTAG|
|Push buttons (B1, B2)|    GPIO|
|LEDs|            GPIO|
|SDRAM|         |
|USB- OTG|               |
|ST MEMS Gyroscope (I3G4250D)|    I2C/SPI|
|2.4" QVGA TFT LCD|       Parallel interface|

Look through the datasheet for the processor and other documents. Answer these questions: 

* What kind of processor is it? 
STM32F429ZIT6

* How much Flash and RAM does it have? Any other memory types? 
2MB Flash and 256KB RAM
4KB backup SRAM

* Does it have any special peripherals? (List 3-5 that you find interesting.
ADC, DAC, CAN, TIMERS, USART, SDIO, SAI, DCMI 

* If it has an ADC, what are the features? 
![ADC features](assets/ADC_features.png)
