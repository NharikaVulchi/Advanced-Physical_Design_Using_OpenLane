
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
</details>

**Introduction to all components of open-source digital ASIC design**

**Simplified RTL2GDS flow**

**Introduction to OpenLane and Strive Chipsets**

**Introduction to OpenLane detailed ASIC design flow**

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

