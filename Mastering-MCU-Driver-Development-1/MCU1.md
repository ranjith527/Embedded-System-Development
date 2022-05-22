# *Mastering Microcontroller and Embedded Driver Development*

## About this Upskilling Process

To Learn about bare metal driver development using Embedded C and Writing drivers for STM32 GPIO, SPI, I2C, USART from scratch

## My Personal Expectation from this Work

``` text
To Learn, to understand the working of MUC's internal working process, it's the Architecture of the MCU and Building the Drivers, implementing various applications based on this in real world applications.
```

*To Work through this process I need to Sub divide the whole process into Logical pieces and Working on those thing on a Logical pattern to understand them better.*

## The Logical Phase of the Whole Processor

- **Phase-1 Microcontroller Architecture Understanding**:
  - Embedded Code Debugging
  - Understanding MCU Memory Map
  - MCU Bus Interface
  - Understanding MCU Clock tree
  - Understanding Vector table
  - Understanding MCU Interrupt Design, NVIC, Interrupt handling
  - Importance of "Volatile" Keyword

- **Phase-2 GPIO Driver Development**:[^1]
  - GPIO Concepts
  - GPIO Registers
  - GPIO Alternate functionality register
  - GPIO peripheral clock control
  - GPIO Driver Development overview
  - Structuring peripheral registers
  - Writing clock enable and disable macros
  - GPIO driver API requirements and handle structure
  - GPIO driver API Implementation
    - Clock control
    - GPIO init and de-init
    - GPIO data read and write
  - GPIO Interrupt Configuration
  - MCU I/O Pin specifications
  
- **Phase-3 SPI Driver Development**:[^2]
  - SPI Introduction and Bus Details
  - SPI bus configuration and functional block diagram
  - STM32 NSS pin settings and management
  - SPI CPOL and CPHA discussion
  - SPI serial clock discussion
  - SPI Driver: API requirements and configuration structure
  - SPI Driver API Implementation
    - Clock Control
    - SPI init
    - Send Data
    - Receive Data
  - SPI Interrupt
  - SPI Interrupt mode
  - SPI Driver API: IRQ handling
  - Common problems in SPI
  
- **Phase-4 I2C Driver development**:
  - I2C Introduction and I2C signals
  - I2C modes
  - Understanding I2C protocal
  - I2C master and slave communication
  - STM32 I2C functional block diagram
  - I2C Driver API Implementation
    - API Requirements and config structure
    - I2C serial clock discussion(SCLK)
    - I2C Init
    - I2C Master send data
    - I2C pull up resistance, rise time and bus capacitance
  - I2C Interrupts and IRQ numbers
  - I2C Interrupts based adipiscing
  - I2C IRQ handler implementation
  - I2C slave programming
  - Common problems in I2C


- **Phase-5 USART Driver Development**:
  - USART Essentials
  - USART functional block and Peripheral Clock
  - USART Communication
  - USART Driver API Implementation
  - USART oversampling and baudrate
  - USART Interrupts

- **Phase-6 Conclusion about the Learning Experience**

---

> ***Let's Begin the Journey***


## Phase-2 GPIO Driver Development

### GPIO Keywords

``` markdown
  - GPIO (General Purpose Input Output)
  - GPIO Pin
  - GPIO Port
  - Output Buffer
  - Input Buffer
  - Enable Line
  - PMOS and NMOS Transistor
  - Higher and Lowe Potential
  - Floating state
  - Pullup and Pulldown state
  - internal Pullup and Pulldown
  - HI-Z state
  - Open Drain
  - Input and Output Mode
  - Internal pull up and pull down resistor

```

### GPIO Concepts

- GPIO ports is collection of some fixed number of IO pins
- GPIO ports of different microcontrollers has different IO pins (STM32 has 16 IO Pins for single port)
- GPIO pins has two buffers along with enable line:
  - Output Buffer
  - Input Buffer
  - Enable Line

``` text
- When the enable line is 0, the Output buffer will get activated and input buffer will get diactivated.
- A Buffer is a connection of two CMOS transistor of PMOS and NMOS, which provides the higher potential and lower potential to the drain.     
```

- GPIO input mode with high impedence state
  - it's also called HI-Z state
  - it's about keeping the pin floating by not connecting to lower or higher potential.
  - keeping the pin in a floating state can lead to leakage current which may lead to higher powe consumption.
- GPIO input mode with pullup or pulldown state
  - By activating pullup or pulldown to the pin the floating state can be avoided.

``` text
It's always safe to always to keep unused GPIO pins in either position of pullup or pulldown state so that they are reluctant to voltage fluctuation.
```

- GPIO output mode with open drain state
  - In open drain configuration the PMOS transistor simply not present
  - so when the transistor is switched ON the drain will be pulled low and if its OFF the drain will be in floating state
  - so it can only pull down the pin and can't able to pull up resistor
  - So to slove the floating state we need to activate internal pullup resistor
- GPIO Mode with Push-Pull Configuration
  - Here the Output will be pulled actively between high and low by using these two transistors
  - The top transistor is PMOS and bottom transistor is NMOS transistor
- Optimizing the I/O Power Consumption
  - When the input pin is connected with pullup or pulldown state, there won't be any close loop path between the PMOS and NMOS transistor, so the higher potential won't reach the ground, so there won't any current leakage
  - But in the case of floting state the input pin will toggle between high and low of about 50 or 70% between 0.5 V to 0.3 V which leads to leakage current
  - In all Modern MCU, I/O pins use Schmitt trigger to combat the noise issues!!
  
### GPIO Registors
