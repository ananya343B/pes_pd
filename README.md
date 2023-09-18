![image](https://github.com/VardhanSuroshi/pes_asic_class/assets/132068498/33403244-c9dd-4aef-a022-da52e2eef51c)

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
 
## Introduction to QFN-48 package, chip, pads, core, die and IPs

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

![one](https://github.com/ananya343B/pes_pd/assets/142582353/27106a1c-c77d-4294-95c8-a922da405f80)


Type ```package require openlane 0.9``` to import all the packages


```prep -design picorv32a```

![two](https://github.com/ananya343B/pes_pd/assets/142582353/da9450e7-1bc6-4f9d-8336-7d584db3f03f)


After preparing the design, a new 'runs' folder is created.

![three](https://github.com/ananya343B/pes_pd/assets/142582353/3e8aa2cc-50c3-498d-ac76-38178f6eef05)

![four](https://github.com/ananya343B/pes_pd/assets/142582353/ad3c3631-9a20-4f16-857f-1ae2d6e98df7)


```less merged.lef```

![five](https://github.com/ananya343B/pes_pd/assets/142582353/12865f0d-3576-4901-84f2-d3d537570d2f)

![six](https://github.com/ananya343B/pes_pd/assets/142582353/b8e7f044-3e7c-4716-861e-acaf84902671)

``` less config.tcl```

Default parameters taken by the run

![seven](https://github.com/ananya343B/pes_pd/assets/142582353/ac821ee5-11eb-44a3-a428-89b98c7af487)

![eight](https://github.com/ananya343B/pes_pd/assets/142582353/0e897980-d29a-4f72-a7a0-f8bd36777516)

```less cmds.log```

Has all commands.

![nine](https://github.com/ananya343B/pes_pd/assets/142582353/91d75f98-ac9b-441f-92ab-b15744e6b21a)

![ten](https://github.com/ananya343B/pes_pd/assets/142582353/26f6a09c-78b6-4732-bee8-9c04a1f7123c)


```run_synthesis```

![twelve](https://github.com/ananya343B/pes_pd/assets/142582353/bfa6d72f-7ea4-4083-8a30-1a36b83538b0)

![eleven](https://github.com/ananya343B/pes_pd/assets/142582353/38512c83-a562-48cd-9b74-58abefada6d7)

Ratio of no. of flip flops to total no. of cells = 1613/18039 = 0.0894.

Netlist is generated in the runs folder

![thirteen](https://github.com/ananya343B/pes_pd/assets/142582353/5393d808-caca-4251-bdd2-8390078193f1)

</details>

<details>
<summary> 
 Day 2
</summary>
<br>

## Good floorplan vs Bad floorplan and Introduction to library cells

### Chip floorplanning considerations

**1) Defining width and height of core and die**

   Consider a netlist having flip flops and combinational logic. We take the combinational logic in terms of blocks to calculate the area.

   ![Screenshot (19)](https://github.com/ananya343B/pes_pd/assets/142582353/4fa35857-3743-4464-bbda-a2c4aa48b803)

    Let the dimension of the blocks be 1x1.

   ![Screenshot (20)](https://github.com/ananya343B/pes_pd/assets/142582353/33ee1743-e5a4-4971-8d51-8d9e8c7d615c)

   Arrange the blocks for minimum area
   
   ![Screenshot (21)](https://github.com/ananya343B/pes_pd/assets/142582353/adcc3706-7966-4363-b8fc-a2f73a4fd767)

   Place the logic segment inside the core

   ![Screenshot (22)](https://github.com/ananya343B/pes_pd/assets/142582353/6b316025-9d14-4f47-b3e2-a00ec558dd7e)

   ##### Aspect ratio and Utilization factor

   ![Screenshot (23)](https://github.com/ananya343B/pes_pd/assets/142582353/0fb1d50f-0bfb-4723-990b-df8629001e28)

   In the above case utilization ratio = 1.  Ideally utilization ratio is 0.5 to 0.6

   Aspect ratio = height/ width =1/1 = 1.


**2) Defining locations of pre placed cells**

Pre-placed cells are predefined blocks or modules of logic gates, flip-flops, or other functional elements that have a fixed placement on the chip's layout. Unlike standard cells, which are synthesized from a library of basic logic gates and placed automatically by a synthesis tool, pre-placed cells are manually placed by the chip designer in specific locations on the chip.

First divide the logic into blocks:

![Screenshot (28)](https://github.com/ananya343B/pes_pd/assets/142582353/62dfe1be-c7cd-4122-b606-7e5d32387574)

Extend the IO pins and make the blocks as different IPs or modules:

![Screenshot (29)](https://github.com/ananya343B/pes_pd/assets/142582353/e8210d2b-289d-4ba5-8b40-a4c4d640b0b7)

- The arrangement of Ips in a chip is referred as floorplanning.

- These IPs have user defined locations ans hence are placed in the chip before the automated placement and routing is done. These cells are called pre placed cells.

- Automated placement and routing toll places the remaining logical cells in the design onto the chip.
  
**3) Surround the preplaced cells with decoupling capacitors**

![Screenshot (24)](https://github.com/ananya343B/pes_pd/assets/142582353/bfcaa1e9-37d6-41f0-87cb-ad7ad9fd8e43)

During the switching operation, current is demanded by the circuit (peak current)

Due to Ldd and Rdd there will be a voltage drop and the voltage at node A is not Vdd but Vdd'.

If Vdd' goes below the noise margin, there can be an incorrect output at the end of the circuit. (Logic 1 becomes Logic 0 and vice versa).

![Screenshot (26)](https://github.com/ananya343B/pes_pd/assets/142582353/856968d5-89bc-4a65-9d3a-80c04a996980)

To avoid this we place a capacitor with large capacitance in paralel to the circuit.

![Screenshot (27)](https://github.com/ananya343B/pes_pd/assets/142582353/2e5c4bcb-41c0-4a57-b9e8-eda55190e263)

Everytime the circuit switches it draws current from the decoupling capacitor, whereas the outer network with the power supply and other componets is used to re-charge the capacitor

The primary purpose of a decoupling capacitor is to reduce or minimize voltage fluctuations and noise on the power supply lines caused by the rapid switching of transistors within the IC. When digital circuits switch, they can draw short bursts of current from the power supply, causing momentary drops in voltage. 

The decoupling capacitor is placed as close to the circuit as possible to minimise loss due to large wire length.

**3) Power planning**

![Screenshot (30)](https://github.com/ananya343B/pes_pd/assets/142582353/d6acdd39-5846-4f23-832d-62d12e68357e)

Signal from the driver should remain same until it reaches the load throught the line.

To ensure that we require a power supply.

Ground bounce: "Ground bounce" is a phenomenon that occurs when there is a temporary increase in the voltage level of the ground (GND) reference plane due to the switching activities of digital circuits. Ground bounce is a type of noise or voltage perturbation on the ground line of an IC. If the ground bounce is not within the noise margin, we may enter the undefined region which should be avoided.

![Screenshot (31)](https://github.com/ananya343B/pes_pd/assets/142582353/395c9de5-a204-49c2-a551-44d98c8c366a)

Voltage droop:  "Voltage droop," also known as "voltage sag" or "power droop," refers to a temporary decrease or reduction in the supply voltage level in response to a sudden increase in current demand within the circuit. 

![Screenshot (32)](https://github.com/ananya343B/pes_pd/assets/142582353/b1b64bb2-5e7b-4705-baf3-6dd7d46064a4)

These problems occur because there is only one voltage supply. We use multiple voltage supplies which run as a grid in the core. Such a pattern is referred as a voltage mesh.

![Screenshot (33)](https://github.com/ananya343B/pes_pd/assets/142582353/144be3a8-9aec-4578-9895-b3bd8f8af61e)

![Screenshot (34)](https://github.com/ananya343B/pes_pd/assets/142582353/fa2b93a2-7e0a-4dfe-9d01-7fca16fe0fbf)

**4) Pin Placement and logical cell blockage**

In pin placemnt step we use the HDL netlist to determine where a specific pin should be placed in the circuit.

We join the common pins and try to keep the connections as effecient as possible.

Pins are placed in the Die area. 

The pin for the clock signal is bigger as they contin=nuosly send signals to the entire circuit ie. it drives the chip

No cells are placed between the core and the die.

### Lab

Run the command ```run_flooorplan``` in the openlane shell

Go to the  ```/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14-09_17-44/results/floorplan``` directory and run the following command:

```magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &```

 Magic opens and we can see the cell. Use s and then v on the keyboard to center the floorplan. Use z to zoom in.
 
![Screenshot (37)](https://github.com/ananya343B/pes_pd/assets/142582353/b355b0d0-0b3d-449d-9119-b44e22e8d226)

![Screenshot (38)](https://github.com/ananya343B/pes_pd/assets/142582353/ec298ee6-c435-4022-b8ac-e2dbcda38f31)


### Library Binding and Placement

Netlist binding and initial place design

Netlist binding is the process of mapping the logical representation of a digital design (typically described in a hardware description language l onto a library of standard cells.

Each component is mapped to a given shape. All these shapes and the working are defined in the library. Then all these shapes from each stage of the netlist are placed onto the floorplan in a efficient way so that delay is minimal.

![Screenshot (39)](https://github.com/ananya343B/pes_pd/assets/142582353/41013d89-a123-44d4-9661-2ab5c8431c6d)

The components of the netlist are placed in the core area.

They are placed according to the convenience of distance from the pins.

When sending signal from FF1 to FF2, according to the circuit requirements, there has to be a very fast propogation of signals. Hence, they are placed very close and buffers are added since there is a small delay for the signal from the pin to reach FF1. The buffers maintain signal integrity.

Estimated wire-length and capacitance is a crucial step to ensure that the physical layout of components and interconnections meets performance and power goals. Wire-length estimation and capacitance modeling help guide the placement process, especially when considering factors like signal delay, power consumption, and signal integrity. If the wire area is big then the resistance and capacitance huge. To maintain signal inteegrity we route the signal through buffers that replicates and routes the signals.

The integration of wire-length and capacitance estimates into the placement optimization process helps balance performance, power, and area trade-offs in the design. The goal is to achieve a placement that minimizes signal delays, reduces power consumption, maintains signal integrity, and meets all design constraints.

- Final placement optimization

When performing final placement optimization with timing analysis using an ideal clock, you are essentially optimizing the physical placement of components within an integrated circuit while assuming that the clock signal is perfect.. This approach allows you to focus primarily on optimizing the physical layout of the design without considering clock-related timing challenges.

- Need for libraries and characterization

Libraries and characterization are foundational elements of the IC design process. Libraries provide standardized building blocks that enhance design productivity and reusability, while characterization provides the essential data needed to accurately model and simulate the behavior of these components, ensuring that the final design meets its performance, power, and reliability goals.

#### Lab

To view the placement, type ```run_placement``` in the openlane shell.

We type the following command in the terminal in the  ../OpenLane/designs/picorv32a/runs/<most_recent_run>/results/placement/ directory

```magic -T ../git_open_pdks/sky130/magic/sky130.tech lef read ../OpenLane/designs/picorv32a/runs/<most_recent_run>/tmp/merged.nom.lef def read picorv32.def &```

![Screenshot (40)](https://github.com/ananya343B/pes_pd/assets/142582353/2f8158ef-1b19-43b1-bda2-98f9de28f1f9)

![Screenshot (41)](https://github.com/ananya343B/pes_pd/assets/142582353/679fbd90-8ca0-401d-bbb6-3194e73b8474)

We can see the standard cells used upon zooming.

#### Cell Design and Characterization Flow

Inputs :Process design kits(PDKs) : DRC and LVS rules, SPICE models, library and user-defined specs.

Design Steps: Circuit Design, Layout Design(Euler Path and Stick Diagram), Characterization.

Outputs: CDL(Circuit Description Language), GDSII, LEF, extracted spice netlist(.cir)

**Characterization Flow**

For an inverter:

1)Read the model files.

2)Read the extracted SPICE netlist.

3)Recognize the behaviour of the buffer.

4)Attaching the necessary power sources

5)Apply the stimulus, which is the input signal to the circuit.

6)Read the sub-circuit of the inverter.

7)Provide necessary output capacitances.

8)Provide the necessary simulation commands

Timing Characterization

- slew_low_rise_thr = 20%

- slew_high_rise_thr = 80%

- slew_low_fall_thr = 20%

- slew_high_fall_thr = 80%

- in_rise_thr = 50%

- in_fall_thr = 50%

- out_rise_thr = 50%

- out_fall_thr = 50%

**Propagation Delay**

The time difference between when the transitional input reaches 50% of its final value and when the output reaches 50% of its final value.

Propagation delay=time(out_fall_thr)-time(in_rise_thr)

**Transition Time**

The time it takes the signal to move between states is the transition time , where the time is measured between 10% and 90% or 20% to 80% of the signal levels.

Rise transition time = time(slew_high_rise_thr) - time (slew_low_rise_thr)

Fall transition time = time(slew_high_fall_thr) - time (slew_low_fall_thr)
</details>


<details>
<summary>
 Day 3
</summary>
<br>
 
 **IO Placer revision**
 
PnR is a iterative flow and hence, we can make changes to the environment variables when required.

To change the pin configuration along the core from equvi distance randomly placed to someother placement.

```set::env(FP IO MODE)2```


##### Inception of Layout and CMOS Fabrication Process

**SPICE Deck Creation for CMOS Inverter**
- SPICE Deck is a netlist that has information on:
  
  - component connectivity
    
  - component values
    
  - identifying the nodes
    
  - giving a designation to the nodes

**SPICE Simulation and Switching Threshold**

Switching Threshold of a CMOS Inverter CMOS cells have three modes of operation:

Cutoff - No inversion Triode - Inversion but no pinchoff in channel Saturation - Inversion and pinchoff in channel

The voltages at which the switch between the modes of operation happens is dependent on the threshold voltage of the device. Threshold voltage is a function of the W/L ratio of a device, therefore varying the W/L ratio will vary the output waveform of CMOS devices. To enable efficient description of the varying waveforms a single parameter called switching threshold is used. Switching threshold is defined at the intersection of Vin = Vout.

![image](https://github.com/ananya343B/pes_pd/assets/142582353/98ba86bb-fac0-4293-9669-018c115636fc)


![image](https://github.com/ananya343B/pes_pd/assets/142582353/9e3c77ea-bc56-48a0-bf3f-4ccd7c8fe88a)



SPICE Simulation steps:

```
cd <folder where the .cir file is present>
source CMOS_INVERTER.cir
run
setplot
dc1
display
plot out vs in
```

**16 Mask CMOS Process**

1) Selecting a Substrate - Selecting the appropriate substrate to synthsize the design on.

2) Creating active reagion for transistors - Adding layers of SiO2(40nm), Si3N4(80nm) and photoresist(1um). On top of the photoresist we put a mask layer. Pass UV light and remove the mask. Resist is removed. LOCOS(Local Oxidation of Silicon) is performed. Si3N4 is etched.

3) N-Well and P-Well formation - The next masks are used to create the source and drain regions of the MOSFETs. Boron is used to make P-Well using ion implantation. Phosphorus is used to create N-Well. Put the MOSFET in a Drive In furnace.

4) Formation of Gate - Gate formation involves depositing a gate oxide, defining gate patterns using photolithography, depositing gate material, etching to create gates, doping the substrate and insulating the gates.

5) Lightly Doped Drain Formation(LDD) - Lightly doped drain (LDD) formation involves implanting the drain and source regions of a MOSFET transistor with a lighter concentration of dopants to reduce hot electron effect and short channel effect and enhance device performance.

6) Source and Drain Formation - Source and drain formation in a MOSFET transistor typically involves doping the silicon substrate with chemicals such as arsenic or phosphorous for n-type regions (source and drain) and boron for p-type regions (source and drain). High temperature annealing is performed.

7) Steps to form Contacts and Interconnects(local) - Titanium is deposited with a process known as sputtering. Wafer is heated to about 650 - 700 C in an N2 ambient furnace for 60 seconds. TiSi2 contacts are formed.  TiN is also formed used for local communication. TiN is etched using RCA cleaning.

8) Higher Level Metal Formation - Forming contacts and interconnects locally involves depositing a dielectric material like silicon dioxide, patterning it using photolithography, etching contact holes, depositing a barrier metal (e.g., titanium or titanium nitride), filling with a conductor (e.g., aluminum or copper) using chemical vapor deposition (CVD), and then planarizing through chemical-mechanical polishing (CMP).


Git cloning:

```
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```
- Now we need to copy the  'sky130A.tech' file into the directory  just cloned

```
cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
```

in the follwoing directory

```
... openlane_working_dir/pdks/sky130A/libs.tech/magic
```

command for layout

```
magic -T sky130A.tech sky130_inv.mag &
```

![image](https://github.com/ananya343B/pes_pd/assets/142582353/11b9e184-92ab-4cf9-b443-a4686251414a)


Click on the component and type ```what``` in the tkcon window

To select a region, place cursor on that point and press ```s```. 

![image](https://github.com/ananya343B/pes_pd/assets/142582353/2d0eee22-437e-4056-8c3c-4da2d7b579fa)


**DRC Check**

To check for DRC Errors, select a region (left click for starting point, right click at end point) and see the DRC column at the top that shows how many DRC errors are present.The Details of DRC Errors will be printed on the console.

![image](https://github.com/ananya343B/pes_pd/assets/142582353/e7581556-80e0-4a47-a73e-46204491ab5d)

**Extracting to SPICE Command**

Use the following commands in the tkcon window to extract the spice netlist.

```
pwd
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```

```cthresh``` and ```rthresh``` are used to extract all parasatic capacitances.

![image](https://github.com/ananya343B/pes_pd/assets/142582353/5c6ad2a6-bba0-4576-a7bd-0575b9011e16)

Activate the grid and right click on a grid.

Type the command ```box``` in the tkcon window to checkminimum value ofthe layout.

Spice wrapper file:

![image](https://github.com/ananya343B/pes_pd/assets/142582353/823afbe2-8bf5-4de1-8b24-79d97902b4cf)

To open the spice file using the command:

```gedit sky130_inv.spice```

Extraxted spice file:

![image](https://github.com/ananya343B/pes_pd/assets/142582353/f7843a5f-a54d-4647-a64b-6bbbd80518d6)

The above file has details of inverter netlist but the sources and their values are not specified. So we have to modify the file.

-Grid size from the layout is 0.01u

-specify the library for MOS

-create VDD, VSS, Input pulse Va

-specify the type of analysis to be done

![image](https://github.com/ananya343B/pes_pd/assets/142582353/76be91a1-7fa3-4e40-99eb-c570e904d620)


Modified Spice file:

![image](https://github.com/ananya343B/pes_pd/assets/142582353/7c3454ba-9929-41b6-8517-a389df818d9e)

To run the spice netlist, run ```ngspice sky130_inv.spice```

![image](https://github.com/ananya343B/pes_pd/assets/142582353/86771f60-027c-4d51-a818-608d0964dee0)

```plot y vs time a```

![image](https://github.com/ananya343B/pes_pd/assets/142582353/0020829a-b887-4e5f-8756-5531c84fce26)

