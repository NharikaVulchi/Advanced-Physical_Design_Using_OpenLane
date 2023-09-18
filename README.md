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
  
**Timing threshold** definitions are as follows:

* slew_low_rise_thr  --> 20% value
* slew_high_rise_thr --> 80% value
* slew_low_fall_thr  --> 20% value
* slew_high_fall_thr --> 80% value
* in_rise_thr        --> 50% value
* in_fall_thr        --> 50% value
* out_rise_thr       --> 50% value
* out_fall_thr       --> 50% value

(thr = threshold , in =input, out = output)

**Propogation delay and transition time**

Propogation delay : 

The time difference between when the input reaches 50% of its final value and when the output reaches 50% of its final value. Poor choice of threshold value will lead to negative delay values. If the output comes before the input, we get a negative delay, so we should choose a correct threshold value.


```
Propagation delay = time(out_*_thr) - time(in_*_thr)
```

Slew of the waveform specifies the delay of the wire capacitance. The propogation delay is also dependent on the slew. So to get a correct delay, we have to design the circuit to bring out the right slew

**Transition time**: The time that takes the signal to move between states is the transition time , where the time is measured between 10% and 90% or 20% to 80% of the signal levels.


</details>



## DAY 3 Library Cell using Magic Layout and ngspice characterization

<details>
<summary>
Labs for CMOS inverter ngspice simulations
</summary>
  
**IO Placer revision**

* We can make changes to the environment variables in the flow to observe the changes in our design.
* We change the I/O pins distance which are equidistant in the last run

In the below image, we can see that the pins are equidistant , now we change the environment variables

  ![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/f58938f9-e4e4-4a6c-868b-aa3da9bd72f1)

We use the below code in the flow.tcl file of /Openlane/configrations/ directory

```
set ::env(FP_IO_MODE) 2
```

**Spice deck creation for CMOS inverter** : 

* Component connectivity - Connectivity of the Vdd, Vss,Vin, substrate. Substrate tunes the threshold voltage of the MOS.
* Component Values - values of w/L PMOS and NMOS, Output load capacitor, Input Gate Voltage, supply voltage (ideally PMOS should be twice the width of NMOS)
* Identify the nodes - nodes are required to define spice netlist
* Give the simulation commands and Netlist description 

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/6586c000-bbc0-4c0c-8299-9be745a634c2)


Spice simulation of different w/L ratio for nmos and pmos

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/341de6a3-fdd4-4503-9015-5de95dc3371d)

Inference:
* Shape of the waveform is same : CMOS circuit is a very robust device and is widely used in circuit designing
* **Switching threshold** : A point where Vin=Vout , used in static behaviour evaluation. Both the PMOS and NMOS are ON, and there is direct current flowing from power to ground


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/26b872c7-28bd-4e20-91dc-ca4cdda63e7a)


Viewing the inveter layout:

```
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
magic -T ./libs/sky130A.tech sky130_inv.mag &
```


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/afbb0334-1311-415d-a8e5-79e0264d4d94)

</details>

<details>
<summary>
Inception of layout A CMOS fabrication process
</summary>

**16-mask CMOS process**

1. Selecting a substrate : The required substrate is chosen, for nMOS we choose, a p-type silicon substrate. Substrate doping should be less than **well** doping

2. Creating active region :
   * Small pockets of active regions are made on the p-substrate.
   * Deposition of 40nm SiO2 and 80nm of Si3n4 is made on the p-substrate.
   * Then a 1 um layer of photoresist is applied on the silicon layers.
   * Masks are used to protect the required regions from UV light (photolithography). Extra photoresist is washed away.
   * Areas exposed to the UV light chemically reacts and is edged off. 
   * The substrate is then placed in a oxidation furnace and the SiO2 layers which are exposed gets oxidised(LOCOS - Local oxidation of silicon) and the areas which are protected with Si3N4 are unoxidised and isolated.
   * Extra Si3N4 is stripped using hot phosphoric acid

3. N-well and P-well formation :
   * both the n-well and p-well formation can not be done together
   * p-well is formed using Boron in ion-implantation process. Boron atoms penetrate through oxide layer and moves into the p-substrate to form p-well
   * p-well is covered using a mask while we create a n-well
   * Phosphorous atoms are used in ion-implantation process to make a n-well.
   * pMOS is made in n-well tub and nMOS is made in p-well tub

