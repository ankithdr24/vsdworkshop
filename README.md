# DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING

# <h1 id="header-1">Day 1 -Inception of open-source EDA, OpenLANE and sky130 PDK</h1>	 
## <h1 id="header-1_1">How to talk to computers?</h1>
### <h1 id="header-1_1_1">Introduction to QFN-48 Package, chip, pads, core, die and IPs</h1>

**Arduino Board**:- An Arduino board serves as a microcontroller, distinguished by its integrated microprocessor chip (highlighted in the encircled region) that interfaces with the surrounding circuitry. The development of this chip, from high-level abstraction to the final fabrication stage, adheres to the RTL to GDSII design methodology. Arduino, as a platform, comprises a physical, programmable circuit board and a software component, the Integrated Development Environment (IDE), enabling users to write and upload code to the board from a computer.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/ff3696b5-cf69-41dd-86e5-160875e8eaba)


#### Chip components 
i **Pads:** Through which we can send the signal inside the chip.

ii **Core:** Place where all the logic gates are fixed.

iii **Die:** Present at the corner. it is the size of the entire chip.

**EX. RISC-V SoC**:- Key components like SRAM, SoC, ADC, DAC, and SPI are considered foundry intellectual property (IP). The fabrication of all integrated circuits depends on foundries, which employ techniques such as deposition and lithography for chip manufacturing.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/0900c16a-29b9-47fd-84bd-28b7249a2938)


### <h1 id="header-1_1_2">Introduction to RISC-V</h1>
**RISC-V** refers to the fifth generation of Reduced Instruction Set Computer (RISC) architectures developed at the University of California, Berkeley. This open-standard instruction set architecture (ISA) is built upon well-established RISC principles. A key differentiator for RISC-V is its availability under open-source licenses, meaning there are no fees associated with its use, unlike most other ISA designs. Consequently, several companies are now providing or have announced RISC-V hardware, and open-source operating systems with RISC-V support are readily available. Furthermore, various popular software toolchains also support this instruction set.

The RISC-V instruction set is engineered for broad applicability. Its foundational instruction set features a consistent 32-bit length with natural alignment. The ISA also accommodates variable-length extensions, allowing instructions to comprise any number of 16-bit segments. The specification for the instruction set outlines both 32-bit and 64-bit address space variations. While a 128-bit flat address space variant is described as an extrapolation, its specification remains "not frozen." This intentional decision reflects the limited practical experience with such expansive memory systems to date.
Chip is connected to the package with the help of bond wires.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/d3bfdac2-c95c-49dd-bdab-223a42692197)

### RISC V SoC CHIP
![RISC SoC Chip](day%2001/RISC%20SoC%20Chip.jpeg)

The central component is a **RISC SoC (System-on-Chip) chip**. This chip integrates several key functional blocks, which the image labels as "Macros" and "Foundry IPs," indicating pre-designed and validated components.

Prominently displayed within the SoC are a **GPIO (General Purpose Input/Output) bank** and an **SRAM (Static Random-Access Memory)** block. The GPIO bank suggests the chip's ability to interface with external devices through various digital pins, as seen with the numerous "gpio" labels surrounding the chip. The SRAM block provides fast, volatile memory for data storage during operation.

Additionally, the chip incorporates other "Foundry IPs" essential for its functionality. These likely include Analog-to-Digital Converters (ADCs) and Digital-to-Analog Converters (DACs) for handling analog signals, and an SPI (Serial Peripheral Interface) module, indicated by the "SPI" label and associated pins, for serial communication with peripherals. The presence of these IPs alongside the RISC core signifies a comprehensive, integrated solution designed for a range of embedded applications.

### <h1 id="header-1_1_2">From Software Applications to Hardware</h1>
![Application to Hardware flow](day%2001/Application%20to%20Hardware%20flow.jpeg)

This section explores the execution of applications on a computing system, detailing the flow from application software through system software to the hardware chip. Applications first interact with the system software, which is responsible for translating the entire program into binary code. Within the system software, several layers facilitate this process: the Operating System (OS), Compiler, and Assembler. 

The OS manages fundamental tasks such as input/output (I/O) operations, memory allocation, and low-level system functions. The Compiler receives high-level programming languages (like C, C++, or Java) from the OS and translates them into hardware-specific instructions. Subsequently, the Assembler converts these instructions into binary numbers. 

