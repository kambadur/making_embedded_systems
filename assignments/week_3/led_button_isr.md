# Week 3 Exercise: Make Blinky
## NUCLEO F401RE
### Dev board: Hardware block diagram
![](assets/hw_bd_f401re.png)

**1. What build environment are you using?**  
    STM32CubeIDE  
**2. Can you step through the code to see what each line does?**  
    Yes, in debugger perspective of IDE

**3. What are the hardware registers that cause the LED to turn on and off? (From the processor manual, don’t worry about initialization.)**  
   ![GPIOx_MODER](assets/Gpio_Mode_Reg.png)  
   Mode register sets the direction of the pin  
   Set the port pin for Led as Output. (Led is connected to GPIOA Pin 5 on Nucleo F401RE board)  
   Set the port pin for user button as Input. (User button is connected to GPIOC Pin 13 on Nucleo F401RE board)  
   These pins can be accessed via memory mapped IO.  
   To set the mode for the pin to which led is connected, first get its location in the memory map by adding the base address of GPIOA with GPIOx_MODER offset address.  

   Base address of GPIOA:            0x40020000U  
   Offset address of GPIOx_MODER:    0x0U  
   [*The below code snippets are only for understanding. In the assignment, HAL abbstration is used.*]
   
        uint32_t* const pGpioAModeReg = (uint32_t*) (0x40020000U + 0x0U);  
   PA5 (Led) can now be set as output (as shown in the above image of GPIOx_MODER)  

        *pGpioAModeReg |= (1<<10);	//set bit 10  
        *pGpioAModeReg &= ~(1<<11); //clear bit 11  

   Base address of GPIOC:            0x40020800U  
   Offset address of GPIOx_MODER:    0x0U  

        uint32_t* const pGpioCModeReg = (uint32_t*) (0x40020800U + 0x0U);  
   PC13 (button) can now be set as input (as shown in the above image of GPIOx_MODER)  
   
        *pGpioCModeReg &= ~(3<<27); //clear bits 27, 26


   ![GPIOx_ODR](assets/Gpio_Odr_Reg.png)  
   Writing 1/0 to output data register changes the voltage level on the respective pin mapped to it.  
   To turn the Led On, write 1 to GPIOA pin 5 of ODR  
   To turn the Led Off, write 0 to GPIOA pin 5 of ODR  
   Base address of GPIOA:            0x40020000U  
   Offset address of GPIOx_ODR:    0x14U  
   
        uint32_t* const pGpioAOdrReg = (uint32_t*) (0x40020000U + 0x14U);  

        //Set PA5 (turn on led)  
        *pGpioAOdrReg  |= (1<<5);

        //Clear PA5 (turn off led)
        *pGpioAOdrReg  &= ~(1<<5);


**4. What are the registers that you read in order to find out the state of the button?**  
   ![GPIOx_IDR](assets/Gpio_Idr_Reg.png)  
   Other than RESERVED, every bit in the IDR register corresponds to a pin on the MCU.
   Similar to MODE and ODR registers, tha base address of the GPIO port to which the button is connected is needed. Then adding the offset address of the IDR regsiter gives the right location in the memory map. Bit manipulation helps to read the correct bit (pin) of interest.  
   Base address of GPIOC:            0x40020800U  
   Offset address of GPIOx_IDR:    0x10U  

        //GPIOC IDR Reg
        uint32_t volatile * const pGpioCIdrReg = (uint32_t*) (0x40020800U + 0x10U);

        //Read the status of pin PC13.
        uint8_t pinState;
        pinState = (uint8_t ) (*pGpioCIdrReg >> 13) & 1);  


**5. Can you read the register directly and see the button change in a debugger or by printing out the value of the memory at the register’s address?**  
   ![ButtonState_0](assets/Debugger_buttonState_0.png)  

   ![ButtonState_1](assets/Debugger_buttonState_1.png)


### Implementation
#### Add a button to turn the LED on and off. Button causes an interrupt. Debounce the button signal.  
##### **GPIO Configuration for button B1 and LED LD2**  
Interrupt is configured on B1 for both Rising and Falling edjes, to react for both press and release events.  
![STM32CubeIDE_GPIO_B1_Interrupt](assets/STM32CubeIDE_GPIO_B1_Interrupt.png)  

##### **Code generation**  
In Rose: RCC enables clocks to the respective GPIOx peripherals.  
In Red:  GPIO configuration for input button B1 [*macro expansion of Pin_B1 shows that it is defined as (uint16_t) 0x2000, which is bit 13*]  
In Blue: GPIO configuration for output Led  
In Black: EXTI interrupt has to be enabled in NVIC, otherwise interrupts doesn't get through to the Core.  
![STM32CubeIDE_CodeGen_GPIO_B1_Interrupt](assets/STM32CubeIDE_CodeGen_GPIO_B1_Interrupt.png)  

##### **Button ISR Callback and Debouncing Timer**  
![Button_ISRCallback_Debouncing](assets/Button_ISRCallback_Debouncing.png)  

#### **Source file:**   [main.c](assets/main.c)  

#### **Video**
[Blinky](assets/nucleo-f401re_led_button_isr.mp4)
