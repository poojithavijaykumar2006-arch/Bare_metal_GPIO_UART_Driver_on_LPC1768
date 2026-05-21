
# ARM Cortex-M3 & LPC1768 Basics

As part of my embedded systems learning, I explored the architecture and internal working of the ARM Cortex-M3 processor and the NXP LPC1768 microcontroller.

---

# ARM Cortex-M3 Basics

ARM Cortex-M3 is a 32-bit processor widely used in embedded systems for efficient and low-power applications.

## Concepts Learned

### Registers
The processor uses registers for fast data storage and execution.

Important registers:
- `R0 - R12` → General purpose registers
- `SP` → Stack Pointer
- `LR` → Link Register
- `PC` → Program Counter

### Stack
The stack stores temporary data such as:
- Function variables
- Return addresses
- Function call data

Function calls internally use:
- `PUSH`
- `POP`

operations for stack management.

### Program Counter (PC)
The Program Counter stores the address of the next instruction to execute.

It helps the processor track program execution flow.

### NVIC (Nested Vector Interrupt Controller)
NVIC handles interrupts in Cortex-M3.

It allows peripherals like UART, Timers, and GPIO to interrupt the CPU when required.

### Vector Table
The vector table maps interrupts to their corresponding ISR (Interrupt Service Routine).

Example:

```c
UART Interrupt → uart_handler()
````

### Thumb-2 Instruction Set

Cortex-M3 uses the Thumb-2 instruction set for efficient and compact instruction execution.

---

# LPC1768 Architecture Basics

The LPC1768 is an ARM Cortex-M3 based microcontroller from NXP.

## Clock System Understanding

The clock flow inside LPC1768:

```text
Internal Oscillator
        ↓
       PLL
        ↓
Peripheral Clocks
```

### Internal Oscillator

Generates the initial clock signal inside the microcontroller.

### PLL (Phase Locked Loop)

Used to increase clock frequency for faster processor operation.

### Peripheral Clocks

Distributes clock signals to peripherals like:

* GPIO
* UART
* Timers

---

# Important LPC1768 Peripherals Learned

### GPIO

Used for controlling LEDs, switches, and digital input/output pins.

### UART

Used for serial communication.

### Timer

Used for delays, counting, and timing operations.

### NVIC

Handles interrupts from peripherals.

### PLL

Controls system clock frequency.

### PINSEL

Used for configuring pin functions.

Example:

* GPIO function
* UART function
* SPI function

---

# Key Takeaways

* ARM Cortex-M3 Architecture Basics
* Register Understanding
* Stack and Function Calls
* Interrupt Handling using NVIC
* Vector Table Basics
* Thumb-2 Instruction Set
* LPC1768 Clock System
* Peripheral Configuration
* Embedded System Architecture Fundamentals

