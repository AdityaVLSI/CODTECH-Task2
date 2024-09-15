Name : Aditya Singh 

Company: CODTECH IT SOLUTIONS

ID: CT08DS7686

Domain: VLSI 

Duraion: AUGUST TO SEPTEMBER 2024

Mentor: Neela Santhosh Kumar 


## Overview Of The Project ##

# Project : UART (UNIVERSAL ASYNCHRONOUS RECEIVER-TRANSMITTER) DESIGN 

  ## Objective ##

The objective of designing a UART (Universal Asynchronous Receiver-Transmitter) is to facilitate serial communication between devices by converting data from parallel to serial form for transmission, and from serial to parallel form for reception. Specifically, the goals are:
1. Data Transmission  : Convert parallel data from a system bus into serial form to send over a communication channel.
2. Data Reception: Convert serial data received over a communication channel back into parallel form.
3. Asynchronous Communication: Ensure that data transmission occurs without the need for a shared clock between the transmitter and receiver.
4. Baud Rate Control: Maintain a consistent data transmission speed, defined by the baud rate, to synchronize communication.
5. Error Detection: Implement error-checking mechanisms like parity bits to detect data transmission errors.
6. Flow Control: Optionally, manage the flow of data to prevent buffer overflows and ensure proper data handling.
This makes UART a critical component for enabling reliable communication in embedded systems, FPGAs, microcontrollers, and other digital circuits.

## Key Activities ##

The key activities of a UART (Universal Asynchronous Receiver-Transmitter) can be categorized into two main processes: data transmission and data reception. Each of these has specific tasks:

## 1. Data Transmission ##

Parallel-to-Serial Conversion: The UART takes data from the system's data bus (in parallel format) and converts it into a serial stream for transmission.

Start Bit Generation: A start bit is added to indicate the beginning of data transmission.

Data Bit Transmission: The UART transmits the data bits (typically 8 or 9 bits).

Parity Bit (Optional): If enabled, the UART adds a parity bit for error checking.

Stop Bit Generation: A stop bit is added to signal the end of the data frame.

Baud Rate Control: The transmission is controlled by a baud rate generator, which defines the speed at which bits are transmitted.


## 2. Data Reception ##

Serial-to-Parallel Conversion: The UART receives the serial data stream and converts it into parallel form.

Start Bit Detection: The UART detects the start bit to identify the beginning of a data frame.

Data Bit Reception: The UART reads the data bits and stores them.

Parity Check (Optional): If parity is used, the UART performs an error check using the parity bit.

Stop Bit Detection: The stop bit is checked to verify the end of the data frame.

Error Handling: The UART may handle errors such as framing errors, parity errors, or overrun errors.


## 3. Baud Rate Generation ##

The UART manages timing for both transmission and reception through a baud rate generator, ensuring the data is synchronized between sender and receiver despite operating asynchronously.


## 4. Flow Control (Optional) ##

UART can implement flow control mechanisms (e.g., hardware flow control using RTS/CTS or software flow control using XON/XOFF) to ensure data is not lost during transmission, especially when buffers are full.


These activities ensure reliable, asynchronous communication between devices, making UART widely used in embedded systems, microcontrollers, and FPGAs. 


## Technology Used ##

UART design, specifically focusing on how it can be implemented using FPGAs and HDL (Verilog), which you're familiar with:

Technology Used in UART Design

## 1. FPGA (Field-Programmable Gate Array): ##

Programmable Logic: FPGAs offer configurable logic blocks that allow for the design and implementation of custom UART modules. The UART design can be synthesized and deployed on the FPGA using HDL.

High-Speed Serial Communication: FPGAs are widely used in embedded systems for high-speed communication interfaces, such as UART, SPI, and I2C, offering flexibility in baud rate control and serial communication tasks.



## 2. HDL (Hardware Description Language): ##

Verilog: The UART is typically implemented in HDL like Verilog or VHDL. In your case, Verilog is used to describe the behavior of the UART at the hardware level. You can write a top-level module and other submodules (for transmitter, receiver, baud rate generator) to simulate and synthesize the UART for FPGA.

