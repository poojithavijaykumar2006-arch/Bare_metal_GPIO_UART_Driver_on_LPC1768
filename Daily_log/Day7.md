# UART Transmitter and Receiver using LPC1768 (GSAS Board)
To implement serial communication using the UART0 peripheral of the LPC1768 microcontroller for transmitting and receiving data between the board and a computer/terminal.

## Components Used Are
* LPC1768 GSAS Development Board
* Keil uVision 

## Project Overview
UART (Universal Asynchronous Receiver Transmitter) is a serial communication protocol used for exchanging data between devices. In this project, UART0 of the LPC1768 is configured to transmit and receive characters.

The transmitter sends characters or strings through the TX pin, while the receiver reads incoming data through the RX pin.

### Code
```c
#include<LPC17xx.h>
#include "uart.h"

void init(void){
	LPC_PINCON->PINSEL0 &= ~((3<<4)|(3<<6));
	LPC_PINCON->PINSEL0 |= ((3<<4)|(3<<6));

	LPC_UART0->LCR = 0x83;

	LPC_UART0->DLL = 163;
	LPC_UART0->DLM = 0;

	LPC_UARTO->LCR = 0x03;
}

void TXchar( char c)
{
	while(!(LPC_UART0->LSR & (1<<5)));
	LPC_UART0->THR = c;
}

void TXstring(char *str)
{
	while(*str)
	{
		TXchar(*str++)
	}
}

void RX(void)
{
	while(!(LPC_UART0->LSR & (1<<0)));
	return LPC_UART0->RBR;
}
````
## Working Principle

#### UART Initialization (init())
* Configures P0.2 as UART0_TXD.
* Configures P0.3 as UART0_RXD.
* Enables access to baud rate registers using LCR.
* Sets baud rate using DLL and DLM registers.
* Configures UART communication parameters.
#### Character Transmission (TXchar())
* Waits until the transmit holding register becomes empty.
* Loads a character into the THR register.
* UART hardware serially transmits the character.
#### String Transmission (TXstring())
* Sends characters one by one until the null character ('\0') is encountered.
* Useful for transmitting messages.
#### Character Reception (RX())
* Waits until data is received.
* Reads the received character from the Receive Buffer Register (RBR).
* Returns the received character to the program

## UART Register Used

| Register | Purpose                                       |
| -------- | --------------------------------------------- |
| PINSEL0  | Selects UART function for pins P0.2 and P0.3  |
| LCR      | Configures UART settings and baud rate access |
| DLL      | Baud rate divisor low byte                    |
| DLM      | Baud rate divisor high byte                   |
| THR      | Holds data to be transmitted                  |
| RBR      | Stores received data                          |
| LSR      | Indicates transmitter and receiver status     |

### UART Driver Debug Output

![UART Debug](images\uart_driver_ouput.jpeg)
