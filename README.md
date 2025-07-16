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

**Eg. RISC-V SoC**:- Key components like SRAM, SoC, ADC, DAC, and SPI are considered foundry intellectual property (IP). The fabrication of all integrated circuits depends on foundries, which employ techniques such as deposition and lithography for chip manufacturing.

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
![digital_asic_flow](day%2001/digital_asic_flow.png)

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

![synthesis](day%2001/synthesis.png)

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

![mergedlef](day%2001/mergedlef.png)

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

# <h2 id="header-2">Day 2 - Good floor planning considerations</h2>	 
## <h2 id="header-2_1">Chip Floor planning consideration</h2>
### <h2 id="header-2_1_1">Utilization factor and aspect ratio</h2>

Let's determine the width and height of the Core and Die, a crucial initial step in the physical design flow. We'll start with a netlist comprising two flip-flops interconnected by basic combinational logic. A netlist, fundamentally, defines the interconnections within an electronic circuit. Our focus here hinges on the physical dimensions of the constituent logic gates (AND and OR) and the specific flip-flops employed. Our goal is to translate these symbolic representations into tangible physical dimensions, specifically for the Core and Die areas, while excluding the dimensions attributable to routing wires. 

Let's standard cell have dimensions of 1unit*1unit

So, area= 1 Sq. units

Asuume same area for the flipflop as well = 1 Sq. units

with help of these dimensions and netlist let's calculate the area occupied by the netlist on a silicon wafer.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/abf79875-e1e3-4faf-87a6-43a12d44db8d)

Prior to delving into detailed routing, we effectively condense all the flip-flops and logic gates onto a unified "plate" or base. By consolidating these components and abstracting away the interconnecting wires for this initial calculation, we can determine a preliminary footprint. In this simplified view, if the width and length of this combined unit are both 2 square units, then the total occupied area amounts to 4 square units. This gives us a rough, minimum area estimate for the given netlist, setting the stage for subsequent physical design steps.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/beb2d87b-db4f-47ac-95db-7a5586018c98)

What is 'Core' and 'Die' section of a chip?

We have a silicon wafer on which all the logics are implemented. In this one section is referred as 'Die' and inside the Die we have the Core. 

A **Die** which consists of core, is small semiconductor material  specimen on which the fundamental circuit is fabricated.

A '**Core** is the section of the chip where the fundamental logic of the design is placed.

![Slicon_Wafer](day%2002/Slicon_Wafer.png)

Now, envision placing this aggregated logic, representing our netlist, within the core of the chip. If this netlist is designed to fully occupy the entire core area, it signifies 100% core utilization. This concept allows us to calculate the "utilization factor," a critical metric in physical design. The utilization factor is typically defined as:

Utilization Factor = Area occupied by netlist / Total area of the core
   
Let us now put the dimensions we have,

Utilization factor = 4*1sq.unit / 2unit *2unit = 4sq unit /  4sq unit

So, utilization factor = 1 (It means core has utilized all the area and no span left)

Aspect Ratio = Height /  width =  2 unit /  2unit =  1

Whenever Aspect Ratio is 1 it signifies that chip is square shaped. When it is not 1 it means the chip is in rectangular shape.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/51360246-9ab3-4209-ba7d-d1d99bcd65ef)

For example, Lets take another dimensions of the width= 4unit and height = 2unit. So from the above formula of utilization factor we it equal to 0.5 which means the chip has not covered the whole area of the core and aspect ratio is also 0.5  which means the chip is rectangular in shape.

The leftover area can be used to placed some additional cells like buffers or something else.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/10a1d860-d6c2-4efc-95a7-d5f123cbdca3)


### <h2 id="header-2_1_2">Utilization factor and aspect ratio</h2>

Lets take another example for a square chip wth dimensions 4*4 sq units. We will get utilization factor= 0.25 it means out of the whole chip area only 25% area is utilized by the netlistand 75% is available for additional cells which can be use for routing in which we will have layering. Aspect ratio we get = 1 it means chip is square in shape.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/a64a81cd-760a-44b8-a81c-93318bf49746)

