# Week 3 Exercise: Make Blinky
## NUCLEO F401RE
### Dev board: Hardware block diagram
![](assets/hw_bd_f401re.png)

**1. What build environment are you using?**
   1. STM32CubeIDE
**2. Can you step through the code to see what each line does?**
   1. Yes, in debugger perspective of IDE

Investigate further, using the processor manual:  
**3. What are the hardware registers that cause the LED to turn on and off? (From the processor manual, don’t worry about initialization.)**  
   ![GPIO_MODEREG](assets/Gpio_Mode_Reg.png)  
   ![GPIO_ODRREG](assets/Gpio_Odr_Reg.png)  
**4. What are the registers that you read in order to find out the state of the button?**  
   ![GPIO_IDRREG](assets/Gpio_Idr_Reg.png)  
**5. Can you read the register directly and see the button change in a debugger or by printing out the value of the memory at the register’s address?**  
   ![ButtonState_0](assets/Debugger_buttonState_0.png)  
   ![ButtonState_1](assets/Debugger_buttonState_1.png)


For peripherals, note the communication paths (SPI, I2C, etc).
### Dev board: Peripherals
|Peripheral      |Communication with MCU|
|:-------------|:--------------------------|
|PSoC 5LP Debugger/Programmer|    SWD|
|Reset button|    GPIO|
|Status/Power LEDs|            GPIO|
|F-RAM (256 KB)|   I2C      |
|RGB LED|     GPIO          |

Look through the datasheet for the processor and other documents. Answer these questions: 
### Processor related:
* What kind of processor is it? 
    * CY8C4014LQI-422

* How much Flash and RAM does it have? Any other memory types? 
    * 16 KB of flash
    * 2 KB of SRAM
    * 4 KB of SROM (A supervisory ROM that contains boot and configuration routines
        is provided.)

* Does it have any special peripherals? (List 3-5 that you find interesting).
    * FRAM, PSoC 5LP debugger/Programmer, RGB Led, Proximity header

* If it has an ADC, what are the features?
### ADC
##### General Description:
The CSD Hardware ADC component repurposes the CAPSENSE™ CSD hardware to perform voltage measurements. At its core, the CSD hardware operates as a current sensing circuit. A 1 MΩ resistor placed in series with the input converts an input voltage signal into a small current which is measured by the CSD hardware. The input voltage is calculated from this measured current and reported through an Application Programming Interface (API).  
##### ADC Features
* 0 to 5 volt input range
* Results provided in mV
* End of Conversion (EOC) terminal provided for an optional interrupt

The CSD_ADC can be used in any application to monitor external voltages from batteries, sensors, and transducers. This component is best suited for low-frequency (< 50 Hz) applications due to its low sampling rate.  
Note: The CSD_ADC component uses resources from the PSoC 4 CapSense CSD block. Therefore, the CSD_ADC cannot be used in applications that also require capacitive sensing.  
[Courtesy: Infineon](https://www.infineon.com/cms/en/design-support/tools/sdk/psoc-software/psoc-4-components/psoc-4-voltage-adc-using-csd-hardware-csd-adc-version-1.0/?utm_source=cypress&utm_medium=referral&utm_campaign=202110_globe_en_all_integration-component_datasheet)

##### Board cost
CY8CKIT-040: **$28.12** (Digikey).  
**Stock available at various vendors around.**

##### Processor cost
USB to Serial processor ((CY8C5868LTI-LP039)): **$24.31** (Digikey).  
Main core (CY8C4014LQI-422): **$3.03** (Digikey).  
**Both the processors are out of stock all over.**

##### Application Note:
[PSoc4 ADC using CSD Hardware](https://www.infineon.com/dgdl/Infineon-csd_adc_component_datasheet_1.0-Software%20Module%20Datasheets-v01_00-EN.pdf?fileId=8ac78c8c7d0d8da4017d0eb1e1dd2aed)