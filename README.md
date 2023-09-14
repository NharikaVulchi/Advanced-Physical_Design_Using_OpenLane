
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


6. **Sign off**: After routing the chip undergoes verification process.
     * Physical verification
             --> Design Rule Checking (DRC)
             --> layout vs Schematic (LVS)
     * Timing Verification
             --> Static Timing Analysis (STA)


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/0a8cc960-33bc-4af9-b180-54b7d43b4dd8)





**Introduction to OpenLane and striVe Chipsets**

* OpenLane is an open-source digital integrated circuit (IC) design flow and toolchain that helps automate the process of designing and manufacturing custom semiconductor chips or integrated circuits.
  
* Using OpenLane we produce a GDS with no human intervention that has no LVS violations, no DRc violations and no timing violations

* OpenLane is developed as an open-source project, which means that the source code and associated tools are freely available for anyone to use, modify, and contribute to. 
  
* OpenLane automates many of the tasks involved in the IC design process, including synthesis, placement, routing, and more. This automation can significantly reduce the time and effort required to design a custom chip.

* Openlane has different families, one of them is stiVe

  ![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/6d21b9eb-4cb4-4f61-9070-55a933be9aaa)

* OpenLane can be used to harden macros and chips

* There are 2 modes of operation : automative and interactive

 
**Introduction to OpenLane detailed ASIC design flow**


The below figure depicts OpenLane ASIC design flow

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/52e5e502-8322-4237-83f2-cd922df0d03b)


Synthesis Exploration : Best optimisation strategy is decided 


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/ad742388-bdfd-491c-8982-77bd14b3c80d)

Design exploration is a major step in Openlane where it tests the design on various metrics. OpenLane runs on 70 designs and compare the results to the best ones.

Testing :

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/1969f499-eea0-47a5-88d6-60ece938a8f4)

OpenRoad does the physical implementation: Placement and routing.

Netlist after the optimization is compared to the gate level netlist to ensure that they are functionally equivalent


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/736d7883-ee6e-4e2b-907e-795a8c55f264)


RTL Synthesis, Technology Mapping, and Formal Verification:  Yosys (for RTL synthesis), ABC (for technology mapping and formal verification).

Static Timing Analysis:OpenSTA (for static timing analysis).

Floor Planning: init_fp (initial floorplanning), ioPlacer (I/O placement), pdn (power distribution network planning), tapcell (tap cell insertion).

Placement: RePLace (global placement), Resizer (optional for resizing cells), OpenPhySyn (formerly used for placement), OpenDP (detailed placement).

Clock Tree Synthesis: TritonCTS (for clock tree synthesis).

Fill Insertion: OpenDP (for filler placement).

Routing:
   Global Routing: FastRoute or CU-GR (formerly used).
  Detailed Routing: TritonRoute (for detailed routing) or DR-CU (formerly used).

SPEF Extraction: OpenRCX (or SPEF-Extractor, formerly used) for Standard Parasitic Exchange Format (SPEF) extraction.

GDSII Streaming Out: Magic and KLayout (for viewing and editing GDSII files).

Design Rule Checking (DRC) Checks: Magic and KLayout (for DRC checks).

Layout vs. Schematic (LVS) Check: Netgen (for LVS checks).

Antenna Checks: Magic (for antenna checks).

Circuit Validity Checker: CVC (for circuit validity checking).



</details>

<details>
<summary>
Get familiar to open-source EDA tools
</summary>






**Design Preparation Step**


Installing Openlane 

```
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane --recurse-submodules 
cd OpenLane
make
make test
cd /home/niharika/OpenLane/designs/ci
cp -r * ../
```


Invoking Openlane

```
cd ~/OpenLane
make mount
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
```


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/37769e8a-4334-4cbe-a8da-232d4fe3a6e4)


Viewing the netlist file generated for **picorv32**

![Screenshot from 2023-09-11 15-33-14](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/87315fe6-aab7-4161-9765-afdf00dbaad6)


![Screenshot from 2023-09-11 15-32-59](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/2cd0464d-7bc9-4cc2-8f10-bcb39580e07d)



![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/bd5801d5-d333-4ef4-b3f8-10222f9049f9)



We can view the synthesis reports in the following directory:

```
/home/niarika/OpenLane/designs/picorv32a/runs/RUN_2023.09.14_06.35.44/logs/synthesis/1-synthesis.log
```

![Screenshot from 2023-09-14 12-27-03](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/3d439a88-81ac-4f25-8ba1-5febf75eb556)


</details>


## DAY 2 Floor planning and Introduction to Library Cells

<details>
<summary>
Chip floor planning considerations
</summary>
  
**Utlization factor and aspect ratio**
1. Width and height of core and die are dependent on the dimension on the logic gates that has to be designed on the chip.
2. We will calculate the area of a netlist and accordingly decide the area of core and die.
3. A core is the section of the die where the fundamental logic design sits
4. A die is a small semiconductor material specimen which encapsulates the core.
5. We place the logic cells inside the core
6. Utilization factor = Area of netlist / Area of core
7. Aspect Ratio =    Height/ Width
8. Aspect ratio is 1, implies that the core is square shaped.
9. A utilization factor of 0.5 to 0.6 isf typical and allows for the necessary design elements and potential future modifications
    

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/1fe173ce-eb8c-40f5-80c9-0bbd876685a8)


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/01bd0d0c-0ed0-4fe0-ba37-0c8adb66bdad)

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/cf397803-176d-4e02-a25c-0c71a4227c89)


**Pre-placed cells**
* Pre-placed cells are an integral part of the physical design process. They are placed manually or through automated placement tools in the chip layout, along with the interconnect routing to create a physical design that meets performance, power, and area constraints.hese cells typically include standard components such as logic gates, flip-flops, multiplexers, and other building blocks used in digital circuit design.

* Combinational logic that are implemented in common are generalised such that it is placed on the chip, with specific number of input and output pins.

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/1bda2c8e-ccd3-4c87-a77d-2e46f29105a9)

* This helps in multiple implementation of the same circuit when it is used greater number of times.

* There also IPs available which are used as preplaced cells:
        --> Memory

  
        --> Clock-gating cell

  
        --> Comparator

  
        --> MUX

  

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

