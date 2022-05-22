# STME32Fx Microcontroller Custom Bootloader Development

---

## About this Upskilling Process

To learn about Bootloader working method and process inside MCU, to write my own custom bootloader for STM32Fx microcontroller and to test it's operations. To implementation Bootloader Communication. To know about Custom Bootloader command packets and different boot modes of the STM32 microcontroller.

And to know about Boot loader:

- Flash handling implementation (Sector Erase/Program/Mass erase)
- Options bytes(OB) Program handling implementation
- Flash sector protection status handling implementation
- In application programming implementation (IAP)
- Vector table relocation of ARM cortex Mx processor

---

## The Logical Phase of the Whole Process

- **About Bootloader**
- **MCU memory, Reset Sequence and Boot configs**
- **Exploring STM32 Native Bootloader**
- **Custom Bootloader Communication with Host**
- **Boot-Loader :**
  - Project Creation
  - UART Testing
  - Jumping to User Code
  - Read Commands from Host
- Implementing :
  - BL_GET_VER_CMD
  - BL_GET-HELP_CMD
  - BL_GET_CID_CMD
  - BL_GET_RDP_LEVEL_CMD
  - BL_GET_GO_TO_ADDR_CMD
  - BL_FLASH_ERASE_CMD
  - BL_MEM_WRITE_CMD
- **Options Bytes and Flash Sector protection**
- **Exploring Host Application**

---

> ***Let's Begin the Journey***

## Bootloader and Development Keywords

- In-Circuit Debugger/Programmer (ICDP)
- In Application Programming
- In System Programming
  
  
---

## *About Bootloader*

> ***Bootloader***
> A Bootloader is nothing but a small piece of code stored in the MCU flash or ROM to act as an application loader as well as a mechanism to update the applications whenever required.

