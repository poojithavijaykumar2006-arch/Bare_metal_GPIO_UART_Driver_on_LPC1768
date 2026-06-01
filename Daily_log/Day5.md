# Day 1: LPC1768 UART and PINSEL

## UART Basics

UART (Universal Asynchronous Receiver Transmitter) is used for serial communication between devices.

It uses:
- TX (Transmit)
- RX (Receive)
- GND

Think of UART like sending and receiving messages:
- TX sends data
- RX receives data

---

## Why PINSEL is Required

LPC1768 pins can perform multiple functions.

Example:

| Pin | Functions |
|------|-----------|
| P0.2 | GPIO / TXD0 |
| P0.3 | GPIO / RXD0 |

PINSEL selects which function the pin should perform.

```c
PINSEL0 |= (1<<4);
PINSEL0 |= (1<<6);
```

This configures:
- P0.2 as TXD0
- P0.3 as RXD0

---

## Important UART Registers

### U0THR
Transmit Holding Register.

```c
U0THR = 'A';
```

Sends character 'A'.

### U0RBR
Receiver Buffer Register.

```c
char c = U0RBR;
```

Reads received data.

### U0LSR
Line Status Register.

```c
U0LSR & (1<<5)
```

Checks if transmitter is ready.

```c
U0LSR & 1
```

Checks if data is received.

### U0LCR
Line Control Register.

```c
U0LCR = 0x83;
```

Configures UART for 8-bit data, no parity, and 1 stop bit (8N1).

---

## UART Data Flow

```text
CPU
 ↓
U0THR
 ↓
UART Hardware
 ↓
TX Pin
 ↓
RX Pin
 ↓
U0RBR
 ↓
CPU
```

---

## Key Points

- UART enables serial communication.
- PINSEL selects UART function on pins.
- U0THR sends data.
- U0RBR receives data.
- U0LSR checks UART status.
- U0LCR configures UART settings.
