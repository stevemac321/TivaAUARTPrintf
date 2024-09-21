
# Tiva C Series UART Project with `UARTprintf`

## Overview

This project demonstrates how to set up UART0 on the Tiva C Series microcontroller for basic serial communication using the `UARTprintf` function provided in the TivaWare library. This example prints formatted strings via the UART, similar to how `printf` works in a standard C environment.

## Files

- **main.c**: The main C file that initializes UART0 and continuously prints data using `UARTprintf`.
- **uartstdio.c**: A source file from the TivaWare `utils` library that provides the `UARTprintf` functionality. This file must be included in the project for proper UART string handling.
- **uartstdio.h**: The header file from TivaWare's `utils` directory, which is necessary for using `UARTprintf`.

## Setup

1. Ensure that you have installed TivaWare:
   - Download from [Texas Instruments](https://www.ti.com/tool/SW-TM4C).
   - The TivaWare directory should be added to your include paths.

2. Add the following source and header files from TivaWare's `utils` folder:
   - `C:\ti\TivaWare_C_Series-2.2.0.295\utils\uartstdio.c`
   - `C:\ti\TivaWare_C_Series-2.2.0.295\utils\uartstdio.h`

3. Ensure you configure the include paths in Code Composer Studio to point to the TivaWare directories.

## Configuration

### UART Initialization

The UART0 module is initialized at a baud rate of 115200 using the `UARTStdioConfig()` function, and then it continuously prints messages using `UARTprintf()`. You can modify this for different baud rates or UART modules as needed.

Here’s an example of UART initialization:

```c
void UART_Init(void) {
    // Enable UART0 and GPIOA peripherals
    SysCtlPeripheralEnable(SYSCTL_PERIPH_UART0);
    SysCtlPeripheralEnable(SYSCTL_PERIPH_GPIOA);

    // Configure GPIO for UART0 (PA0 and PA1)
    GPIOPinConfigure(GPIO_PA0_U0RX);
    GPIOPinConfigure(GPIO_PA1_U0TX);
    GPIOPinTypeUART(GPIO_PORTA_BASE, GPIO_PIN_0 | GPIO_PIN_1);

    // Configure UART0 with 115200 baud rate
    UARTStdioConfig(0, 115200, SysCtlClockGet());
}
```

### Main Loop

In the main loop, `UARTprintf` is used to send formatted text over UART:

```c
int main(void) {
    // Initialize UART0
    UART_Init();

    while(1) {
        UARTprintf("UART0 is working! Counter: %d\n", counter++);
        SysCtlDelay(5000000);  // Simple delay
    }
}
```

This will continuously print a counter to the terminal.

## Running the Project

1. Connect the Tiva C Series LaunchPad to your computer via USB.
2. Open the serial terminal (e.g., PuTTY, Tera Term) and configure it for:
   - **115200 baud rate**
   - **8 data bits**
   - **No parity**
   - **1 stop bit**
3. Flash the program to the Tiva C LaunchPad.
4. Observe the output in the terminal.

## License

This project is released under the GPL Version 2 License. See [LICENSE](LICENSE) for details.