**Define locations of Preplaced Cells**:-  Lets take a combinational logic which does some amount of function and assume its a huge circuit having some N Logic gates so let's devide it into some small numbers of gates. We will cut the whole circuit into two parts, and separate both of them into two blocks and both block will be implemented seperately.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/477f5715-38c7-4cb8-ab4f-6b6108839e69)

In both the blocks lets extend the input output pins and now we will black box the boxes and detached them. After black boxing, the upper portion is invisible from the top or invisible to the one , who is looking into the main netlist. now will seperate them out as two different IP's or modules.

![blackbox](day%2002/blackbox.png)

A significant advantage of this modular approach is the ability to reuse these pre-designed components multiple times after a single implementation. This principle extends beyond basic logic gates and flip-flops to other Intellectual Property (IP) blocks. For instance, specialized IP cores like Memory units, Clock-gating cells, Comparators, and Multiplexers are all integral parts of a larger, top-level netlist. Each of these IPs receives specific input signals, performs its designated function, and delivers outputs, yet their complex internal functionality is designed and verified only once, making them readily deployable in diverse designs. 

The arrangement of these IP's in a chip is refer as **floor planning**.

These IP's have user-defined locations, and hence are placed in chip before automated placement and routing are called **"pre-placed cells"**. 

These cells are placed in such a way that, the placement and routing tool do not touch the location of the cell.

![preplaced_cells](day%2002/preplaced_cells.png)

The figure above illustrates the placement of pre-placed cells within a chip's core, demonstrating how larger, fixed-location blocks (Block a, Block b, and Block c) are integrated into the overall die and core structure.


### <h2 id="header-2_1_3">De-coupling capacitors</h2>

#### Enhancing Power Integrity with Decoupling Capacitors
**Why Decoupling is Essential for Pre-Placed Cells?**

Pre-placed cells, such as large IP blocks (memories, processors) or critical clock distribution components, often exhibit high current demands during their switching cycles. These sudden current surges can cause localized voltage drops (IR drop) or ground bounces across the power distribution network. Such fluctuations can negatively impact the performance and reliability of the surrounding circuitry, potentially leading to timing violations or functional failures. By placing decoupling capacitors in close proximity to these pre-placed cells, they can rapidly supply the necessary transient current, thereby stabilizing the local power supply and ensuring consistent voltage levels. This localized energy buffering is vital for maintaining the integrity of the power delivery network and ensuring the robust operation of high-performance integrated circuits.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/b8b1d031-c395-4fde-8c28-25a7f2f7cfcc)

In real-world circuits, an ideal logic '1' (typically 1V) often experiences a voltage drop, becoming, for example, 0.97V (Vdd'). This directly shrinks both the noise margins: NM low (for logic '0') and NM high (for logic '1'). Such reduced margins create a hazardous scenario where external noise or internal variations can easily cause a signal to be misinterpreted, leading to erroneous operation.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/36d7fe02-ad66-4b72-be7a-998378684242)

To mitigate this issue, decoupling capacitors (Cd) are strategically placed in parallel with the circuit. Each time the circuit transitions, it draws the necessary current from Cd, while an associated RL (Resistor-Inductor) network is concurrently employed to replenish the charge within Cd. Consequently, the immediate current demands of the circuit are effectively supplied by the decoupling capacitor.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/3547d7d2-ff77-43ba-9e69-c1e64393c1c1)

In the chip's layout, this appears as depicted below: decoupling capacitors are strategically positioned among blocks 'a', 'b', and 'c'. Within this entire arrangement, the consistent power supply from these decoupling capacitors is thus ensured. Upon completion of this step, we have effectively addressed the requirements for local power delivery.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/3078f01a-e20f-4aee-868a-9a2bb0449f71)


### <h2 id="header-2_1_4">Power planning</h2>