4. Formation of **gate**
   * The gate is a pivotal CMOS transistor terminal that controls threshold voltages for transistor switching.
   * A polysilicon layer is deposited and photolithography techniques are applied to create NMOS and PMOS gates.
   * Important parameters for gate formation include oxide capacitance and doping concentration.

  5. Lightly doped drain formation :
     * drain is lightly doped due to two reasons - hot electron effect and short channel effect.
     * we follow the same steps as forming active regions to form drains

  6. Source and drain formation :
     * Thin oxide layers are added to avoid channel effects during ion implantation.
     * N+ and P+ implants are formed using arsenic implantation(75 kev energy) and high temperature annealing.
     * Annealing penetrates the active regions deeper into the substrate.

 7. Steps to form contacts and interconnects
    * Thin screen oxide is removed through etching in HF solution.
    *  Titanium deposition through sputtering is initiated.
    *  Heat treatment results in chemical reactions, producing low-resistant titanium silicon dioxide for interconnect contacts and titanium nitride for top-level connections, enabling local communication.

 8. Higher Level Metal Formation:
    * To achieve suitable metal interconnects, non-planar surface topography is addressed.
    * Chemical Mechanical Polishing (CMP) is utilized by doping silicon oxide with Boron or Phosphorus to achieve surface planarization.
    * TiN and blanket Tungsten layers are deposited and subjected to CMP.
    * An aluminum (Al) layer is added and subjected to photolithography and CMP.
    * This constitutes the first level of interconnects, and additional interconnect layers are added to reach higher-level metal layers.

 9. Dielectric Layer Addition:
     * a  stronger dielectric layer, Si3N4, is applied to safeguard the chip.

The final output after 16-Mask CMOS process

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/06a2a82c-4ca5-4f52-b957-8d50469d887d)

**Basic layers layout and LEF using inverter**

1. We see the layers which are required for CMOS inverter from the layout.
2. Gates of both PMOS and NMOS are connected together and fed to input, NMOS source connected to ground(here, VGND), PMOS source is connected to VDD(here, VPWR)
3. Drains of PMOS and NMOS are connected together and fed to output(here, Y).
4. The First layer in skywater130 is localinterconnect layer(locali) , above that metal 1 is purple color and metal 2 is pink color. 

  



</details>

<details>
<summary>
Sky130 Tech File Labs
</summary>
  
**Spice Extraction** : Use the below commands in tkcon to achieve .mag to .spice extraction:

1. Make an extract file .ext by typing extract all in the tkon terminal.
2. Extract the .spice file from this ext file by typing _ext2spice cthresh 0 rthresh 0_then ext2spice in the tcon terminal.
3. .spice file is created as shown below

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/5839ab03-fd1f-404c-8832-897c3a2d9f4a)

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/ba643a32-e37f-40e9-833e-6d52b874dbaf)

* For transient anaylsis, we would like to define these following connections and extra nodes for these in spice file
  1. VGND to VSS
  2. Supply voltage from VPWR to Ground - extra nodes here will be 0 and VDD with a value of 3.3V
  3. Sweep in pulse between A pin and VGND (0) Before, editing the file, make sure scaling is proper, we measure the value of the gride size from the magic layout and define using  .option scale=0.01u in the Deck file.

We comment the subckt since we are trying to input the controls and transient analysis also. Model names are changed to nshort_model.0 and pshort_model.0 according to the libs of nmos and pmos.

We run the ngspice simulation using the below code in the **~/vsdstdcelldesign** directory

```
ngspice sky130_inv.spice
tran 1n 20n
plot v(y) v(a)
```

The netlist and ouput:

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/cc045304-2dc8-45bf-b144-76b85c525fc5)

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/0a85123e-537d-47ba-8de1-ed24732ca961)

Rise time = 20% - 80% of final value = 0.064 ns
Fall time = 805 - 205 of final value = 0.042 ns

**Magic tool options and DRC rules**

The technology file is a setup file that declares layer types, colors, patterns, electrical connectivity, DRC, device extraction rules and rules to read LEF and DEF files. Magic layouts can be sourced from **opencircuitdesign.com** using the following commands :

```
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
tar xfz drc_tests.tgz
```
drc_tests file is created . Invoke magic and run the following command :

```
magic -d XR met1.mag
```


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/366307bd-06ae-42a4-8575-9348cda53c8a)


</details>

