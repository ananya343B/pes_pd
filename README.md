# Physical design for ASIC

#### Advanced Physical Design using Openlane/Sky130

<details>
<summary> 
 Installation
</summary>
<br>

Create a Linux virtual machine with Ubuntu 18.04 (Bionic Beaver)(64 - bit) version.

Select ```openlane.vdi``` as the virtual hard disk.

Open terminal and follow the steps below:

![openlane_working](https://github.com/ananya343B/pes_asic_class/assets/142582353/afd0fe45-e39a-425c-aa82-9e981035d2c7)

![working_2](https://github.com/ananya343B/pes_asic_class/assets/142582353/1d77549d-5920-44f8-bc07-ea1afecb1ce5)

</details>

<details>
<summary> 
 Day 1
</summary>
<br>
 
#### Introduction to QFN-48 package, chip, pads, core, die and IPs

- PADS:

A peripheral device (PAD) refers to any external device or component that connects to an integrated circuit (IC) chip. These external devices can include input/output pins, power supply pins, clock input pins, and other interface pins that facilitate communication between the chip and the outside world. PADs are an essential part of chip design because they determine how the chip interacts with its environment.

- DIE

The silicon wafer is divided into multiple identical, discrete sections, each of which is known as a "die." Each die contains a single instance of the integrated circuit design that was created by the semiconductor design team. These dies are created using photolithography and other semiconductor fabrication processes, and they share the same design and functionality.

- CORE

A "core" is a functional block of circuitry that performs a specific function within an integrated circuit design. Cores are often reusable, customizable, and can simplify the development process by allowing designers to integrate well-optimized and tested circuitry into their projects. They are a fundamental building block for complex IC designs.

![Screenshot (13)](https://github.com/ananya343B/pes_pd/assets/142582353/8ca4186c-bbaa-48e9-b501-b7f97e8dbafc)


- FOUNDRY IPs

Foundry IPs are IPs that are specifically developed, qualified, and provided by the foundry to be used in conjunction with their manufacturing processes. These IPs are optimized for the foundry's technology, ensuring compatibility and efficiency. They are thoroughly tested and characterized to meet performance, power, and reliability requirements within the foundry's process.

- MACROS

Macros are pre-designed, customizable functional blocks that perform specific complex functions within an integrated circuit. They are a valuable tool for chip designers to streamline the design process, improve efficiency, and reduce the risk associated with complex custom circuit design.

![Screenshot (14)](https://github.com/ananya343B/pes_pd/assets/142582353/fb4c471a-f8f3-43a5-bd4e-a4347d671095)

#### Introduction to RISCV ISA and flow from Software applications to Hardware

![Screenshot (15)](https://github.com/ananya343B/pes_pd/assets/142582353/0afcd24f-0200-4bee-981f-4e6f2d1138a3)


1) C Program to RISC-V Assembly:

- Write a C program.
  
- Compile it using a RISC-V-compatible C compiler to generate RISC-V assembly code.

2) RISC-V Assembly to HDL:

- Analyze the assembly code.

- Write HDL code (e.g., Verilog or VHDL) to describe hardware components.
 
- Map assembly operations to hardware behavior in HDL.
  
- Design registers, datapath, control logic, and memory interfaces.

3) HDL to Binary:

- Use an HDL synthesis tool to translate HDL into a netlist.

- Optimize the design for performance, area, and power.

- Place and route components on the FPGA/ASIC.

- Generate a binary configuration file.

4) Program the Target Device:

- Load the binary configuration onto the FPGA/ASIC to configure it as hardware.

![Screenshot (16)](https://github.com/ananya343B/pes_pd/assets/142582353/63cd83f7-733a-40e6-8466-958c1f42b0a1)




</details>