Now, let's treat that local circuitry as a black box, a reusable element that can be replicated multiple times. We acknowledge that some logic exists at the boundaries, and the issue of current demand within these local blocks has been addressed by decoupling capacitors. Consider a signal propagating from a driver to a load, specifically a transition from logic '0' to logic '1'. It's crucial to maintain signal integrity across this driver-to-load line so the load receives an accurate representation. Power supply is then applied.

Now, imagine a 16-bit bus that must reliably transmit this same signal from the driver to the load, requiring sufficient power from the supply. However, this bus lacks decoupling capacitors because it's simply not feasible to place them everywhere. Given the power supply is physically distant from this bus, a definite voltage drop will occur along the path.

 ![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/7c9f6257-fb53-43e6-a5d2-bb37e703f943)


When a specific line on the 16-bit bus signifies a logic '1', it indicates that the associated capacitance is charged to Vdd. Conversely, if it represents a logic '0', that capacitance is discharged to ground. Now, consider this 16-bit bus connected to an inverter. Consequently, all initially charged capacitors will discharge, and those initially discharged will charge, due to the inverter's operation.


![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/77998949-b1e9-4321-a935-1f463dffc968)


The critical issue arises because all capacitors are tied to a single ground connection. During discharge, this common ground experiences a sudden voltage fluctuation, commonly known as a "Ground Bounce." Should the magnitude of this bounce surpass the defined noise margin, the circuit risks entering an undefined state. In this ambiguous condition, the signal could unpredictably settle as either a logic '1' or a '0', rendering the system's behavior entirely unpredictable.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/67eb5dd9-6bf5-4581-8f21-af3ad7fb8285)


Conversely, all capacitors at '0' volts must charge to 'V' volts via a singular Vdd tap point. This action inevitably causes a voltage drop at that Vdd tap. As long as this voltage reduction remains within the acceptable noise margin, circuit operation is stable. However, if the drop pushes the voltage into an undefined region, the system's behavior becomes unpredictable.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/ef424a46-925a-431b-bdb8-9a210e7ca3bf)

The previously observed phenomenon, characterized by supply voltage degradation, originated from applying power at a singular point. The resolution involves employing multiple power supplies. Consequently, each distinct block will draw current from its nearest power source and similarly discharge current into its closest ground connection. This distributed power delivery configuration is commonly referred to as a **mesh**.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/b1d49ca0-8e8a-4953-887a-19628abc3448)


And the power planning is shown below,

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/97e14546-cd7d-4eff-aa10-c93df7ae3562)

### <h2 id="header-2_1_5">Pin placement and logical cell placement blockage</h2>

**Pin Placement**

Let's consider the following design example for implementation. The first circuit here is driven by clk1, while the second circuit is driven by clk2; they have distinct inputs, Din1 and Din2, and corresponding outputs, Dout1 and Dout2, respectively. Additionally, we have some pre-placed cells, specifically BlockA, which receives inputs from both Din1 and Din2. Another pre-placed cell, BlockB, takes inputs from clk1 and clk2 and generates a clk output. Therefore, our current setup features four input ports: Din1, Din2, Clk1, Clk2, and three output ports: Dout1, ClkOut, Dout2.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/0e1bf8ee-1b0e-452e-8a05-6b7dbbce57c7)

Let's introduce an additional design for implementation. Circuits of this nature are exceptionally valuable for comprehending the intricate timing analysis between different clock domains.

![pinplacement1](day%2002/pinplacement1.png)

The complete design now appears as shown below, featuring six input ports and five output ports. The intricate connectivity details among these gates are encoded using either VHDL or Verilog hardware description languages, collectively forming what is termed the 'Netlist'.

![completedesign](day%2002/completedesign.png)

This diagram illustrates the "Pin Placement" stage in chip design. It shows the core with pre-placed blocks (Block a, Block b, Block c) now surrounded by strategically positioned Decoupling Capacitors (DEC P1, DEC P2, DEC P3). Input and output pins (like Din1, CLK1, Dout1, Clk Out, etc.) are visible along the perimeter of the core. Crucially, the Vss (ground) and Vdd (power) lines form a mesh grid, interconnected by contact points, highlighting the robust power delivery network within the chip.

