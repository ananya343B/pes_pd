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

- PADS

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

#### Simplified RL2GDS flow

The flow mainly consists of the following steps:

![Screenshot (17)](https://github.com/ananya343B/pes_pd/assets/142582353/e8fff7da-5b9b-4ce4-beb3-48e50f7bdbd0)

1) **Synthesis**

   Converts RTL to circuit out of components from standard library cell (SLC). Standard cells have regular layout.

2) **Floor/ Power planning**

   - Chip floor planning: Partition the chip die between different system building blocks and place I/O pads.
  
   - Macro floor planning: Dimensions, pin location, row definition is decided.
  
   - Power planning: Power network is constructed.

3) **Placement**

   Place cells on floor paln rows, alligned with the sites.
   Two steps:

   - Global placement: Cells may overlap.
  
   - Detailed placement: Cells do not overlap.

4) **Clock tree synthesis**

   Creates clock distribution network.

5) **Routing**

   Implement the interconnects using available metal layers.

   Divide and conquer in routing:

   - Global routing: Generates routing guides.

   - Detailed routing: Uses the routing guides and implement the actual wiring.

6) **Sign off**

   Construction of final layout and verification.

   Physical verification:

   - Design rules checking (DRC)

   - Layout vs Schematic (LVS)

   Timing verification:

   - Static timing analysis (STA)


#### Introduction to OPENLANE

OpenLane is an open-source digital ASIC (Application-Specific Integrated Circuit) design flow framework. It provides a comprehensive set of tools and scripts for automating and streamlining the process of designing and manufacturing custom silicon chips. 

Main goal: to produce a clean GDSII with no human intervention.

Two modes of operation: Autonomous and Interactive.

**OPENLANE ASIC flow**

![Screenshot (18)](https://github.com/ananya343B/pes_pd/assets/142582353/06d745f3-3c72-4bb1-abbb-1f3d7454e885)


Synthesis exploration is a process in digital integrated circuit design where designers explore various design options and configurations during the synthesis stage. The goal is to find the best combination of logic optimizations, architecture choices, and design constraints to meet the desired performance, power consumption, and area targets for the design.

Design exploration refers to the process of investigating and evaluating various design alternatives, configurations, and choices to optimize a system or product's performance, functionality, cost, or other key attributes.

Regression testing uses design exploration utility on approximately 70 designs and compares the results with the best known ones.

- Design for Test (DFT) is a set of engineering techniques and practices employed during the design of integrated circuits and electronic systems to facilitate and improve the testing and verification process. The main objective of DFT is to make it easier to detect and diagnose faults, defects, or issues within the IC or system.

- Physical implementation refers to the process of transforming a high-level logical description of an IC into a physical layout that can be fabricated. Process involves Floorplanning, Placement, Clock Tree Synthesis, Routing etc

- Logic Equivalence Check done by using yosys. Every time the netlist is modified ,verification must be performed. CTS modifies the netlist, post placement optimizations modifies the netlist

- Antenna Rules ViolationsWhen ametal wire segment is fabricated ,it can act as an antenna. Reactive ion etching causes charges to accumulate on the wire due to which transistor gates are damaged during fabrication. Solutions are bridging attaches a higher layer intermediary or adding antenna diode cell to leak away charges

  


##### Getting Familiar with the Open Source EDA Tools

Tool we will be working on pdk variant called sky130_fd_sc_hd

sky130 : is the process name

fd : skywater foundary

sc : standard cell

hd(high density) : variant of pdk

Design Preperation step First we go the the working directory

```cd Desktop/work/tools/```

```cd openlane_working_dir/```

```cd openlane```

Type ```docker``` command, a shell opens . In the shell type ```./flow.tcl -interactive```

photo

Type ```package require openlane 0.9``` to import all the packages

photo

```prep -design picorv32a```

photo

After preparing the design, a new 'runs' folder is created.

photo

```run_synthesis```

2 photo

Flop ratio = 1613/14876 = 0.108

10.8% of the cells in our design are flip flops

Netlist is generated in the runs folder

photo






</details>