## DAY 4 Pre-layout timing analysis and importance of good clock tree

<details>
<summary>
Timing modeling using delay tables
</summary>

PnR tool does not need all informations from the .mag file like the logic part but only PnR boundaries, power/ground ports, and input/output ports. This is what a LEF file actually contains. So the next step is to extract the LEF file from Magic. But first, we need to follow guidelines of the PnR tool for the standard cells:

1. The input and output ports lie on the intersection of the horizontal and vertical tracks (ensure the routes can reach that ports).
2. The width of the standard cell must be odd multiple of the tracks horizontal pitch and height must be odd multiples of tracks vertical pitch.

use the commands inside the tkon windonw:

```
grid on
grid 0.46um 0.34um 0.23um 0.17um
```
* The grids show where the routing for the local-interconnet layer can only happen, the distance of the grid lines are the required pitch of the wire
* The LEF file contains the cell size, port definitions, and properties which aid the placer and router too

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/17c81990-a05f-484d-9401-2165016a83dc)

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/9c438085-c2a5-4ee0-9244-bd8b346a9f3a)

**Port definition**

* Port definition is required when we create the lef file
* In Magic Layout window, first source the .mag file for the inverter. Select the port and then go to Edit --> Text 
* When we double press S at the I/O lables, the text automatically takes the string name and size. Ensure the Port enable checkbox is checked and default checkbox is unchecked as shown in the figure.
* For ports we make the sticky label as **locali** and for the Vpwr and GND we make it as **metal1** because they are attached to metal layer.
* Our inverter ports are already defined.

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/e817db5c-c609-406f-a659-99db688f124b)


**Port class and port attributes**

```
port A class input
port A use signal    // select port A

port Y class output
port Y use signal    //select y

port VPWR class inout
port VPWR use power    //select VPWR

port VGND class inout
port VGND use ground    //select VGND
```
Creating a lef file : type this command **lef write** in the tckon window, we will see a lef file in the /home/niharika/vsdstdcelldesign directory

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/3a2fe531-a13f-4dc8-a80b-10f4d16a59d2)



Steps to include custom cell in ASIC:

* We have created a custom standard cell in previous steps of an inverter. 
* Now we copy lef file, sky130_fd_sc_hd_typical.lib, sky130_fd_sc_hd_slow.lib & sky130_fd_sc_hd_fast.lib to src folder of picorv32a from libs folder vsdstdcelldesign. Then modify the config.json as follows

```
{
  "DESIGN_NAME": "picorv32",
  "VERILOG_FILES": "dir::src/picorv32a.v",
  "CLOCK_PORT": "clk",
  "CLOCK_NET": "clk",
  "FP_SIZING": "relative",
  "GLB_RESIZER_TIMING_OPTIMIZATIONS": true,
  "LIB_SYNTH" : "dir::src/sky130_fd_sc_hd__typical.lib",
  "LIB_FASTEST" : "dir::src/sky130_fd_sc_hd__fast.lib",
  "LIB_SLOWEST" : "dir::src/sky130_fd_sc_hd__slow.lib",
  "LIB_TYPICAL":"dir::src/sky130_fd_sc_hd__typical.lib",
  "TEST_EXTERNAL_GLOB":"dir::/src/*",
  "SYNTH_DRIVING_CELL":"sky130_vsdinv",
  "pdk::sky130*": {
    "FP_CORE_UTIL": 35,
    "CLOCK_PERIOD": 24,
    "scl::sky130_fd_sc_hd": {
      "FP_CORE_UTIL": 30
    }
  }
}
```

Run OpenLane using the following commands:

```
prep -design picorv32a

//new additional commands for custom cell

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```


We can see changes in the synthesis file :



![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/9df1a85d-f38c-4665-868c-beeaa22fd95a)


after doing placement and flooplan we can view our placement in magic using:

```
niharika@niharika-HP-Pavilion-Laptop-15-eh1xxx:~/vsdstdcelldesign$  magic -T /home/niharika/vsdstdcelldesign/libs/sky130A.tech lef read /home/niharika/OpenLane/designs/picorv32a/runs/RUN_2023.09.18_11.46.06/tmp/merged.nom.lef def read /home/niharika/OpenLane/designs/picorv32a/runs/RUN_2023.09.18_11.46.06/results/placement/picorv32a.def &
```

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/46ea324d-ae36-4fb9-8170-0a641542f2f7)

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/e0a656b7-499c-40ec-87b1-b967d83c952a)