This binary data is then sent to the hardware, which executes the received functions and generates the corresponding output. Essentially, instructions serve as an abstract interface between high-level programming languages and the underlying hardware.

### Stopwatch App: A Journey from C Code to Chip Execution
![Stopwatch app](day%2001/Stopwatch%20app.jpeg)
This diagram illustrates the practical application of the software-hardware interaction pipeline, using a simple "Stop Watch app" as an example.
- **Application Layer (Eg. Stop Watch app):** At the top, we see the user-facing **Stop Watch app** displaying "00:00:03.70", which is the desired output of the application.
- **Compiler Input (a 'C' function for stopwatch):** The process begins with the human-readable source code. Here, a "C" language function for the stopwatch is shown. This code includes standard libraries (`stdio.h`, `time.h`) and defines a `main` function that implements the stopwatch logic, including updating time, printing to the screen, and handling delays (`sleep(1)`).
- **System Software:** This layer, encompassing the **Operating System (OS)** (like Windows 7 or Linux depicted), acts as the primary orchestrator. As before, the OS handles fundamental tasks such as managing I/O operations (like displaying the time on the screen), allocating memory for the program, and overseeing low-level system functions essential for the stopwatch to run.
- **Compiler:** The "C" source code is then fed into the **Compiler**. The compiler translates this high-level code into lower-level instructions. The output, often an executable file (like `*.exe`), contains these machine-understandable instructions (`Instr1`, `Instr2`, etc.), which are specific to the target hardware architecture (in this case, implied to be RISC-V from previous context).
- **Compiler and Assembler Output (A RISC-V assembly language program):** The instructions from the compiler are further processed by an assembler (or the compiler's backend directly generates assembly). The diagram explicitly shows a representation of the RISC-V assembly language. This is a human-readable form of machine code, where instructions like `addi`, `sd`, `lui`, `jalr` are seen alongside memory addresses (e.g., `0: 7136`, `4: sd`). This assembly code directly corresponds to the binary instructions the hardware will execute.
- **Hardware (Chip Layout):** Finally, the assembly instructions are converted into pure binary code and sent to the **Hardware**, specifically the **Chip Layout**. This intricate physical design of the integrated circuit executes the binary instructions. The diagram shows the physical pathways and components on the chip. The hardware processes the binary input (implied by the assembly) and produces the desired output, which, in this example, would be the updated time displayed by the stopwatch app on the screen.

This example clearly demonstrates how a high-level application concept like a stopwatch is progressively transformed through various software layers into low-level instructions that the physical hardware can understand and execute.

 ## <h1 id="header-1_2">Soc design and OpenLANE</h1>
### <h1 id="header-1_2_1">Introduction to all components of open-source digital asic design</h1>
![digital_asic_flow](day%2001/digital_asic_flow.jpeg)

To design Digital ASIC, few tools or things which are required from the day one. These are

**RTL Design
EDA tools
PDK data**
**what is RTL design?**
In digital circuit design, register-transfer level (RTL) is a design abstraction which models a synchronous digital circuit in terms of the flow of digital signals (data) between hardware registers, and the logical operations performed on those signals.for this designs many open sorces are available. like, librecores.org, opencores.org, github.com, etc...

**What is EDA tools?**
The term Electronic Design Automation (EDA) refers to the tools that are used to design and verify integrated circuits (ICs), printed circuit boards (PCBs), and electronic systems, in general. many open sorces tools are available like Qflow, OpenROAD, OpenLANE, etc...

**What is PDK Data?**
PDK is process design kit. It is interface between FAB and design. This data is collections of files like,

process design rules: DRC, LVS, REX
Digital standerd cell libreries
i/o librerirs
etc.....
which are used to model a fabrication process for the EDA tools used to design an ICs. for example, in 2020, google release the open source PDK for FOSS 130nm production with the skywater technology. But right now it is at cutting age of the 5 nm also. But in many applications, the advance node is not required, and the cost of advanced node is also high as compared to 130nm processors. This 130nm processors are also fast processor. for example,

intel: P4EE @3.46 GHz(Q4'o4)

sky130_OSU (single cycle RV32i CPU) pipeline version can achieve more than 1 GHz clock.

### <h1 id="header-1_2_2"> Simplified RTL2GDS flow</h1>

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/bfa1cad8-6338-4306-8ce2-446f7bec8c92)

**Step 1. Synthesis**:-  In the synthesis, the design RTL is translated to a circuit out from the SCL. The resultant circuit is describes in HDL and usualy refered to the gate level netlist. the gate level netlist is functionaly equivelent to the RTL. "standard Cells" have regular layouts like Electrical. HDL,SPICE

![[WhatsApp Image 2025-07-14 at 17.25.41_e8d18911.jpg]]

**Step 2. Floor/Power Planning**:-The main objective here is that to plan silicon area and distribute the power to the whole circuit. In the chip floor planning, the partition chip die between different system building blocks and place the i/o pads. In micro floor planning, we define the dimensions, pin locations, rows.
In power planning, the power network is connstructed. tipically, the chip is power by multiple VDD and GND. so, total components are connected to power supply horizontaly and vertically by metal streps. here parallel structures are used to reduce the resistance. To address the electromagnetization problem, power distribution network uses upper metal leyers, which are thicker than lower metal layers. Hence have less resistance.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/4037aad0-4da5-477f-a46f-0cf62d8ea68c)

