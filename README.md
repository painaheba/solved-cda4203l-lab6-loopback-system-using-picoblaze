Download Link: https://assignmentchef.com/product/solved-cda4203l-lab6-loopback-system-using-picoblaze
<br>
<strong>Objective:  </strong>To design and synthesize a loopback system using a PicoBlaze microcontroller, and to implement functionality using Assembly code.

<strong>Description: </strong> Consider a simple “loopback” system as in Fig. 1. In such a setup, a PC can send a message which is returned (looped) back to PC by the processor. Such a loopback  test is helpful to test the processor is alive or not.

Fig. 1. A simple loopback system

Fig. 2. UART Transmit and Receive Blocks – High Level View

A PC (not shown) interfaces with PicoBlaze processor using an RS232 (serial) connection. Let us examine the case when the PC acts as a transmitter. In this case the data arrives serially on RS232 RX line. But we know that PicoBlaze accepts only byte-size data. So, we need to convert the serial data into parallel (8-bit) data. In such a case, a UART (Universal Asynchronous Receiver Transmitter) block can help (Figure 2). UART_RX does the serial-to-parallel conversion i.e., the data arriving on RS232_RX line is buffered in a 16-byte buffer. Whenever new data is presented on rx_data output, UART_RX will assert data_present i.e., data_present = 1 in other words data_ present validates rx_data. The Input Port Logic block consists of glue logic that connects UART_RX to the IN_PORT. After PicoBlaze reads the data, it can request the next data item by asserting read by uart signal.

Now, let us consider the case when PicoBlaze acts as a transmitter i.e., PC is the receiver. In this case, PicoBlaze puts out 8-bit data while PC is expecting serial data. Again, UART (UART_TX in Fig. 1) comes to our rescue! The output bus with id=3 is connected to UART_TX. Output Port Logic block interfaces PicoBlaze with leds and UART_TX. In this system, we can also manually provide 8-bit data via 8 switches (switches bus in Fig. 1). PicoBlaze can write 8-bit data to drive 8 leds (leds bus in Fig. 1). Recall that PicoBlaze can accept up to 256 input ports each of which can addressed by 8-bit PORT_ID bus. Similarly, it can drive up to 256 ports and the address of the port being driven appears on PORT_ID bus. In Fig. 1, for example, the id of the input port, switches, is 0.

<ol>

 <li><strong>cold_start:</strong> Write code to output a message “Welcome to Loop-back!” to the serial port. You need to encode the message in ASCII format. CAUTION: UART_TX buffer size is only 16 bytes.</li>

 <li><strong>led_echo:</strong> Write code to read switches and write the values, inverted, to the LEDs.</li>

 <li><strong>rs232_echo:</strong> Write code to check if a byte has been received by UART_RX. If so, send it back to the PC via UART_TX.</li>

 <li><strong>Behavior:</strong> The design must be able to perform all the above actions simultaneously.</li>

</ol>

<strong>Design Constraints: </strong>

<ul>

 <li>The design must both function correctly in simulation and on the FPGA board.</li>

 <li>The RESET button must provide a global reset functionality. This includes resetting the microprocessor.</li>

 <li>The 100MHz Clock is used as the system clock.</li>

 <li>Every time the design is initialized (reset) it runs cold start.</li>

 <li>Until it is turned off or reset, it performs the following two actions continuously:</li>

</ul>

<ul>

 <li>Echo inverted Switch values to LEDs.</li>

 <li>Echo RS232 data back to PC.</li>

</ul>

<ul>

 <li>It must do this indefinitely.</li>

</ul>

<strong>Lab 6 – Step by Step Instructions</strong>

It’s strongly recommended that you perform the steps in the given order below.

<ol>

 <li><strong> Download and Unzip</strong></li>

</ol>

(a) In your home directory, create a new folder ‘lab6’.

(b) Download the loopback.zip file from canvas into ‘lab6’.

(c) Unzip the file.

<strong> </strong>

<ol start="2">

 <li><strong> Create ISE Project</strong></li>

</ol>

(a) Create a new ISE project.

(b) Ensure that you are using the correct settings (Tutorial 1).

(c) Add copies of all Verilog source files and the UCF file from the loopback directory.

<strong> </strong>

<ol start="3">

 <li><strong> Edit ‘loopback.v’</strong></li>

</ol>

(a) Complete Worksheet 1 on loopback.v

(b) Open ‘loopback.v’ and fill in the blanks.

<ol start="4">

 <li><strong> Edit ‘loopback.UCF’’</strong></li>

</ol>

(a) Complete Worksheet 2 on FPGA Pin Assignments.

(b) Open ‘loopback.UCF’’ and fill in the blanks.

<strong> </strong>

<ol start="5">

 <li><strong> Write Assembly Code</strong></li>

</ol>

(a) Open the “Assembler” folder in “loopback”.

(b) Open the ‘program.psm’ file with a text editor.

