# Day 1
# Embedded C Concepts I Learned

As part of learning embedded systems and bare-metal programming, I focused on the core C concepts required for hardware-level programming.

## Concepts Learned

### 1. Pointers

Used for accessing hardware registers through memory addresses.

```c 
#define GPIO0_DIR (*(volatile unsigned int*)0x2009C000)
```

Learned:

* Pointer dereferencing
* Memory mapped I/O
* Address handling

### 2. Bitwise Operators
Learned:

* Bit masking
* Register manipulation
* Binary operations

### 3. Functions

```c id="v6d6sw"
void uart_init();
void uart_send_char(char c);
```

Learned:

* Modular programming
* Reusable driver functions

### 4. Arrays & Strings

```c id="n6e4d0"
char buffer[50];
```

Learned:

* Buffers
* `strcmp()`
* `strlen()`
* UART command handling

### 5. Structures (Basics)

Learned how embedded frameworks like CMSIS use structs for peripherals and register organization.