![pinplace_withoutconnection](day%2002/pinplace_withoutconnection.png)

Let's now integrate this netlist into the core we previously designed, and subsequently, populate the empty region between the core and the die with pin information. The frontend team is responsible for defining the netlist's connectivity, including inputs and outputs, while the backend team handles pin placements. Accordingly, we must position the pre-placed blocks in close proximity to their respective input pins.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/fcacd10f-8811-427e-be3a-3931819553c6)

One notable observation here is the larger size of the clock-in and clock-out pins compared to standard input and output pins. This is because input clocks continuously supply signals to every element on the chip, and output clocks must deliver signals as rapidly as possible. Consequently, a path with minimal resistance is crucial for both clock inputs and outputs; a larger pin size directly correlates with lower resistance.

Another critical consideration is that this pin placement area becomes restricted for subsequent routing and cell placements. Therefore, it necessitates a logical cell placement blockage, which is visually represented in the image as the shaded areas between the pins.

The floorplan is now finalized, preparing the design for the subsequent Placement and Routing stages.

### <h2 id="header-2_1_6">Steps to run floorplan using OpenLANE</h2>

Before run the floorplanning, we required some switches for the floorplanning. these we can get from the configuration from openlane.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/67041b25-ee43-4864-9bce-fb0386d53641)

Here we can see that the core utilization ratio is 50% (bydefault) and aspect ratio is 1 (bydefault). similarly other information is also given. But it is not neccessory to take these values. we need to change these value as per the given requirments also.

Here FP_PDN files are set the power distribution network. These switches are set in the floorplane stage bydefault in OpenLANE.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/2b1281f9-b85a-4b08-b507-49c39c51c434)

Here, (FP_IO MODE) 1, 0 means pin positioning is random but it is on equal distance.

In the OpenLANE lower priority is given to system default (floorplanning.tcl), the next priority is given to config.tcl and then priority is given to PDK varient.tcl (sky130A_sky130_fd_sc_hd_congig.tcl).

Now we see, with this settings how floorplan run.

### <h2 id="header-2_1_7">Review floorplan files and steps to view floorplan</h2>

In the run folder, we can see the connfig.tcl file. this file contains all the configuration that are taken by the flow. if we open the config.tcl file, then we can see that which are the parameters are accepted in the current flow.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/be2a8bf3-4857-427e-a690-5ff3241bfbd9)

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/36985c6b-3e9f-473d-ab32-29b224cff6f1)

To watch how floorplane looks, we have to go in the results. in the result, one def( design exchange formate) file is available. if we open this file, we can see all information about die area (0 0) (660685 671405), unit distance in micron (1000). it means 1 micron means 1000 databased units. so 660685 and 671405 are databased units. and if we devide this by 1000 then we can get the dimensions of chips in micrometer.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/cb35a72a-6fa7-402b-a0ed-8010ffdcccd3)

so, the width of chip is 660.685 micrometer and height of the chip is 671.405 micrometer.

To see the actual layout after the flow, we have to open the magic file by adding the command ```magic -T /home/kunalg123/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def```

And then after pressing the enter, Magic file will open. here we can see the layout.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/bc916128-b14b-4d46-af0c-296f39dafb5f)


### <h2 id="header-2_1_8">Review floorplan layout in Magic</h2>

In the layout we can see that, input output pins are at equal distance.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/f02464f8-3bbc-4475-90a6-1d523ba36857)


after selecting (To select object, first click on the object and then press 's' from keyboard. the object will hight lited. to zoom in the object, click on the object and then press 'z' and for zoom out press 'sft+z') one input pin, if we want to check the location or to know at on which layer it is available, we have to open tkcon window and type "what". it will shows all the details about that perticular pin.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/5dc0a65b-4216-4879-b786-e4de4319dfc4)