Synthesis Tools: Tools like Vivado (which you're familiar with) convert Verilog code into a gate-level representation, which is then deployed onto the FPGA. This allows for detailed timing analysis, resource utilization checks, and the creation of RTL schematics.



## 3. Baud Rate Generator: ##

Clock Divider: The baud rate generator in UART uses a clock divider circuit that takes the main FPGA clock and divides it to match the desired baud rate for data transmission/reception. This is typically implemented in Verilog as a counter.



### 4. FIFO (First-In, First-Out) Buffers: ###

Memory Management: FIFO buffers are used for managing data flow in UART to avoid data loss when handling high-speed communication. This is implemented in Verilog using registers and control logic to ensure data is processed in the correct order.



## 5. Error Handling: ##

Parity Check: UART often implements parity bits to detect errors in transmission. The Verilog code will include logic to add a parity bit (for transmission) or check the received parity bit (for reception) to ensure data integrity.

Framing and Overrun Errors: Logic is also implemented to detect framing errors (when the start or stop bit is incorrectly received) or overrun errors (when the receiver's buffer is full).




# Custom Design Flow for UART 

## 1. Specification: ##

Define the baud rate, data frame format (e.g., 8 data bits, 1 stop bit, optional parity), and error-checking mechanisms.



## 2. Verilog Implementation: ##

Write the UART modules in Verilog:

Transmitter: Serializes the data and adds start/stop bits.

Receiver: Deserializes the data, removes start/stop bits, and handles error checking.

Baud Rate Generator: Ensures correct timing for bit transmission/reception.




## 3. Simulation: ##

Simulate the Verilog code using Icarus Verilog or similar tools to check for functional correctness.



## 4. Synthesis: ## 

Use Vivado to synthesize the Verilog design onto the FPGA, checking for timing issues and resource usage.



## 5. Testing and Debugging: ##

Test the synthesized UART on the FPGA using a testbench and actual hardware communication, adjusting the design as needed to handle real-world signals.

# Summary of the UART Transmitter and Receiver Code

The code consists of two Verilog modules: uart_tx (UART Transmitter) and uart_rx (UART Receiver), designed to handle serial communication over a UART interface.

# UART Transmitter (uart_tx):

The transmitter module is responsible for sending 8-bit data serially over a single wire (tx).

## Inputs: ##

clk: System clock.

reset: Resets the transmitter to its initial state.

tx_start: Signal to start the transmission.

tx_data: The 8-bit data to be transmitted.


## Outputs: ##

tx: The UART transmit line where data is sent serially.

tx_ready: Indicates that the transmitter is ready for the next data to be sent.



## Working: ##

When tx_start is high and the transmitter is ready (tx_ready is 1), the transmitter sends a start bit (0), followed by the 8 bits of data, and then a stop bit (1).

The shift_reg stores the data to be transmitted, and a counter ensures the timing of each bit according to the baud rate.

Once all bits are sent, the transmitter goes idle, and tx_ready is set to 1, indicating it's ready for the next transmission.


# UART Receiver (uart_rx):

The receiver module is responsible for receiving serial data on the rx line and assembling it into 8-bit data.

## Inputs: ##

clk: System clock.

reset: Resets the receiver to its initial state.

rx: The UART receive line where data is received serially.


## Outputs: ##

rx_data: The 8-bit data received from the rx line.

rx_ready: Indicates that valid data has been received.



## Working: ##

The receiver waits for a start bit (0) on the rx line.

After detecting the start bit, it samples each bit of the incoming data at regular intervals (calculated by the baud rate) and stores it in shift_reg.

Once 8 bits are received, the assembled data is stored in rx_data, and rx_ready is set to 1, indicating valid data is available.


## Baud Rate and Timing: ##

Both modules use the baud rate (set to 9600) and system clock frequency (50 MHz) to control the timing of data transmission and reception.

The BIT_PERIOD is calculated as the number of clock cycles per bit, ensuring that data is sent and received at the correct speed.


## Key Features: ##

The UART Transmitter sends data in a serial format with a start bit, 8-bit data, and a stop bit.

The UART Receiver detects the start bit, samples the data, and signals when valid data is received.

Both modules use internal counters and shift registers to ensure correct timing and data handling.

Use Vivado to synthesize the Verilog design onto the FPGA, checking for timing issues and resource usage.


## Waveform 

![Screenshot (35)](https://github.com/user-attachments/assets/3149fcb6-5cf2-4782-b464-eeec9bb34949) 

## RTL Schematics

![Screenshot (36)](https://github.com/user-attachments/assets/9dbcde0a-9e71-475c-953b-375c18dcaf4e)  

## Synthesis

![Screenshot (37)](https://github.com/user-attachments/assets/b70ced6f-2a1e-401e-9281-19d8fd57e632)


