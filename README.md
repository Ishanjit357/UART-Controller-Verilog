# UART Controller using Verilog HDL

## Overview

This project implements a UART (Universal Asynchronous Receiver/Transmitter) controller using Verilog HDL. It supports serial data transmission and reception using the UART 8-N-1 communication format.

The design consists of a UART transmitter, UART receiver, and a top-level controller module. A testbench is provided to verify communication by transmitting data and checking the received output.

## Features

- UART serial transmission and reception
- 8-bit data format
- 1 start bit and 1 stop bit (8-N-1)
- No parity bit
- Parameterized clock cycles per bit
- Separate transmitter and receiver modules
- Testbench for functional simulation
- Loopback testing to compare transmitted and received data

## Tools and Technologies

- **HDL:** Verilog
- **Design and Simulation:** AMD Vivado
- **Verification:** Verilog testbench
- **Target FPGA:** [Add your FPGA board, if applicable]

## Project Structure

```text
UART-Controller-Verilog/
├── uart_tx.v
├── uart_rx.v
├── uart_controller.v
├── tb_uart_controller.v
└── README.md
```

## Design Architecture

```text
       Parallel Data Input
               |
               v
        +--------------+
        |  UART TX     |
        +--------------+
               |
          Serial TX
               |
               v
        +--------------+
        |  UART RX     |
        +--------------+
               |
               v
       Parallel Data Output
```

The transmitter converts parallel data into a serial bitstream. The receiver detects the start bit, samples the incoming data bits, and reconstructs the received byte.

## UART Configuration

| Parameter | Value |
|---|---|
| Data bits | 8 |
| Start bits | 1 |
| Stop bits | 1 |
| Parity | None |
| Baud rate | 9600 baud, when configured for a 100 MHz clock |
| Clock cycles per bit | 10417 for 100 MHz / 9600 baud |

The testbench uses a smaller `CLKS_PER_BIT` value to reduce simulation time. Ensure the parameter is configured consistently for the transmitter, receiver, and testbench.

## Testbench

The testbench checks UART loopback communication using the following data patterns:

- `8'hA5`
- `8'h3C`
- `8'h00`
- `8'hFF`

The received data should match the transmitted data for each test case.

**Simulation status:** [Update after running the testbench in Vivado.]

## How to Run in Vivado

1. Open AMD Vivado and create a new RTL project.
2. Add `uart_tx.v`, `uart_rx.v`, and `uart_controller.v` as design sources.
3. Add `tb_uart_controller.v` as a simulation source.
4. Set `tb_uart_controller` as the simulation top module.
5. Run **Behavioral Simulation**.
6. Inspect the serial transmit signal, receive signal, data output, and valid/status signals in the waveform.
7. Check that the received bytes match the transmitted bytes.

## Learning Outcomes

- Understanding UART serial communication
- Designing finite-state machines for digital communication
- Implementing serial-to-parallel and parallel-to-serial conversion
- Using parameterized RTL for baud-rate timing
- Writing testbenches and inspecting simulation waveforms in Vivado

## Future Improvements

- Add parity-bit support
- Add configurable baud-rate selection
- Improve error detection for framing errors
- Integrate the design with an FPGA development board and USB-to-UART interface

## Author

**[Your Name]**  
M.Tech, Communication and Signal Processing  
Indian Institute of Technology Indore

## License

This project is available for educational and learning purposes. Add a license file if you want to specify reuse and distribution terms.