so, it show that the pin is in the metal 3.similarly doing for the vertical pins, we find that this pin is at metal 2.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/b934b69a-5357-4b4d-a51a-e66cd352fb6c)


Along with the side rows,the Decap cells are arranged at the border of the side rows.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/e5f09e25-ff25-411b-aacc-74ae3df0ae61)



here we can see that first standerd cells is for buffer 1. similarly other cells are for buffer 2, AND gate etc.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/e0624489-5298-45cd-a08d-db2b3ec572b7)


## <h2 id="header-2_2">Library building and Placement</h2>
#### Netlist binding and initial place design 

**Binding a netlist with physical cells:-** This involves translating the abstract logical representation of gates into tangible, geometrically defined components. In the netlist, a NOT gate might be symbolically represented as a triangle, but in reality, it's implemented as a rectangular box with specific physical dimensions (width and height). Similarly, an AND gate and flip-flops, while having distinct logical symbols, are also physically realized as rectangular or square blocks. Therefore, for every component listed in the netlist, a particular shape and precise physical dimensions are assigned. This is crucial because abstract shapes like those for AND or OR gates do not exist in the physical world; all blocks, including these gates, must be defined with real-world width, height, and a proper, typically rectangular, physical form.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/687b1d86-e4aa-48d6-9cec-f354f5b2c5eb) 

All wires are now disregarded; the gates, flip-flops, and blocks are now compiled within a designated **Library**.

A library functions as a repository, akin to a collection of books, where all gates and flip-flops are cataloged. This library also stores crucial timing data for each "book," such as gate delays. It can be categorized into two sub-libraries: one dedicated to physical shape and size, and another solely for delay information. Furthermore, the library offers diverse variations of each cell; for instance, the same cell might be available in a larger form. A larger cell typically offers a lower resistance path, resulting in faster operation and reduced delay. Designers can select cells from these options based on specific timing requirements and the available space within the floorplan.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/8871a0f8-ddd0-419c-bbf5-fe09fe42fb49)

**Placement**: After assigning precise shapes and sizes to each gate, the subsequent step involves positioning these physical representations onto the pre-defined floorplan. We possess a floorplan complete with input and output ports, a specific netlist, and assigned dimensions for every component within that netlist. This effectively provides us with a physical perspective of the logic gates. The immediate next action is to integrate this netlist onto the floorplan, utilizing the connectivity data from the netlist to arrange the physical gate views within the designated layout.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/7936ded3-ad15-404b-9a32-3ea64bc591b2) 

Now, with our existing floorplan containing the pre-placed cells from earlier stages, the placement process ensures their undisturbed locations are preserved. Furthermore, it strictly prevents any other cells from being positioned over these pre-existing ones. Our objective is to arrange the physical view of the netlist onto the floorplan such that logical connectivity is meticulously upheld, enabling the circuit to interact efficiently with its input and output ports, thereby maintaining precise timing and minimizing signal delay.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/8c6fb8e4-9124-4983-be3f-757f2845ecea)


Here, we initially observe the arrangement of the netlist's remaining components on the floorplan. All elements have been positioned to be in close proximity to their respective input and output pins. 

However, the distance between FF1 of Stage 4 and Din4 remains notably larger than other connections. This particular issue can be resolved through further placement optimization.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/ac32f3c9-c3a9-4320-894b-a08ab407f068)


### <h2 id="header-2_2_2">Optimize Placement using Estimated wire-length and Capacitance</h2>

**Placement Optimization**: In this phase, we address the aforementioned distance issue. Considering the connection from Din2 to FF1, a significant wire length would be required. Before actual routing, we estimate the substantial capacitance and resistance associated with such a long wire. If a signal is sent from Din2, FF1 would struggle to reliably receive that input due to the extended distance. To maintain signal integrity, we can insert intermediate steps called "repeaters." These repeaters, essentially buffers, regenerate the original signal, creating a fresh, identical signal to propagate further. This process repeats until the signal reaches the intended cell, ensuring signal integrity. While repeaters solve the signal integrity problem, they inherently increase area consumption on the floorplan due to their inclusion.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/f47771b4-b28a-47db-b0dc-e5f13dd4c1b1)

