
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
* Pre-placed cells are an integral part of the physical design process. They are placed manually in the chip layout, along with the interconnect routing to create a physical design that meets performance, power, and area constraints.hese cells typically include standard components such as logic gates, flip-flops, multiplexers, and other building blocks used in digital circuit design.

* Combinational logic that are implemented in common are generalised such that it is placed on the chip, with specific number of input and output pins.


* This helps in multiple implementation of the same circuit when it is used greater number of times.

* Functionality of preplaced cells is implemented only once.
* The arrangement of these IP's in a chip is referred as floorplanning
* There also IPs available which are used as preplaced cells:

 --> Memory

--> Clock-gating cell

--> Comparator

--> MUX
* These Ip's have user defined locations and hence are placed in chip, before automated placement and routing and are called as pre-placed cells.
 
![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/1bda2c8e-ccd3-4c87-a77d-2e46f29105a9) 

**Decoupling Capacitors**

* swithcing of inputs at the logic cells from 0 to 1 needs to charge the capacitors at the gate, this helps in maintaining the logic level at 1.
* similarly the change in input from 1 to 0 , discharges the capacitor to ground.

* The input voltage of the ciruit should be inside the noise margin of the circuit, to expect a correct output.
* Decoupling capacitor supplies current to the circuit, when needed.
* Their primary role is to decouple the circuit from the power supply, ensuring that the circuit receives the necessary amount of current during transient events, such as switching activities.
* Decoupling capacitors are placed in close proximity to the Ip blocks.

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/cd330c4b-2587-45d8-90bc-be0f0afbbdb3)

**Power planning**

* While pre-placed macros or cells can have dedicated decoupling capacitors for local power stability, it's not practical to provide each block or standard cell with its own decap.
* Instead, a well-designed power planning strategy includes creating a power mesh to efficiently distribute power and ground (VDD and VSS) across the entire chip.
* Multiple GND and VDD points are strategically placed throughout the IC layout to ensure even power distribution.
* This even distribution reduces the likelihood of voltage drops and improves the efficiency of power delivery across the chip.
* We will have multiple Vdd and vss lines as shown in the below figure.



![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/fb5e1b66-8466-4cc5-962b-8151c6d19be2)

**Pin placement**

* Pin placement refers to the process of determining the locations and connections of input and output pins on an integrated circuit (IC) or semiconductor chip. 
* This critical step ensures proper functionality and performance of the chip while considering factors like signal integrity, power distribution, and manufacturing constraints. 
* Pin placement involves optimizing the arrangement of pins to minimize signal delays, reduce power consumption, and simplify the chip's layout for efficient manufacturing and testing.
* Pin placement depends on the inputs and functionality of the netlist
* clk port is the widest port, to make sure that it sees the least resistance


**Floorplanning and placement**

Run the following command 

```
run_floorplan
```

To view the floorplan in magic use

```
cd ~/OpenLane/designs/picorv32a/runs/RUN_2023.09.11_10.01.18/results/floorplan
magic -T /home/niharika/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def &

```
![Screenshot from 2023-09-11 16-09-52](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/f536d1f0-fe81-467e-b580-6eacda6ecc91)





</details>

<details>
<summary>
Library Binding and Placement
</summary>

**Netlist binding and Initial Placement**

* All the logic cells in the netlist are visualised as physical cells with a defined width and height for design
* A library has all the physical cells with each logic functionality with timing and area information.
* Library also has different physical variants of logic cells
* The logic cells of the generated netlist should not be placed over the pre-placed cells.

**Optimized placement**

* Logic cells are placed such that they are close to their respective inputs on the die.
* Optimized placement is done by placing, input flop close to the input port and output close to the output port.
* We estimate the wire length and capacitance and based on that we insert repeaters, if there is a long path from the input port to the flipflop
* Slew is dependent on the capacitance value, higher is the capacitance more is the slew.
* If the distance between the input port and flip-flop is not sufficient to maintain the signal integrity, we add buffers/repeaters in the path to reproduce input signal through the path without any loss of signal.
* The cells which work at very high frequency are made sure to be placed together, so that there is no delay produced from the wires between the logic cells


Optimised placed and routed cell

  ![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/390f0153-b6ac-4ac3-a20a-d6ead2bccc18)

  
**Placement**

Placement in openlane occurs in two stages: 
1. Global Placement: It finds optimal position for all cells which may not be legal and cells may overlap. Optimization is done through reduction of half parameter wire length[HPWL]. Overlap parameter should also reduce while we run placement.
2. Detailed Placement: It alters the position of cells placed in the global placement step to legalise them

use :

```
  run_placement
```

To view placement:

```
  cd ~/OpenLane/designs/picorv32a/runs/RUN_2023.09.14_10.50.04/results/placement
  magic -T /home/niharika/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def &
```
  

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/c65af9b4-3032-4538-93b9-d1b3e8bf2bc0)

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/9af0766e-44a2-43c0-b007-4d45df0f6a50)

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/c7874c51-9b69-4e56-89ba-dc266b66e6bc)

**Power ground generation is done post CTS in OpenLane**

</details>


<details>
<summary>
Cell design and characterization flows
</summary>
All the standard cells used in the design are placed in a library. We get a variant of standard cells in terms of functionality, area and power.

Each cell goes through **cell design flow** before being used in our design.

Cell design flow:
1. inputs : PDKs, DRC and LVS rules, Spice models , library and user defined specs.
2. design Step :Circuit design (decide the widths of tranistors) , Layout design (pmos and nmos network graph,Art of layout : Euler's path and stick diagram), Extraction of parasitics, Characterization (timing, noise, power).Stick diagram to layout according to inputs. After the layout, we get a defined library cell with specific height and width.
3. Outputs: CDL (circuit description language), LEF(defines size of the cell), GDSII, extracted SPICE netlist (.cir), timing, noise and power .lib files

**Standard Characterization flow**

1. Read in the model files 
2. Read the extracted spice netlist
3. recognize behaviour of the model
4. Read the sub-circuits of inverter
5. Attach necessary power source (Vdd, GND)
6. Apply the stimulus
7. Provide necessary output capacitance
8. Provide simulation command

We feed the above 8 steps as input the characterisation software GUNA, which gives the timing,noise and power models.

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/505e3dc5-e93c-4800-9da7-ae6fd3ff5907)

</details>


<details>
<summary>
General timing characterization parameters
</summary>

</details>

