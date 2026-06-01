# Day 2: UART Initialization and Serial Debugging

## Objective

Learn how to:
- Initialize UART0
- Send data using UART
- Debug programs using a serial terminal

---

## Why Serial Debugging?

Microcontrollers do not have a monitor to display output.

UART allows us to send messages from the LPC1768 to a PC terminal.

Example:

```c
uart_send_string("System Started");
```

Terminal Output:

```text
System Started
```

This helps verify that the program is running correctly.

---

## UART Initialization Steps

### 1. Configure UART Pins

```c
PINSEL0 |= (1<<4);
PINSEL0 |= (1<<6);
```

Configures:
- P0.2 as TXD0
- P0.3 as RXD0

---

### 2. Configure UART Format

```c
U0LCR = 0x83;
```

Sets:
- 8 Data Bits
- No Parity
- 1 Stop Bit (8N1)

---

### 3. Set Baud Rate

Baud rate determines communication speed.

Common value:

```text
9600 bps
```

Meaning UART transfers 9600 bits per second.

---

### 4. Enable UART

After configuring registers, UART is ready for communication.

---

## Sending a Character

```c
while(!(U0LSR & (1<<5)));

U0THR = 'A';
```

Steps:
1. Check if transmitter is ready.
2. Send character.

---

## Sending a String

A string is sent one character at a time.

Example:

```text
HELLO
```

UART sends:

```text
H
E
L
L
O
```

---

## Serial Debugging Flow

```text
LPC1768
   ↓
UART0
   ↓
TX Pin
   ↓
USB-UART Converter
   ↓
PC Terminal
```

---

## Terminal Software

Common serial terminals:

- PuTTY
- Tera Term
- Hercules

These programs display UART messages from the microcontroller.

---

## Debugging Example

Code:

```c
uart_send_string("ADC Initialized");
```

Terminal:

```text
ADC Initialized
```

Sensor Example:

```text
Temperature = 30°C
ADC Value = 742
```

This helps monitor program execution in real time.

---