In **Stage 1**, the signal transmission requires no repeaters. However, in **Stage 2**, the considerable distance leads to an extended wire length, causing the signal to fall outside its specified range. Consequently, a repeater becomes necessary to ensure proper signal propagation.

![placement_stage2](day%2002/placement_stage2.png)

### <h2 id="header-2_2_3">Final placement optimization</h2>

As similar to **Stage 2**, in **Stage 3** also we required the buffer between gate2 and FF2.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/2fc8bf91-4303-4837-b7e9-f9832d7a3723)

**Stage 4** presents unique complexities compared to preceding stages. At this point, it becomes imperative to verify the accuracy of our actions. To achieve this, we must conduct a thorough Timing Analysis, utilizing ideal clock conditions. The data derived from this analysis will then enable us to determine the correctness of the current placement.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/121df907-96ad-4893-ae1d-d9fa96b7a328)

### <h2 id="header-2_2_4">Need for libraries and characterization</h2>

Every IC design flow mandates a series of sequential steps. Initially, Logic Synthesis converts a functional description, often coded in RTL, into a valid hardware representation. The outcome of this process is an arrangement of gates that accurately reflects the original RTL-described functionality.

Following Logic Synthesis is Floorplanning, where the synthesized output is imported to determine the Core and Die dimensions. Placement, the subsequent step, involves strategically positioning logic cells onto the chip to optimize initial timing. Next, Clock Tree Synthesis (CTS) ensures that clock signals reach every element simultaneously, while also guaranteeing consistent rise and fall times for each clock signal. Routing then follows a specific flow, dictated by the flip-flop characteristics. 

![needftorlib_synplaceroute](day%2002/needftorlib_synplaceroute.png)

Finally, Static Timing Analysis (STA) concludes the process by evaluating setup time, hold time, and the circuit's maximum achievable frequency. Throughout all these stages, "GATES or Cells" remain the unifying element.

![need_forlibsta](day%2002/need_forlibsta.png)


### <h2 id="header-2_2_5">Congestion aware placement using RePlAce</h2>

Right now we are not constrain about timing, but constrain about the congestion. so, we are making the congrstion is less.

The placement is donne in two stages. Global and detailed. In global placement, legalization is not happened but after detailed placement legalization will be done.

When we run the placement, first Global placement is happens. main objective of glibal placement is to reducing the length of wires.

Now opening the Magic file to see actual view of standerd cells placement.And the actual view in the magic file is given below.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/d7e29ff0-f009-4c72-9129-d7662b46f8b8)

If we zooom into this, we find the buffers, gates, flip flops in this.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/768d1fbd-c7b4-4b15-bbd5-cebd57a1c79a)



## <h2 id="header-2_3">Cell design and characterization flows</h2>
### <h2 id="header-2_3_1">Inputs for cell design flow</h2>

In Cell Design Flow, Gates, flipflops, buffers are named as 'Standard Cells'. These standard cells are being placed in the section called as 'Library'.And in the library many other cells are available which have same functionality but the size is different.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/22c0c83e-e32e-453b-ad64-b5cef4c4d6af)

If you lokk into one of the inverter from the library the cell design flowis as follows

The inverter has to represented in form of the shape, drive strength, power charracteristic and so on. Here cell design flow is devided into three parts.

1. Inputs

2. Design steps

3. Outputs

**1) INPUTS**:- Inputs required for cell design is PDKs, DRC and LVS rules SPICE models, library and user defined specs. In DRC& LVS rules tech file is provided which contains design rules and actual values. Rules can be converted in to code. SPICE MODEL tells about threshold voltage equation.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/2fb42be5-76e2-4017-9ff9-4fb23306b24e)