Now we see the custom cell in our placement:

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/47f18711-0647-49fc-a915-015544437620)

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/f52d8b50-56f3-4d4c-b5a5-311d639a83b2)


**Delay Tables**

We encounter several types of delays in ASIC design. They are as follows:
* Gate delay or Intrinsic delay
* Net delay or Interconnect delay or Wire delay or Extrinsic delay or Flight time
* Transition or Slew,Propagation delay,Contamination delay.
* Wire delays or extrinsic delays are calculated using output drive strength, input capacitance and wire load models. Other delays are intrinsic properties of each and every gate.
* Delays are interdependent on different electrical properties.Input capacitance of the logic gate is a function of output state, output loads and input slew rate, Internal timing arcs and output slew rate is a function of switching inputs, Capacitance of the wire is dependent on frequency. 


![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/7b99ea58-f6d4-40d5-9979-4a8a0e8e4c7c)

</details>

<details>
<summary>
Timing analysis with ideal clocks using OpenSTA
</summary>

1. **Setup time** is the required time duration that the input data is stable before the triggering-edge of the clock. 
2. If data is changing within this setup time window, the input data might be lost and not stored in the flip-flop as metastability might occur.
3. Metastability: When setup and hold time requirements are violated, the flip-flop state becomes unstable, and after an unpredictable duration, the state of the flip-flop can settle either way (1 or 0). This scenario is known as metastability.
4. As shown in the following figure, output Q1 passes through the slow logic and arrives late at the input D2 of FF2, which leads to setup time violation and the loss of the new data. Thus combinational delay must be less than **clock frequency - setup time**

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/0647e75e-2abb-4cf2-b567-da9c3ed99e3a)

1. **Clock jitter** is a characteristic of the clock source and the clock signal environment.
2. It can be defined as “deviation of a clock edge from its ideal location.” Clock jitter is typically caused by clock generator circuitry, noise, power supply variations, interference from nearby circuitry etc. Jitter is a contributing factor to the design margin specified for timing closure.The below figure explains clock jitter

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/eac415ef-c85a-4ffc-95c9-3f65db8bebc2)

**Configuring OpenSTA tool**

Timing analysis is carried out outside the openLANE flow using OpenSTA tool. For this, pre_sta.conf is required to carry out the STA analysis. Invoke OpenSTA outside the openLANE:

```
sta pre_sta.conf
```


</details>

<details>
<summary>
Clock tree synthesis TritonCTS and signal integrity
</summary>

1. The purpose of building a clock tree is to enable the clock input to reach every element and to ensure a zero clock skew.
2.  H-tree is a common methodology followed in CTS. Before attempting a CTS run in TritonCTS tool, if the slack was attempted to be reduced in previous run, the netlist may have gotten modified by cell replacement techniques. T
3.  Therefore, the verilog file needs to be modified using the write_verilog command. In this stage clock is propagated and make sure that clock reaches each and every clock pin from clock source with mininimum skew and insertion delay. Inorder to do this, we implement H-tree using mid point strategy.

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/d9cbef07-d6ee-4bb2-9e80-c710d8ef5653)


**Balanced Tree CTS**: In a balanced tree CTS, the clock signal is distributed in a balanced manner, often resembling a binary tree structure. This approach aims to provide roughly equal path lengths to all clock sinks (flip-flops) to minimize clock skew. It's relatively straightforward to implement and analyze but may not be the most power-efficient solution.

**H-tree CTS**: An H-tree CTS uses a hierarchical tree structure, resembling the letter "H." It is particularly effective for distributing clock signals across large chip areas. The hierarchical structure can help reduce clock skew and optimize power consumption.

**Star CTS**: In a star CTS, the clock signal is distributed from a single central point (like a star) to all the flip-flops. This approach simplifies clock distribution and minimizes clock skew but may require a higher number of buffers near the source.

**Global-Local CTS**: Global-Local CTS is a hybrid approach that combines elements of both star and tree topologies. The global clock tree distributes the clock signal to major clock domains, while local trees within each domain further distribute the clock. This approach balances between global and local optimization, addressing both chip-wide and domain-specific clocking requirements.