**Step 3. Placement**:- In this process, we place the gate level netlist on the floor planning rows, alligned with the sites. cells should be placed very closed to eachother to reduce the interconnnect delay. Usually placement is done in 2 steps:

**Global placement**:- It is very first stage of the placement where cells are placed inside the core area for the first time looking at the timing and congestion. Global Placement aims at generating a rough placement solution that may violate some placement constraints while maintaining a global view of the whole Netlist.

**Detailed placement**:- In detailed placements, we determined the exact route and layers for each netlist. the objective of detailed placement is valid routing, minimize area and meet timing constrains. Additional objective is minimum via and less power.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/4834af5e-a20a-48b6-987a-4b2d7102d787)

**Step 4. Clock Tree Synthesis**:- Clock distribution is a crucial step preceding signal routing. In clock synthesis, the clock signal is propagated to all sequential components like flip-flops, registers, Analog-to-Digital Converters (ADCs), and Digital-to-Analog Converters (DACs). The resulting clock network typically forms a tree-like structure, where the clock source serves as the root and the clocked elements are the terminal leaves. The synthesis process demands careful execution to ensure minimal clock skew and a robust network configuration. Specialized low-skew global routing resources are employed for clock signals to mitigate skew. Microsemi, for instance, offers various global routing capabilities that notably reduce skew. Standard clock tree topologies include H-tree and X-tree designs.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/32d071b0-b762-4670-af57-708abb963744)

**Step 5. Routing**:- After routing the clock, the signal routing comes. Making physical connections between signal pins using metal layers are called Routing. Routing is the stage after CTS and optimization where exact paths for the interconnection of standard cells and macros and I/O pins are determined. There are two types of nets in VLSI systems that need special attention in routing:

Clock nets
Power/Ground nets
The sky130 PDK defines the 6 routing leyers. the lowest leyer is called local interconnect layer (titanium nitride layer). Other five layers are alluminium layersIn the proccess of routing, metal trackes forms a routing grids and these grids are huge. so, devide and conquer approach is use for routing. The two types of routing is used:

**Global routing:** Generates the routing guides

**Detailed Routing:** Uses the routing guides to implement the actual wiring.

![Global routing and Detailed routing](day%2001/Global%20routing%20and%20Detailed%20routing.jpeg)
**Step 6. Sign Off**:- Once the routing is done, we can construct the final layout. This final layout will goes under the verification. Two types of verifications are there:

Physical verification: Here design rule checking will done and it will check the final layout and owners layout
Timing Verification: Here Static Timing Analysis will done.


### <h1 id="header-1_2_3">Introduction to OpenLANE and Strive chipsets</h1>

OPENLANE provides an automated RTL-to-GDSII flow, utilizing multiple tools such as OpenROAD, Yosys, Magic, Netgen, Fault, CVC SPEF-Extractor, CU-GR, Klayout, and various scripts for design exploration and optimization. This flow began as an open-source project for authentic open-source tape-out endeavors. striVe signifies a line of entirely open SoCs: featuring an Open PDK, Open EDA, and Open RTL.