**Inputs DRC and LVS**
This emphasizes that Design Rule Check (DRC) and Layout Versus Schematic (LVS) rules are key inputs from PDKs, providing the geometric and connectivity constraints for valid cell layouts.

![celldesign_drc_lvs](day%2002/celldesign_drc_lvs.png)

**Inputs SPICE Models**
This details how "SPICE model parameters" from PDKs provide the complex mathematical equations and values (like threshold voltage, current in linear/saturation regions) necessary for accurate circuit simulation.

![celldesign_spicemodel](day%2002/celldesign_spicemodel.png)

**Inputs Library and user-defined Specs**
There are inputs like height, supply voltage, pin-location, gate length, metal layers etc.

![celldesign_libnuser_height'](day%2002/celldesign_libnuser_height'.png)

The above figure highlights how "Cell-height" is a crucial input from the Process Design Kits (PDKs) in the cell design flow, influencing the overall vertical dimension of the standard cells and IP blocks.

![celldesign_libnuser_voltage](day%2002/celldesign_libnuser_voltage.png)

The above figure illustrates that "Supply voltage" is a fundamental input from PDKs, defining the operational voltage levels critical for the design and performance of the cells within the chip.

![celldesign_libnuser_pinloc](day%2002/celldesign_libnuser_pinloc.png)

The above figure shows "Pin location" as another critical input from the PDKs for cell design, dictating where the input and output connections are precisely positioned on a cell's layout.

![celldesign_libnuser_gatelength](day%2002/celldesign_libnuser_gatelength.png)

The above figure points out that "Drawn gate-length" is a vital parameter derived from PDKs, specifying the physical length of the transistor gates, which directly impacts device performance.

![celldesign_libnuser_metallayers](day%2002/celldesign_libnuser_metallayers.png)

The above figure indicates that "Metal layers" are fundamental inputs from PDKs, defining the number and characteristics of the conductive layers used for interconnects within the cell layout.

### <h2 id="header-2_3_2">Circuit design steps</h2>

The separation between the power rail and the ground rail defines the cell height. Cell width depends upon the timing and drive strength.

**2)Design steps**:- Design involves three steps which are circuit design, layout design, characterization.

**In circuit Design** there are two steps.

First step is to implement the function itself and second step is to model the PMOS and NMOS transistor in such a fashion in order to meet the library.

**3)Outputs**

The typical output what we get from the circuit design is CDL(circuit description language) file, GDSII, LEF, extracted spice netlist(.cir).


![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/8e9891ea-35e0-48eb-b6f5-53376c86528e)


### <h2 id="header-2_3_3">Layout design step</h2>

In Layout Design, the initial step involves realizing the desired circuit function using a combination of PMOS and NMOS transistors. Following this, the next crucial phase is to extract the distinct PMOS and NMOS network graphs from the implemented transistor-level design.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/25c9f2db-c630-41d7-be4a-cab6f93a94af)

After acquiring the network graphs, the subsequent step is to determine the Euler's path. An Euler's path is essentially a traversal within the graph where each edge is visited precisely once.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/117eb8be-2f24-4b7b-a5fa-052ef4b3bd43)

Next step is to draw stick diagram based on the Euler's path. This stick diagram is derived out of the circuit diagram.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/a89a6f84-fa7e-4a36-9af7-74ab04f5b5c3)



The subsequent step involves transforming this stick diagram into a standard, proper layout, then applying the specific rules previously discussed. Once this particular layout is achieved, all cell specifications, including cell width, cell length, drain current, pin locations, and other relevant attributes, will be precisely defined.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/7917c567-5aa7-4c66-b8ab-43e0e4808e06)

The final step involves extracting the parasitics from the specific layout and characterizing them in terms of timing. Prior to this, the output from the layout design will be in GDSII format. Once the extracted SPICE netlist is obtained, it undergoes characterization. This characterization process provides crucial timing, noise, and power information.

### <h2 id="header-2_3_4">Typical characterization flow</h2>

