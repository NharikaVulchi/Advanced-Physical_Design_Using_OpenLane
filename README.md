
## DAY 1 Introduction to open-source EDA , OpenLane and Sky130 PDK


<details>
  
<summary>
Introduction to package, chips and ICs
</summary>

The chip design process begins with conceptualization, where the designers outline the high-level functionality, goals, and specifications of the chip.Processor interfaces all the instructions that are performed on the board(micro-controller).


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/2b3cf20b-89a0-402a-b10c-83f26b25a103)

1. Chip is the IC of the board, all the on-board pins are interfaced with the processing unit.
2. PADS are the interface between the signals which mvoe into and outside the chip
3. Core of the chip is Digital Logic Unit where the digital instructions are performed.
4. The chip design is fabricated on silicon, this is called a die

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/db38c896-fe93-4a9c-abfd-ba519034f29a)

1. A sample RISC-V SoC is shown in the below figure.
2. PLL, ADC, SRAM's on the chip are the foundry IPs(Intellectual property)
3. macros are the digital units 

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/049e4aa9-096e-448a-b74d-514a3440da38)


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/5c893594-2d1b-4f11-a151-d4d4e795aeea)



**Introduction to RISC-V**


RISC-V is an open-source instruction set architecture (ISA) designed with simplicity and versatility. It features a modular structure, enabling custom extensions for diverse applications. Its load-store memory model and compact register set streamline execution. Privilege levels ensure secure operation. RISC-V suits embedded systems to high-performance computing, fostering innovation through open collaboration and customization. It is a 64 bit architecture.

Applications to Hardware: There are 3 major steps of how an application can be run on hardware, which are as follows:

Operating System:

Interface between hardware and user.

Compiler

Converts the high level language to respective instruction set which are hardware specific such as MIPS, Intel or RISC-V.

Assembler

Converts the output from compiler, to binary language which are further fed to the hardware.

</details>

<details>
<summary>
SoC design and OpenLane
</summary>


**Introduction to all components of open-source digital ASIC design**

Digital ASIC design basic elements:


1. RTL IP's (Register Transfer Level Intellectual Property ):RTL IPs are pre-designed and pre-verified building blocks of digital logic circuits. These blocks are created using hardware description languages (HDLs) like Verilog or VHDL. RTL IPs can include components such as adders, multiplexers, flip-flops, memory blocks, and more.
2. EDA tools (Electronic Design Automation) : EDA tools are software applications that facilitate the design, analysis, simulation, and verification of electronic circuits and systems. In ASIC design, EDA tools are essential for tasks like RTL synthesis, logic optimization, floor planning, placement, routing, and timing analysis. These tools help automate many aspects of the design process, improve design productivity, and ensure that the ASIC meets its performance and power consumption requirements.
3. PDK Data (process design kits) :Collection of files to model a fabrication process for the EDA tools used to design an IC. Few of them are device models, digital standard cell libraries, I/O libraries.


**Opensource RTL Designs: github, librecores, opencores**

**Opensource EDA tools: QFlow, OpenROAD, OpenLANE**

**Opensource PDK data: Google Skywater130 PDK**

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/96edde63-0411-4c58-85cb-cd8b04b2e50c)




**Simplified RTL2GDS flow**

Major steps in RTL to GDS flow are described below:




1. **Synthesis** : Design is translated to circuits made of components which are the logic cells. Eah stndard cell have a regular layout. Cell width is variable and discrete . Each cell has different views which comes with the EDA tools.RTL code is transformed into a gate-level netlist using synthesis tools. These tools map RTL constructs into specific gates and optimize the design for area, power, and speed.

2. **Floor and power planning** : Planning the silicon area on which we fabricate our design to create robust power distribution. Rows, pin locations and routing tracks are designed here. In power planning, power pins are connected to all the cells through power straps, pads and rings.

3. **Placement** : Gate level netlist cells are placed on the rows such that interconnect delay is reduced and to enable better routing. This is done in 2 steps:
       --> Global placement : Finds the optimal positions for all cells, which can nvolve cell overlapping
       --> Detailed placement : Positions are minimally altered to their fixed positions

4. **Clock Tree Synthesis** : After the placement , we deliver clock to all the cell components by creating the clock distribution network. The clock network is in the shape of a tree, with the clock as node and all the elements as leaves. The clock should be delivered to all the cells with minimum skew and latency. Clock Skew means the arrival of time at different cells at different times.

   
![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/412c6693-771d-446c-b6e4-fdaa40bd18a1)

5. **Routing** : After placing the cells, the next step is signal routing. A valid pattern of horizontal and vertical wires is found to interconnect the cells. The router uses available metal layers defined by EDA. Finite width and pitch is defined for the metal layers. Skywater130 PDK defines 6 different metal layers. Lowest layer is the local interconnect layer, its the titanium nitride layers. The other 5 layers are aluminium layers.Most routers are grid routers. Divide and conquer approach is used for routing


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/646822f6-47fa-45b9-90df-0b107e425b31)


6. Sign off: After routing the chip undergoes verification process.
     * Physical verification
             --> Design Rule Checking (DRC)
             --> layout vs Schematic (LVS)
     * Timing Verification
             --> Static Timing Analysis (STA)


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/0a8cc960-33bc-4af9-b180-54b7d43b4dd8)



**Introduction to OpenLane and striVe Chipsets**

* OpenLane is an open-source digital integrated circuit (IC) design flow and toolchain that helps automate the process of designing and manufacturing custom semiconductor chips or integrated circuits.

* OpenLane is developed as an open-source project, which means that the source code and associated tools are freely available for anyone to use, modify, and contribute to. 
  
* OpenLane automates many of the tasks involved in the IC design process, including synthesis, placement, routing, and more. This automation can significantly reduce the time and effort required to design a custom chip.

* Openlane has different families, one of them is stiVe

  ![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/6d21b9eb-4cb4-4f61-9070-55a933be9aaa)



**Introduction to OpenLane detailed ASIC design flow**
</details>

<details>
<summary>
Get familiar to open-source EDA tools
</summary>

**OpenLane Directory Structure in Detail**

**Design Preparation Step**

**Review files after design prep and run synthesis**

**OpenLane project Git link description**

**Steps to characterize synthesis results**


</details>


## DAY 2 Floor planning and Introduction to Library Cells

<details>
<summary>
Chip floor planning considerations
</summary>
</details>

<details>
<summary>
Library Binding and Placement
</summary>
</details>

<details>
<summary>
Cell design and characterization flows
</summary>
</details>

<details>
<summary>
General timing characterization parameters
</summary>
</details>

## DAY 3 Library Cell using Magic Layout and ngspice characterization

<details>
<summary>
Labs for CMOS inverter ngspice simulations
</summary>
</details>

<details>
<summary>
Inception of layout A CMOS fabrication process
</summary>
</details>

<details>
<summary>
Sky130 Tech File Labs
</summary>
</details>


## DAY 4 Pre-layout timing analysis and importance of good clock tree

<details>
<summary>
Timing modeling using delay tables
</summary>
</details>

<details>
<summary>
Timing analysis with ideal clocks using OpenSTA
</summary>
</details>

<details>
<summary>
Clock tree synthesis TritonCTS and signal integrity
</summary>
</details>

<details>
<summary>
Timing analysis with real clocks using OpenSTA
</summary>
</details>

## DAY 5 Final steps for RTL2GDS using tritonRoute and openSTA

<details>
<summary>
Routing and Design Rule Check(DRC)
</summary>
</details>

<details>
<summary>
Power Distribution Networking and Routing
</summary>
</details>

<details>
<summary>
TritonRoute Features
</summary>
</details>