![Openlane](day%2001/Openlane.jpeg)

striVe SoC Family

![striVe Family](day%2001/striVe%20Family.jpeg)

The main goal of OPENLANE is to produce a clean GDSII with no human intervation (no-human-in-the-loop). here the meaning of clean is that:

No LVS violations

No DRC Violations

No timing Violations

OPENLANE is tuned for skyWter130nm open PDK. it can be used to harden Macros and chips.there is two mode of operation
Autonomus : it is the push botton flow. with the push botton , it is a some time base design and due to this push botton, we get final GDSII

interactive : here we can run comamds and steps one by one.

It has large number of design examples(43 designs with their best configurations).


### <h1 id="header-1_2_4">Introduction to OpenLANE detailed ASIC design flow</h1>

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/f46800c7-53cc-4541-b8eb-fd3fe9422cc6)

The above block diagram shows the OpenLANE detailed ASIC design flow.

**Synthesis Exploration**

![Synthesis Exploration](day%2001/Synthesis%20Exploration.jpeg)

This graph illustrates **synthesis exploration** by plotting **design area (μm2) against circuit delay (ps)** for different implementation strategies (S1-S8). Each point represents a unique design trade-off. The goal is to find designs with **lower area and lower delay**, effectively identifying optimal solutions on the performance-area frontier.

**Design Exploration and OpenLANE regresssion testing**

![Design Exploration and OpenLane Regression testing](day%2001/Design%20Exploration%20and%20OpenLane%20Regression%20testing.jpeg)

The design exploration utility is also used for regression testing(CI). we run OpenLANE on ~ 70 designs and compare the results to the best known ones.

**DFT(Design for Test)**
it perform scan inserption, automatic test pattern generation, Test patterns compaction, Fault coverage, Fault simulation.After that physical implementation is done by OpenROAD app. physical implementation involves the several steps:

![DFT](day%2001/DFT.jpeg)

Floor/Power Planning

End Decoupling Capacitors and Tap cells insertion

Placements: Global and Detailed

Post Placement Optimization

Clock Tree synthesis (CTS)

Routing: Global and Detailed

Netlist changes occur frequently, notably during Clock Tree Synthesis (CTS) and Post-Placement Optimization, requiring verification. Formal verification, often utilizing tools like LCE (Yosys), is crucial to ensure functional equivalence after netlist modifications. Addressing antenna rule violations is also key: during fabrication, metal wire segments can behave as antennas, collecting charges. This charge accumulation can lead to damage to transistor gates, making it vital to prevent such occurrences in the manufacturing flow.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/be8630b5-1b3d-4061-a636-8ecbbed1669e)


Mitigating this issue involves restricting wire lengths, a task commonly handled by the router. If the router cannot resolve the problem, two alternatives are available: either bridging, which connects segments via a higher metallization layer, or adding antenna diode cells. These specialized diodes, sourced from the SCL, effectively drain excess charges, thereby protecting transistor gates from potential damage during the fabrication process.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/c1ff8bd1-2951-44ae-8a4e-aa31d63e0322)


OpenLANE adopts a proactive strategy for antenna rule management. Initially, placeholder antenna diodes are inserted beside every cell input following placement. Subsequently, an antenna checker analyzes the routed layout. When this checker flag a violation at a cell input pin, the temporary diode cell is then swapped with a functional one.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/9448d09a-5647-4b60-986c-d1e8f8f16309)


**Static Timing analysis(STA)**
It involves the interconnect RC Extraction(DEF2SPEF) from the routed layout, followed by STA on OpenSTA(OpenROAD) tool. resulting report will shows the timing violations if any violations is there.

**Physical Verification (DRC and LVS)**
Magic is used for design Rules checking and SPICE Extraction from Layout. Magic and Netgen are used for LVS.



## <h1 id="header-1_3">Get familiar to open-source EDA tools</h1>
### <h1 id="header-1_3_1">OpenLANE Directory structure in detail</h1>
**Basic Linux Commands**

**cd** : opens the particular folder

**ls** : lists the content of the folder

**pwd** : shows the present working directory

**mkdir** : to make a new directory