Drawing upon our available inputs, let's now construct the characterization flow.

The initial step involves ingesting the model. Subsequently, the extracted SPICE netlist is read in. The third step requires defining or recognizing the buffer's behavior. Following this, in the fourth step, the inverter's subcircuits are read. The fifth step necessitates attaching the required power supplies. Next, in the sixth step, the stimulus is applied. The seventh step involves providing the necessary output capacitance. Finally, the eighth step entails issuing the appropriate simulation command; for instance, a `.tran` command for transient simulation or a `.dc` command for DC simulation.

All the steps are shown below in the two images.

![typchar_flow1](day%2002/typchar_flow1.png)

![typchar_flow2](day%2002/typchar_flow2.png)

Next step is to feed in all this inputs from 1 to 8 in a form of a configuration file to the characterization software **"GUNA"** .

This software will generate power, noise and timing model.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/19b01aa6-c6ba-4d39-8d10-539a40ab9f39)

## <h2 id="header-2_4">General timing characterization parameters</h2>
### Timing threshold definitions


As observed in the preceding section, the cascaded inverters, power sources, and applied stimulus introduce a crucial aspect: comprehending the distinct threshold points within a waveform, referred to as "Timing threshold definitions." 

In the accompanying figure, the term 'Slew_low_rise-thr' represents a value near zero, typically around 20%, though it can also be 30%.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/3819e09b-be65-480b-b01b-dab709ef687b)

Slew_high_rise_thr

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/d8134157-d13c-49b3-9ec2-ef50e8ff1bf7)


Slew_low_fall_thr

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/cca7ece5-603a-46b4-b781-9c82b3d14f9b)


Slew_high_fall_thr

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/3e5dd161-ff39-4a74-89da-06a642835f14)


Now, considering the input stimulus waveform (the first buffer's input) and the corresponding output waveform from that same buffer, thresholds are also defined for delay, analogous to slew. For this, we must identify specific rise and fall points on the waveforms. These delay thresholds are typically set at approximately 50%.

in_rise_thr

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/eb232344-b6d9-4de0-b351-9910214a8fbc)

in_fall_thr , its typical value is 50%.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/b40bb02f-aac3-4635-9615-d7e95901aa08)

out_rise_thr

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/9e16ea11-c75e-40da-91d8-82baa271b7d8)

out_fall_thr

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/2cb0db7d-8dcb-41bb-b0d9-b2b10e8eb31b)


### <h2 id="header-2_4_2">Propagation delay and transition time</h2>

Based on these defined threshold values, we proceed to calculate further parameters such as propagation delay, current, and slews.

To determine any delay, we subtract the 'out_rise_thr' time from the 'in_rise_thr' time. Using a typical value of 50%, we can observe its application on a specific waveform: Time delay = Time(out_thr) - Time(in_thr).

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/d157a7da-02ba-44d7-9acf-90899273eb7f)

In the preceding example, both in_rise_thr and out_fall_thr were set at 50%. However, if the threshold point shifts higher, the output appears before the input, resulting in an unaccepted negative delay. This negative delay arises from a poor choice of threshold point, underscoring its critical importance.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/6540a5e2-cf40-4202-994e-e7ff05d6d60f)

Consider an alternative scenario, in the below figure

![transitiontime_MIDPOINT](day%2002/transitiontime_MIDPOINT.png)

Despite a correctly chosen threshold point, a negative delay can still manifest. This occurs because the output signal appears prior to the input, resulting in an unacceptable negative delay.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/03a0e311-2552-4a40-8345-9075f655fdee)

**Transition time**=  time(slew_high_rise_thr)- time(slew_low_rise_thr)

or

**Transition time** = time(slew_high_fall_thr)- time(slew_low_fall_thr)

Consider a waveform for illustrating slew calculation.

![image](https://github.com/kmkalpana2001/DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING/assets/165163110/2f7d8314-e195-48fc-98f3-b20441352242)