(c) Enter your assembly code for task 1. Note that the ASCII codes are already entered as constants. For example, if you want to load the ASCII code for ‘h’ then you can write:

LOAD sX, ascii h.

(d) To assemble the code, the syntax is: ./picoasm -i program.psm -t ROM form.v

(e) It will generate a file, ‘program.v’. Add a copy of this file to your project. It contains the assembled code for PicoBlaze.

<strong> </strong>

<ol start="6">

 <li><strong> FPGA Synthesis and Implementation</strong></li>

</ol>

(a) Synthesize and generate the lookup.bit file.

(b) Load the design onto the board.

<strong> </strong>

<ol start="7">

 <li><strong> RS232 Cable Connection</strong></li>

</ol>

(a) Connect the RS232 serial cable to the back of the C4 lab computer, as well as to

the XUP board.

<strong> </strong>

<ol start="8">

 <li><strong> Connect to Serial Port</strong></li>

</ol>

(a) To open the serial terminal, run ‘minicom’ from a terminal.

(b) Test the RS232 capabilities of your design (cold start, loopback).

(c) To exit, Press: ‘ctrl+A’ then ‘ctrl+z’ then ‘x’.

<strong> </strong>

<ol start="9">

 <li><strong> Finish</strong></li>

</ol>

(a) Write assembly code for led echo program. (Task 2)

(b) Write assembly code for rs232_echo program. (Task 3)

<strong> </strong>

<ol start="10">

 <li><strong> (Optional) Create and load PROM file.</strong></li>

</ol>

(a) Do this step only after you have finalized your design.

(b) The tutorial will be available on canvas.

(c) This allows the design to automatically be loaded when the board is powered on.

<strong> </strong>

<strong>Worksheet 1</strong>

<strong> </strong>

<ol>

 <li>What is the instruction bus width for the ROM?</li>

</ol>

<ol>

 <li style="list-style-type: none;">

  <ol>

   <li>18 bits</li>

  </ol></li>

</ol>




<ol start="2">

 <li>For the UART 16x bit rate counter, the maximum baud count using the following formula:</li>

</ol>

<em>max_baud_count = f<sub>clk</sub>/ (16*req_baud_rate)</em>




If f<sub>clk</sub> = 100MHz and the required baud rate is 9600, what is the maximum baud count?

<ol>

 <li>651</li>

</ol>




<ol start="3">

 <li>Write the boolean expression for the write to uart</li>

</ol>

<ol>

 <li style="list-style-type: none;">

  <ol>

   <li>assign write_to_uart = pb_write_strobe &amp; (pb_port_id == 8’h03);</li>

   <li>assign write_to_leds = pb_write_strobe &amp; (pb_port_id == 8’h01);</li>

  </ol></li>

</ol>




<ol start="4">

 <li>Write the boolean expression for the write to leds</li>

</ol>




<ol start="5">

 <li>What are the port_id values for the following input ports:</li>

</ol>

(a) switches:

(b) data_rx:

(c) data_present:

(d) buffer_full:




<ol start="6">

 <li>Write the boolean expression for the read_from_uart signal.</li>

</ol>




<ol start="7">

 <li>Continue with step 3 (b).</li>

</ol>

<strong> </strong>

<strong>Worksheet 2</strong>

<strong> </strong>

Fill in the pin locations for the following components/signals. Refer to the FPGA User Guide and master.ucf available on canvas.

<strong> </strong>

<ol>

 <li>Clock (100MHz):</li>

 <li>Push Button Up (for reset signal):</li>

 <li>LED 0:</li>

 <li>LED 1:</li>

 <li>LED 2:</li>

 <li>LED 3:</li>

 <li>LED 4:</li>

 <li>LED 5:</li>

 <li>LED 6:</li>

 <li>LED 7:</li>

 <li>SW 0:</li>

 <li>SW 1:</li>

 <li>SW 2:</li>

 <li>SW 3:</li>

 <li>SW 4:</li>

 <li>SW 5:</li>

 <li>SW 6:</li>

 <li>SW 7:</li>

 <li>RS232 TX (FPGA_SERIAL1):</li>

 <li>RS232 RX (FPGA_SERIAL1):</li>

</ol>




Now continue with Step 4 (b).

<strong> </strong>

<strong>Deliverables: </strong>

Submit a zipped archive consisting of: (a) A concise report that includes your PicoBlaze assembly code.  Include a README file. Organize your files in folders named Problem1, Problem2, and Problem 3.




<strong>Report Organization (A template is provided on canvas):</strong>

<ul>

 <li>Cover sheet</li>

 <li>Problem 1: Your design details, assembly code.</li>

 <li>Problem 2: Your design details, assembly code</li>

 <li>Problem 3: Your design details, assembly code</li>

 <li>Problem 4: Pin Mapping file and synthesis report.</li>

 <li>Feedback: Hours spent, Exercise difficulty (Easy, Medium, Hard)</li>

</ul>

<strong> </strong>

<strong>Important: </strong>