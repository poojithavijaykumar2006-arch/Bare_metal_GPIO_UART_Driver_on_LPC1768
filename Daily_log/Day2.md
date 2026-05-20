 
# Memory Mapped I/O in Embedded Systems

Memory Mapped I/O is one of the most important concepts in embedded systems and bare-metal programming.

In microcontrollers, peripherals such as GPIO, UART, Timers, ADC, SPI, and I2C are connected to fixed memory addresses.  
The CPU communicates with these peripherals by reading from and writing to their corresponding hardware registers.

Instead of accessing normal variables, embedded systems directly interact with hardware using memory addresses and pointers.

Example:

```c
#define GPIO0_DIR (*(volatile unsigned int*)0x2009C000)
````

The above statement accesses a GPIO hardware register located at a fixed memory address.

## What I Learned

* Memory Mapped I/O fundamentals
* Hardware Register Access
* Pointer Casting and Dereferencing
* Register-Level Programming
* Direct Hardware Control using Embedded C
* Importance of `volatile`
* Bitwise Operations for Register Manipulation
* Low-Level Communication between CPU and Hardware

## Important Concepts

### Peripheral

A hardware module inside the microcontroller used for specific tasks.

Examples:

* GPIO
* UART
* ADC
* Timers

### Register

A small memory location inside hardware used to configure or control peripherals.

### Pointer

A variable that stores a memory address.

### volatile

A keyword that prevents the compiler from optimizing hardware register access.

## Key Understanding

```c
*(volatile unsigned int*)address = value;
```

This means:

> “Access the hardware register located at this address and control the connected peripheral.”

## Outcome

Through this concept, I understood how software directly interacts with hardware in embedded systems using Embedded C and register-level programming.

