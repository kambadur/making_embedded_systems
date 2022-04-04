# Week 3 Exercise: Make Blinky
## NUCLEO F401RE
### Dev board: Hardware block diagram
![](assets/hw_bd_f401re.png)

**1. What build environment are you using?**  
    STM32CubeIDE  
**2. Can you step through the code to see what each line does?**  
    Yes, in debugger perspective of IDE

**3. What are the hardware registers that cause the LED to turn on and off? (From the processor manual, don’t worry about initialization.)**  
   ![GPIO_MODEREG](assets/Gpio_Mode_Reg.png)  
   Mode register sets the direction of the pin  
   Set the port pin for Led as Output. (Led is connected to GPIOA Pin 5 on Nucleo F401RE board)  
   Set the port pin for user button as Input. (User button is connected to GPIOC Pin 13 on Nucleo F401RE board)  
   These pins can be accessed via memory mapped IO.  
   To set the mode for the pin to which led is connected, first get its location in the memory map by adding the base address of GPIOA with GPIOx_MODER offset address.  
   Base address of GPIOA:            0x40020000U  
   Offset address of GPIOx_MODER:    0x0U  
        uint32_t* const pGpioAModeReg = (uint32_t*) (0x40020000U + 0x0U);  
   PA5 (Led) can now be set as output (as shown in the abobe image of GPIOx_MODER)  
        *pGpioAModeReg |= (1<<10);	//set bit 10  
        *pGpioAModeReg &= ~(1<<11); 	//clear bit 11  



   ![GPIO_ODRREG](assets/Gpio_Odr_Reg.png)  

**4. What are the registers that you read in order to find out the state of the button?**  
   ![GPIO_IDRREG](assets/Gpio_Idr_Reg.png)  

**5. Can you read the register directly and see the button change in a debugger or by printing out the value of the memory at the register’s address?**  
   ![ButtonState_0](assets/Debugger_buttonState_0.png)  

   ![ButtonState_1](assets/Debugger_buttonState_1.png)


### Implementation
#### Add a button to turn the LED on and off. 
#### Button causes an interrupt. 
#### Debounce the button signal.
