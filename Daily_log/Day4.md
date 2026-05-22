

Today I focused on understanding GPIO register-level programming using the LPC1768 ARM Cortex-M3 microcontroller.

## Topics Learned

- GPIO Basics
- Input and Output Pins
- HIGH and LOW logic levels
- LED Control using GPIO
- Memory Mapped GPIO Registers
- Bitwise Register Manipulation
- PINSEL Register Basics
- Reading Register Maps from Datasheets

## LPC1768 GPIO Registers Studied

### FIODIR
Used to configure GPIO pin direction.

- `1` → Output
- `0` → Input

Example:

```c
FIODIR |= (1<<22);
````

Meaning:

* Access FIODIR register
* Set bit 22
* Configure P0.22 as output

---

### FIOSET

Used to set GPIO pin HIGH.

```c
FIOSET = (1<<22);
```

---

### FIOCLR

Used to clear GPIO pin LOW.

```c
FIOCLR = (1<<22);
```

---

### FIOPIN

Used to read current GPIO pin state.

Useful for:

* Button input
* Pin status checking

---

## PINSEL Registers

Learned that LPC1768 pins are multiplexed.

One pin can work as:

* GPIO
* UART
* SPI
* I2C

PINSEL registers are used to select pin functionality.

---

## GPIO Driver Skeleton

### gpio.h

```c
#define FIODIR (*(volatile unsigned int*)0x2009C000)
#define FIOSET (*(volatile unsigned int*)0x2009C018)
#define FIOCLR (*(volatile unsigned int*)0x2009C01C)
```

### gpio.c

```c
void led_init()
{
    FIODIR |= (1<<22);
}

void led_on()
{
    FIOSET = (1<<22);
}

void led_off()
{
    FIOCLR = (1<<22);
}
```

## Key Skills Gained

* Reading peripheral registers from datasheets
* Understanding register addresses
* GPIO direction configuration
* Register-level programming
* Bitwise hardware control
* Basic bare-metal GPIO driver development

````

# notes/gpio-register-notes.md

```markdown id="h9j5kq"
# GPIO Register Notes - LPC1768

## GPIO Basics

GPIO stands for General Purpose Input Output.

GPIO pins can work as:
- Input
- Output

Examples:
- LED control
- Button reading

---

## Important GPIO Registers

### FIODIR
Controls pin direction.

- `1` → Output
- `0` → Input

Example:

```c
FIODIR |= (1<<22);
````

---

### FIOSET

Sets pin HIGH.

```c
FIOSET = (1<<22);
```

---

### FIOCLR

Sets pin LOW.

```c
FIOCLR = (1<<22);
```

---

### FIOPIN

Reads current pin value.

Used for input operations.

---

## PINSEL

Pins in LPC1768 are multiplexed.

A single pin can act as:

* GPIO
* UART
* SPI
* I2C

PINSEL registers select pin functionality.

````

# src/gpio.h

```c id="lx4t8u"
#ifndef GPIO_H
#define GPIO_H

#define FIODIR (*(volatile unsigned int*)0x2009C000)
#define FIOSET (*(volatile unsigned int*)0x2009C018)
#define FIOCLR (*(volatile unsigned int*)0x2009C01C)
#define FIOPIN (*(volatile unsigned int*)0x2009C014)

void led_init(void);
void led_on(void);
void led_off(void);

#endif
````

# src/gpio.c

```c id="8w8r5r"
#include "gpio.h"

void led_init(void)
{
    FIODIR |= (1 << 22);
}

void led_on(void)
{
    FIOSET = (1 << 22);
}

void led_off(void)
{
    FIOCLR = (1 << 22);
}
```