**CrossTalk** is a disturbance caused by the electric or magnetic fields of one telecommunication signal affecting a signal in an adjacent circuit. Essentially, every electrical signal has a varying electromagnetic field. Whenever these fields overlap, unwanted signals -- capacitive, conductive or inductive coupling -- cause electromagnetic interference (EMI) that can create crosstalk. Overlap can occur with structured cabling, integrated circuit design, audio electronics and other connectivity systems. For example, if there are two wires in close proximity that are carrying different signals, their currents will create magnetic fields that induce a weaker signal in the neighboring wire. 

Impact: Crosstalk is a significant concern in VLSI design due to the high integration density of components on a chip. Uncontrolled crosstalk can lead to data corruption, timing violations, and increased power consumption. Mitigation: VLSI designers employ various techniques to mitigate crosstalk, such as optimizing layout and routing, using appropriate shielding, implementing proper clock distribution strategies, and utilizing clock gating to reduce dynamic power consumption when logic is idle


**Clock Net Shielding**

Shielding is done so as to prevent gltch. Shields are connected to VDD or GND. The shields do not switch.VLSI designers may use shielding techniques to isolate the clock network from other signals, reducing the risk of interference. This can include dedicated clock routing layers, clock tree synthesis algorithms, and buffer insertion to manage clock distribution more effectively. Clock Domain Isolation: VLSI designs often have multiple clock domains. Shielding and proper clock gating help ensure that clock signals do not propagate between domains, avoiding metastability issues and maintaining synchronization.

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/0379de4f-c8a1-46e9-bf49-12e5e8379953)

**LAB**

Before attempting to run CTS in TritonCTS tool, if the slack was attempted to be reduced in previous run, the netlist may have gotten modified by cell replacement techniques. Therefore, the verilog file needs to be modified using the write_verilog command. Then, the synthesis, floorplan and placement is run again. To run CTS use the command: **run_cts**

 We use OpenROAD within the openLANE flow tp analyse Setup and hold time slacks :


```
 openroad
read_lef /home/niharika/OpenLane/designs/picorv32a/runs/RUN_2023.09.18_11.46.06/tmp/merged.nom.lef
read_def /home/niharika/OpenLane/designs/picorv32a/runs/RUN_2023.09.18_11.46.06/results/cts/picorv32a.def
read_verilog /home/niharika/OpenLane/designs/picorv32a/runs/RUN_2023.09.18_11.46.06/results/synthesis/picorv32a.v
write_db pico_cts.db
link_design picorv32a
read_liberty $::env(LIB_SYNTH_COMPLETE)
read_sdc /home/niharika/OpenLane/designs/picorv32a/src/my_base.sdc
set_propagated_clock (all_clocks)
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```

Clock skew is chekced using the following command : **report clock_skew -setup**

</details>



## DAY 5 Final steps for RTL2GDS using tritonRoute and openSTA

<details>
<summary>
Routing and Design Rule Check(DRC)
</summary>

**Maze Routing**

1. Routing is the process of creating physical connections based on logical connectivity. Signal pins are connected by routing metal interconnects.
2.  Routed metal paths must meet timing, clock skew, max trans/cap requirements and also physical DRC requirements.
3.  In grid based routing system each metal layer has its own tracks and preferred routing direction which are defined in a unified cell in the standard cell library.
4.  there are four steps of routing :
    * global routing
    * track assignment
    * detail routing
    * search and repair
5. The Maze Routing algorithm, such as the Lee algorithm, is one approach for solving routing problems. In this method, a grid similar to the one created during cell customization is utilized for routing purposes.
6.  The Lee algorithm starts with two designated points, the source and target, and leverages the routing grid to identify the shortest or optimal route between them. The algorithm assigns labels to neighboring grid cells around the source, incrementing them from 1 until it reaches the target (for instance, from 1 to 7).
7.  Various paths may emerge during this process, including L-shaped and zigzag-shaped routes. The Lee algorithm prioritizes selecting the best path, typically favoring L-shaped routes over zigzags.
8.  If no L-shaped paths are available, it may resort to zigzag routes. This approach is particularly valuable for global routing tasks.

**Design Rule check**

A physical design technique called Design Rule Checking (DRC) is used to check whether a chip layout complies with a number of requirements set out by the semiconductor manufacturer. Each semiconductor manufacturing process will have its own set of guidelines and margins to ensure that normal manufacturing variability won't lead to chip failure. below mentioned are few examples of DRC : Minimum width and spacing for metal, Minimum width and spacing for via, Fat wire Via keep out Enclosure, End of Line spacing, Minimum area, Over Max stack level, Wide metal jog, Misaligned Via wire, Different net spacing, Special notch spacing, Shorts violation, Different net Via cut spacing, Less than min edge length