**command --help** : shows the complete use that command

**clear** : clears the terminal screen

The above Linux commands are performed in terminal and the same as been shown in the figure below.

![Linux Commands](day%2001/Linux%20Commands.jpeg)

Here we are working in Sky130_fd_sc_hd PDK varient. where, "sky130" is process name or node name."fd" is a foundary name (skyWater foundary)."sc" means standerd cell librery files and the last one "hd" stands for high density(basically one type of varient).

Sky130_fd_sc_hd varient contains many technology files like verilog, spice, techlef, meglef,mag,gds,cdl,lib,lef,etc. (techlef file contains the layer information).


### <h1 id="header-1_3_2">Design Preparation Step</h1>
Accessing OpenLANE requires using the `flow.tcl` script to direct the automated design sequence. By incorporating the "interactive" switch, users can execute the process incrementally, step by step. Conversely, running the script without this switch will carry out the entire RTL to GDSII flow in one go. Once OpenLANE is successfully launched, a visible change in the command prompt will signify its operational status.

![OpenLane interactive](day%2001/OpenLane%20interactive.jpeg)

Now we have to input all the packages which required to run the flow.

![pacakages](day%2001/pacakages.jpeg)

Now, here we are ready to execute the command.

Within OpenLANE's design directory, numerous pre-built designs, numbering around 30 to 40, are accessible. Any of these can be opened; for instance, here we're examining the `picorv32a.v` design. This particular design folder contains various associated files, such as `src` and `config.tcl`. The `config.tcl` file is comprehensive, detailing every aspect of the design, including critical information like enrollment particulars, specified clock period, and clock port details, among others.

![configtcl](day%2001/configtcl.jpeg)

Here we can see that the time period is set to the 5.00 nsec. but is we see in the openlane sky130_fd_sc_hd folder, the period is set about 24 nsec. so it is not override to the main file. If it override then give first priority to the main folder.

Now, in openlane, we are going to run the synthesis, but before synthesis, we have to prepare design setup stage. for that command is ``` prep -design picorv32a```

![prepration complete](day%2001/prepration%20complete.jpeg)

so, here it is shown that preparation is completed.


### <h1 id="header-1_3_3">Review files after design prep and run synthesis</h1>

After completing the preparation, in the picorv32a file, the run terictory is created. Inside the folder, Today's date is created. so in this terictory some folders are available which is required for openlane.

In the tmp file, merged.lef file is available which was created in preparation time. if we open this merged.lef file, we get all the wire or layer level and cell level information.


![[Pasted image 20250714181854.png]]

While, in the result folder is empty because till we have not run anything and in the report folder all the folders are there about synthesis, placement, floorplanning,cts,routing,magic,lvs.

now here also one config.tcl file is available similar like design folder. But this config.tcl file contains all default parameter taken by the run.

when we make some change in the origional configuration and then we run, for example if we make a change in core utilization in the floorplanning and then we run the floorplanning, at this time in the congig.tcl file, the core utility will change and by cross checking it we can check that the modification is reflected in the exicution or not.

Now coming to the openlane, we are going to run the synthesis. for that command is run synthesis which is shown below. It will take some 4-5 mnts to run the synthesis and finally synthesis will complited.

```bash
run_synthesis
```
The image below shows our synthesis runs successfully. 

![Synthesis Successful](day%2001/Synthesis%20Successful.jpeg)

### <h1 id="header-1_3_5">Steps to characterize synthesis results</h1>

From the data of synthesis, total number of counter D_flip-flops is 1613. and the number of cells is 14876.

![number of ff](day%2001/number%20of%20ff.jpeg)
So, the flop ratio = (number of flip flops)/(number of total cell).

So, the flop ratio is 10.84%.

Before run, we saw that the result folder is empty. but now, after running the synthesis, we can see that all the mapping have been done by ABC.

![picorv32a](day%2001/picorv32a.jpeg)

And in the report, we can see when the actual synthesis has done. and the actual statistics synthesis report is showing below, which is same as what we have seen before.

![yosys start rpt](day%2001/yosys%20start%20rpt.jpeg)

The below figure shows the timing report of the pre-layout synthesis.

![Sta rpt](day%2001/Sta%20rpt.jpeg)