</details>

<details>
<summary>
Power Distribution Networking and Routing
</summary>
  
**PDN generation** is not a component of the floorplan run in OpenLANE, in contrast to the typical ASIC flow. After the CTS and post-CTS STA analysis, PDN must be prepared.

**gen_pdn** is the command used to generate power distribution network.

1. The power distribution network must use design_cts.def as the input def file.
2. This creates a grid and band for Vdd and floor. These are placed around the standard cell. A standard cell is designed so that its height is a multiple of the distance between its Vdd and ground bar.
3. The slope here is 2.72. Power can be supplied to standard cells only if the above conditions are met. The chip is powered via a power connection. There is one for Vdd and one for Gnd Current flows from the pad to the ring through the through hole. The strap is connected to the ring.
4. The Vdd band is connected to the Vdd ring and the Gnd band is connected to the Gnd ring. Has horizontal and vertical support Now we need to supply power from the tape to the standard cell.
5. Straps are connected to standard cell rails If a macro is present, the strap is attached to the macro's ring via the macro pad and her PDN for the macro is pre-created. Straps and rails have definitions.
6. In this design, the tabs are on metal layers 4 and 5, and the standard cell bars are on metal layer 1. Connect layers with vias as needed.

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/a4871453-e824-4151-9d02-00300b6650ae)


**Routing** is the process of physically connecting signal pins using metal layers. Following CTS and optimisation, routing is the phase in which precise connections between standard cells, macros, and I/O pins are made. The logical connections provided in the netlist are used to determine the creation of electrical connections in the layout utilising metals and vias.

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/e2065337-98c0-4c79-b75c-f76ec06a295c)


OpenLANE uses the TritonRoute tool for routing. There are 2 stages of routing:
1. Global routing: Routing region is divided into rectangle grids which are represented as course 3D routes (Fastroute tool).
2. Detailed routing: Finer grids and routing guides used to implement physical wiring (TritonRoute tool).


</details>

<details>
<summary>
TritonRoute Features
</summary>
  
**Feature-1 Honors pre-processed route guides**

1. Adherence to Pre-Processed Route Guides: TritonRoute places significant emphasis on following pre-processed route guides.
2. This involves several actions: Initial Route Guide Analysis: TritonRoute analyzes the directions specified in the preferred route guides. If any non-directional routing guides are identified, it breaks them down into unit widths.
3. Guide Splitting: In cases where non-directional routing guides are encountered, TritonRoute divides them into unit widths to facilitate routing.
4. Guide Merging: TritonRoute merges guides that are orthogonal (touching guides) to the preferred guides, streamlining the routing process.
5.  Guide Bridging: When it encounters guides that run parallel to the preferred routing guides, TritonRoute employs an additional layer to bridge them, ensuring efficient routing within the preprocessed guides.
6.  Route guides are followed to satisfy inter- guide connectivity. Requirements of preprocessed route guides: Must have unit width and must be in the predefined direction. Directions of metal ensures minimum capacitances

   ![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/0f7dc47f-715d-4787-a0c2-dd2e9f53f05e)

**feature-2 inter-guide connectivity , Intra and inter layer routing****
Two guides are connected if They are on the same metal layer with touching edges or they are on neighbouring metal layers with a non zero vertically overlapped area.

Each unconnected terminal should have its pin shape overlapped by a route guide

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/3aec79a2-bc3e-420a-875a-2db12b9fac7c)


**Tritonroute run for routing**

We start routing with : **run_routing** 

This will do both global and detailed routing, this will take multiple optimization iterations until the DRC violation is reduced to zero. The zeroth iteration has 27426 violations and only at the 8th iteration was all violations solved. 

![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/d8480acc-2661-472d-a295-52ee9aac1109)

We can view layout in magic tool 

 magic -T /home/niharika/vsdstdcelldesign/libs/sky130A.tech lef read tmp/merged.nom.lef def read results/routing/picorv32a.def & 

 ![image](https://github.com/NharikaVulchi/Advanced-Physical_Design_Using_OpenLane/assets/83216569/f019e182-30d4-4046-9678-c249de688778)

</details>





















