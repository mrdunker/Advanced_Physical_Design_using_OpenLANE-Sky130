# Advanced_Physical_Design_using_OpenLANE-Sky130
This repository is made to document the coursework done under Kunal Ghosh for ASICs and covers Advanced Physical Design using OpenLane and Sky130.

## Day 1: Inception of open-source EDA, OpenLANE and Sky130 PDK
<details>
  <summary>Introduction to RISC-V</summary>
  <br />
  RISC-V is an open-source instruction set architecture (ISA) for computer processors.<br>
  An instruction set architecture defines the set of instructions that a processor can execute and the organization and behaviour of those instructions.
  RISC-V is unique in that any single company or organization does not own it. and it is freely available for anyone to use, modify, and implement without 
  the need for licensing fees or proprietary restrictions.<br />  
  The RISC-V project began at the University of California, Berkeley in 2010, and it has since gained significant traction in both academia and industry.
  Its open nature has led to a growing ecosystem of hardware and software developers collaborating to create a wide range of products, from simple embedded 
  devices to high-performance supercomputers.
  <br/>
  Application software (apps) and hardware are linked by 'system software'.There are various layers of system softwar*. This includes major components like   
  Compiler and Assembler.<br />
  <br />
  The compiler compiles high-level codes like C and C++ to Instructions(eg: the codes inside .exe files) that can be read by the Assembler.<br />
  The Assembler converts it into binary codes which the machine can understand. The instructions act as an interface between the high-level language and the 
  machine language.<br />
  The converted binary is then given to an RTL snippet that understands the instruction. This is done by a Hardware Description Language (HDL).
  This is basically called RTL implementation and a netlist is being generated. with this, a physical design implementation of the design is generated.<br />
  see more info at : https://github.com/mrdunker/RISC-V_based_MYTH_IIITB/
</details>

<details>
  <summary>Communicating with computers</summary>

  ### QFN-48 Package
  A QFN-48 package is a type of integrated circuit (IC) package that follows the Quad Flat No-Lead (QFN) format and contains 48 leads or pins. This package is characterized by its flat, square or rectangular shape  
  with no leads protruding from the sides. Instead, the electrical connections are made through small exposed pads on the bottom surface of the package, which are soldered directly onto the circuit board or PCB 
  (Printed Circuit Board).
  <br />
  
  ![Screenshot from 2023-09-10 12-25-34](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/8c1bd2a2-0406-4ae9-ae17-2704878f1f00)

  The different componets in a broad view are given below.<br />
  ### Chip
  In a QFN-48 package, the chip is attached to the die attach pad, which is the central exposed pad on the bottom surface of the package. This pad provides a mechanical and thermal connection between the chip and 
  the package. Electrical connections from the chip to the external world are made through the other exposed pads (leads) on the bottom surface of the package.
  <br />
  The chip within a QFN-48 package can vary widely in terms of its function, complexity, and manufacturer. It might be a microcontroller, a memory chip, a sensor, or any other type of integrated circuit designed to 
  perform specific tasks within an electronic system. The QFN-48 package serves to protect, house, and provide electrical connections for the chip, making it suitable for surface-mount assembly onto a printed     
  circuit board (PCB) in various electronic devices and applications.

  ### Pads
  A QFN-48 (Quad Flat No-Lead 48) package typically includes 48 pads, which are the exposed metal areas on the bottom surface of the package. These pads serve as the electrical connections between the integrated 
  circuit (IC) inside the package and the printed circuit board (PCB) on which the QFN-48 package is mounted.

  ### Core
  The core of the QFN-48 package is the central and most essential part of the package. It houses the semiconductor die or microchip, which contains the electronic circuitry, transistors, and other components 
  responsible for the device's intended functionality. The core of the QFN-48 package is attached to the die attach pad, which is the central exposed pad on the bottom surface of the package.

  ### Die
  The die is the heart of the integrated circuit (IC) and contains the actual electronic components, transistors, and circuitry responsible for the device's functionality.
  The die itself is where all the electronic magic happens. It contains the logic, memory, or other functional components that define the IC's purpose. The QFN-48 package serves to protect the die, provide 
  electrical connections, and assist in thermal management, making it suitable for surface-mount assembly onto a PCB in various electronic devices and applications.
  
<br />

  ![Screenshot from 2023-09-10 12-37-50](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/6f7e960c-bfca-48ac-b755-241359dfd6c6)

  
  
</details>
<details>
  <summary>SoC Design using OpenLane</summary>
  <br />
  Desiging Digital Application Specific Integrated Chip(ASIC) require several elements. They are as follows:

- RTL IP's
- EDA tools
- PDK tools
  <br />

 ![Screenshot from 2023-09-10 12-10-23](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/691c28ee-6c96-44e7-ab14-f904801659a3)
 
### RTL IP's
RTL IP encompasses pre-constructed and pre-validated units of digital logic or functional modules, which are described at the register-transfer level (RTL). RTL serves as a hardware description level that
characterizes the operation of a digital circuit through data transfers between registers and logic operations. RTL IP cores represent reusable components that can be incorporated into more extensive ASIC or FPGA
designs. These cores encompass a range of functions, including processors, memory controllers, communication interfaces, and others. Designers frequently employ RTL IP to streamline the development of intricate
digital systems, thereby conserving time and resources.
<br />
### EDA tools
Electronic Design Automation (EDA) tools are software applications that streamline the creation and validation of electronic circuits, encompassing ASICs, FPGAs, and other digital systems. These tools span across 
multiple phases of the design process, from the initial conceptualization to the ultimate physical realization.
<br />
### PDK tools
A Process Design Kit (PDK) encompasses a set of resources, including tools, libraries, and documentation, furnished by semiconductor foundries. These resources are designed to empower creators in fashioning ASICs 
and other integrated circuits, leveraging the foundry's unique manufacturing processes. PDK tools form an integral component of the PDK bundle, serving various essential functions.
<br />

The below photo illustrates the various open source tools that can be used in designing ASIC's.<br />
![Screenshot from 2023-09-10 12-12-20](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/67db0ed2-7876-4948-8a96-3c9a08623d9a)

<br />
The simplified flow from RTL to GDSII is shown below.<br />

![Screenshot from 2023-09-10 12-43-01](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/0ca47cf7-6c04-48b2-b908-d9cb4b879205)

Following are the various step shown in the above figure to convert RTL to GDSII

- **Synthesis**: Synthesis involves the process of translating a high-level hardware description of a digital circuit into a Register-Transfer Level representation, which is a lower-level and more hardware-      oriented description of the same circuit.

- **Floor & Power Planning**: Floor planning and power planning are essential steps in the design and layout of an Application-Specific Integrated Circuit (ASIC). They involve the physical organization and allocation of resources within the chip to meet performance, power, and area requirements
  - Chip floor planning : involves strategically organizing and allocating the available silicon area on a chip to accommodate various functional blocks.
  - Macro floor planning : specific aspect of the chip floor planning process that focuses on the organization and placement of large functional blocks, often referred to as macros or IP (Intellectual Property) blocks, within an integrated circuit (IC) design. 
  - Power Planning :  It involves the strategic distribution and management of power supply and ground connections within the chip to ensure proper power delivery, minimize voltage drop, and control power consumption.

- **Placement**: process of determining the physical location of various functional blocks and components on the silicon die of the chip. 
  - Global Placement: It involves determining the approximate positions of all the functional blocks and components on the chip's silicon die. Global placement sets the initial arrangement of these blocks.
  - Detailed Placement: Detailed placement aims to meet stringent design constraints, optimize chip area utilization, and minimize wirelength to ensure the chip's performance, power efficiency, and manufacturability.

- **Clock Tree Synthesis**: CTS, or clock tree synthesis, involves creating a clock distribution network to guarantee that clock signals reach all sequential elements, like flip-flops, in a synchronized manner. Adequate CTS is essential to uphold timing requirements.
  
-  **Routing**: process of creating the physical interconnections or paths that allow electrical signals to flow between various components, such as gates, flip-flops, and memory elements, on a silicon die.

- **Signoff**: After placement and routing,detailed design rule checking (DRC) and final verification is done to ensure the layout complies with fabrication constraints and meets specified requirements for timing, area, and power.

## OpenLANE

OpenLane is a fully automated process, spanning from RTL (Register-Transfer Level) to GDSII (Graphics Data System II), and relies on various components, including OpenROAD, Yosys, Magic, Netgen, CVC, SPEF-Extractor, KLayout, and a set of specialized scripts for design exploration and enhancement. This comprehensive flow covers every step of ASIC implementation.
<br />

OpenLANE utilises a variety of opensource tools in the execution of the ASIC flow:
- RTL Synthesis & Technology Mapping: yosys,abc
- Floorplan & PDN:init_fp, ioPlacer, pdn and tapcell
- Placement:RePLace, Resizer, OpenPhySyn & OpenDP
- Static Timing Analysis:OpenSTA
- Clock Tree Synthesis:TritonCTS
- Routing:FastRoute and TritonRoute
- SPEF Extraction:SPEF-Extractor
- DRC Checks, GDSII Streaming out:Magic, Klayout
- LVS check:Netgen
- Circuit validity checker:CVC

More info can be obtained from [here](https://github.com/The-OpenROAD-Project/OpenLane)
<br />

### Invoking OpenLANE

```
cd OpenLane
make mount
```
Inside the openlane container
```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
```
![Screenshot from 2023-09-10 13-20-32](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/a16a15a4-544a-4eca-a558-23e8e27447c4)

![Screenshot from 2023-09-10 13-28-12](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/1148cc75-75a9-4365-b2cc-7f63634a8f77)

The netlist generated is shown below:<br />
```
cd OpenLane/designs/picorv32a/runs/RUN_2023.09.10_07.47.37/results/synthesis/
gvim picorv32.v
```
![Screenshot from 2023-09-10 13-34-48](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/2085f6aa-42aa-4de4-9af3-70fa8fa8c641)

To view report:<br/>
```
cd OpenLane/designs/picorv32a/runs/RUN_2023.09.10_07.47.37/reports/synthesis/
gvim 1-synthesis.AREA_0.stat.rpt
```

![Screenshot from 2023-09-10 13-37-34](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/bcbe3d1d-be23-4d7d-b585-bd92ea798e74)


```
Flop ratio = Number of D Flip flops = 1596  = 0.1579
             ______________________   _____
             Total Number of cells    10104
```

</details>

## Day 2: Good floorplan vs. Bad floorplan and introduction to library cells
<details>
  <summary>Chip floorplanning and considerations</summary>

  ### Floorplan considerations

  There are certain factors that we have to take into consideration when doing floorplanning.Such as:
  
  - Utilization factor and Aspect Ratio
  - Define locations of preplaced cells
  - Decoupling capacitors
  - Power Planning
  - Pin Placement

    ### Utilization Factor & Aspect Ratio

    The utilization factor, also known as the area utilization factor or chip utilization factor, is a measure of
    how efficiently the silicon area on a chip is being used for active components (logic gates, memory cells,
    etc.) compared to the total available area.
    <br />
    A Utilisation Factor of 1 signifies 100% utilisation leaving no space for extra cells such as buffer. However,
    practically, the Utilisation Factor is 0.5-0.6. Likewise, an Aspect ratio of 1 implies that the chip is square
    shaped. Any value other than 1 implies rectanglular chip.

    ```
    Utilisation Factor =  Area occupied by netlist
                         __________________________
                            Total area of core
    ```

    The aspect ratio in ASIC design is a measure of the chip's physical shape, specifically the ratio of its width
    to its height. It is often used in the context of standard cell libraries and the dimensions of the chip's core
    area. The aspect ratio is expressed as:

    ```
    Aspect Ratio =  Height of the core
                   _____________________
                     Width if the core
    ```

    ### Preplaced cells

    Preplaced cells, also known as predefined cells, are a category of components used in
    Application-Specific Integrated Circuit (ASIC) and digital integrated circuit design. Unlike standard cells,
    which are typically placed and routed automatically during the design process, preplaced cells are fixed or
    manually placed at specific locations on the chip's layout by the designer.Preplaced cells are IPs comprising
    large combinational logic which once placed maintain a fixed position.

    ### Decoupling capacitors

    The above mentioned preplaced cells must be surrounded with decoupling capacitors.Since the imepedence of the
    long wire lengths can cause power supply to drop significantly before reaching the logic circuit,leading to the
    signal not entering the noise margin range.<br />
    Decoupling capacitors are large capacitors that are charged to power supply voltage and kept close to the logic
    circuit.**It serves the purpose of decoupling the logic circuit from power supply by providing adequete amount
    of current to the circuit**.It prevents cross-talk.

    ### Powerplanning

    Unlike preplaced macros,each block on chip cannot have it's own decoupling capacitor. Powerplanning ensures
    that each block gas its own VDD and VSS pads and ground lines forming a mesh.

    ### Pinplacement

    The space between the core and the chip is allocated for the placement of pins. The connectivity data encoded
    in either VHDL or Verilog is employed to decide the location of I/O pads for different pins. Subsequently, a
    logical placement is carried out for pre-placed macros to clearly distinguish that region from the pin area.

    ### Running floorplan using OpenLANE

    After simulation we run picorv32a floorplan using the commnand below:

     ```
     run_floorplan
     ```
     
     ![Screenshot from 2023-09-10 16-46-57](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/d84821ab-781b-4050-8981-dce01377652c)

    For viewing the floorplan we are using the tool **magic**.<br/>
    We should move into the directory 'results/floorplan' and use the below command.<br />

    ```
    magic -T /home/emil/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def &
    ```

    Here we need to specify the sky130A.tech file directory as well.
    
     ![Screenshot from 2023-09-10 17-45-19](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/071b616a-cc25-4d66-8229-db70540b6c51)

    **Basic Magic shortcuts:**
    - Press 'Z' on keryboard to zoom in.
    - Press 'V' to center (zoom out fully).
    - Hover over an element and press 'S' to select it.
    - After selecting type 'what' in the console window to view it's details.
  
    ![Screenshot from 2023-09-10 17-56-07](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/f480cc1a-4b3a-43aa-87c0-d4c87a4abab6)



</details>
<details>
  <summary>Library binding and Placement</summary>

  ### Placement

  In this step of OpenLANE ASIC flow,The synthesized netlist is to be placed on the floorplan.It occurs in two 
  stages:
  1. Global Placement
  2. Detailed Placement

  **Global Placement** finds optimal position for all cells which may be not legal at the time and overlap.<br />
  **Detailed Placemnent** changes this particular placement and make it legal.It is important from a timing point 
  of view<br />

  ### Running Placement on OpenLANE

  Here we are going to run placement and view the new layout on magic.<br />
  We are going to use the below command to run placement, in OpenLANE.<br />
  ```
  run_placement
  ```
  ![Screenshot from 2023-09-10 22-47-32](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/4bd0174a-c627-4c26-a0ca-5b791062860b)

  After which we change directory to results/placement.<br />
  Inside the directory we run the following command for executing magic.<br /> 
  ```
  magic -T /home/emil/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read
  picorv32.def &
  ```
  The below  is the screen shot in magic.<br />
  ![Screenshot from 2023-09-10 22-49-32](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/e443a681-8f32-41c0-9d46-36b5f4a2fa76)

  ![Screenshot from 2023-09-10 22-50-31](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/8bbf39a7-8e08-48aa-ade1-857f49865cdb)

  
</details>

<details>
<summary>Cell Design and Characteristic Flow</summary>

  ### Standard Cell Design Flow
The standard cell design flow in ASIC involves iterative processes, and each step must be 
carefully executed to ensure a successful design that meets the specified requirements within 
the constraints of the target technology node.

Standard cell design flow involves the fillowing:
1. Process Design Kits (PDKs), Design Rule Checking (DRC) and Layout vs. Schematic (LVS) guidelines, SPICE models, libraries, and user-defined specifications.
2. Circuit design, Layout design (Art of layout Euler's path and stick diagram), Extraction of parasitics, Characterization (timing, noise, power).
3. CDL (circuit description language), LEF, GDSII, extracted SPICE netlist (.cir), timing, noise and power .lib files.

  ### Standard Cell Characterizarion Flow

The industry-standard process for characterizing standard cells typically consists of the following stages:

1. Read in the models and tech files
2. Read extracted spice Netlist
3. Recognise behavior of the cells
4. Read the subcircuits
5. Attach power sources
6. Apply stimulus to characterization setup
7. Provide neccesary output capacitance loads
8. Provide neccesary simulation commands

For characterization an opensource software called GUNA is used.<br />
All the steps from 1 to 8 are fed into GUNA,which in turn generates timing,noise and power models.
  
</details>

<details>
  <summary>Timing characterization paramenters</summary>
  <br />
  It is the process of assessing and quantifying the timing behavior of digital logic elements, 
  such as standard cells or custom-designed blocks, within an integrated circuit. It is a 
  crucial step to ensure that the ASIC operates correctly and meets the required performance 
  specifications. 
  <br />

  ### Timing threshold definitions
  
  Timing defintion |	Value
  -------------- | --------------
  slew_low_rise_thr	| 20% value
  slew_high_rise_thr | 80% value
  slew_low_fall_thr |	20% value
  slew_high_fall_thr |	80% value
  in_rise_thr	| 50% value
  in_fall_thr |	50% value
  out_rise_thr |	50% value
  out_fall_thr | 50% value

  ### Propagation Delay

  The time disparity between the moment the changing input attains 50% of its ultimate level and 
  the instance when the output reaches 50% of its ultimate level can be described as the delay. 
  If you select inappropriate threshold values, it can result in negative delay values. Even 
  when appropriate threshold values are chosen, the delay can occasionally be either positive or 
  negative, influenced by the quality of the signal transition (slew rate).

  ```
  Propagation delay = time(out_fall_thr) - time(in_rise_thr)
  ```

  ### Transition Time

 The interval required for the signal to transition between its states is referred to as the 
 transition time. This time span is typically measured by observing the signal's shift from 10% 
 to 90% or 20% to 80% of its signal levels.

 ```
 Rise transition time = time(slew_high_rise_thr) - time(slew_low_rise_thr)

 Low transition time = time(slew_high_fall_thr) - time(slew_low_fall_thr)
```

</details>

## Day 3: Design Library Cell using magic layout and ngspice Characterizations

<details>
  <summary>CMOS inverter using ngspice simulations</summary>
  <br />
  NGSpice is an open-source electronic circuit simulator software used for analog, digital, and 
  mixed-signal electronic circuit simulation. It is part of the larger family of SPICE 
  (Simulation Program with Integrated Circuit Emphasis) simulators.<br />

  ### IO Placer revision
  
  - PnR is a iterative flow and hence, we can make changes to the environment variables in the fly to observe the changes in our design.
  - If i am required to change pin configuration along the core from randomly placed to some other placement, we use the below command in the openlane interactive window

  ```
  set ::env(FP_IO_MODE) 2
  ```

### SPICE Deck Creation and Simulation for CMOS inverter

  A SPICE deck includes information about the following:
  1. Model description
  2. Netlist description
  3. Component connectivity
  4. Component values
  5. Capacitance load
  6. Nodes
  7. Simulation type and parameters
  8. Libraries included

Before doing a SPICE simulation it is required for us to create a SPICE Deck,which provides information about various things such as:
1. Component Connectivity - Connectivity of the Vdd, Vss,Vin, substrate. Substrate tunes the threshold voltage of the MOS.
2. Component values - values of PMOS and NMOS, Output load, Input Gate Voltage, supply voltage.
3. Node identification
4. Simulation commands
5. Model file - This file will have information regarding the NMOS and PMOS paramenters of a particular technology.
<br />
In the below figures we can see the variation of waveforms when parameters are varied.<br />

![Screenshot from 2023-09-11 11-30-36](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/ac59fcda-aa48-476c-8988-ed671a166e43)

### CMOS Inverter Switching threshold Vm

It is the point with which the Vin = Vout on the DC transfer chara.<br />
Here,both transistors will be in saturation region, meaning both will be in the ON condition and 
there is a high chance of leakage current.Leakage current is the current which may flow directly 
from VDD to GND.

![Screenshot from 2023-09-11 11-32-38](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/1efd337e-53bd-40cd-9f58-0a57b2779bb8)
<br />
Through transient analysis, we calculate the rise and fall delays of the CMOS by SPICE Simulation

### Lab steps to git clone vsdstdcelldesign

We first clone the mag files and spice models of invertoer,pmos and nmos sky130 using the github link below.<br />
Cloning is done inside the openlane folder.<br />

```
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```
After cloning we are required to copy also the tech file into **vsdstdcelldesign** directory.
<br />
Then we run the magic command as shown below to get the layout.<br />

```
magic -T sky130A.tech sky130_inv.mag &
```
![Screenshot from 2023-09-11 12-02-21](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/cffbe0a7-fd3a-4e13-bb15-9b4877e90d45)

</details>

<details>
  <summary>Inception of Layout and CMOS Fabrication Process </summary>

  ### 16-Mask CMOS Fabrication

  16-Mask CMOS Fabrication encompasses several critical phases for crafting integrated circuits.<br />

  1. Substrate Selection.<br />
       This is the most initial phase of the process where the subrstrate is chosen.Here we are chosing a p-substrate.<br />
![Screenshot from 2023-09-11 12-47-12](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/56bccff0-3aa0-4d05-8449-ccbf714f1ce2)

  3. Active region creation.<br />
      This is done to isolate the active regions for transistors, the process begins with the deposition of SiO2 and Si3N4 layers, followed by photolithography and silicon nitride etching.This is also known as LOCOS (Local Oxidation of Silicon),where oxide is grown in certain regions. The Si3N4 layer is removed using hot H2SO4.<br />
        ![Screenshot from 2023-09-11 12-15-33](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/55adbf62-1aac-4281-9ea8-cccda07d10a1)

  4. N-Well and P-Well Formation.<br />
     The N-well and P-well regions are created separately.Ion implanation by Boron for P-well and by Phosphorous for N-well formation.High-temperature furnace processes drive-in diffusion to establish well depths, known as the tub process.<br />

![Screenshot from 2023-09-11 12-16-34](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/4853603c-08da-4d8c-8e63-8d42fbd96482)

  4. Gate Formation.<br />
     The gate is a very important CMOS transistor terminal that controls threshold voltages for transistor switching. NMOS and PMOS gates formed by photolithography techniques.Important parameters for gate formation include oxide capacitance and doping concentration.<br />
     
![Screenshot from 2023-09-11 12-18-13](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/74677788-550a-42bc-8b03-5072d93917f0)


  5. Lightly dopped Drain(LDD).<br />
     LDD formed to avoid the hot electron effect.<br />
 
![Screenshot from 2023-09-11 12-19-38](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/05c59b5f-5b14-4f76-84a5-e950b24c3505)


  6. Source and Drain Formation.<br />
      Screen oxide added to avoid channelling during implants followed by Aresenic implantation and high temperature annealing.<br />
      
![Screenshot from 2023-09-11 12-20-39](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/ae05225f-4262-4b8a-a237-855db1f2d15d)

  7. Local Interconnect Formation.<br />
     Removal of screen oxide by HF etching and deposition of Ti for low resistant contacts is done.Heat treatment results in chemical reactions, producing low-resistant titanium silicon dioxide for interconnect contacts and titanium nitride for top-level connections, enabling local communication.

  ![Screenshot from 2023-09-11 12-21-34](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/0bdb74ca-dffb-4a91-8dc2-5024cb82b86a)

  8. Higher Level Metal Formation.<br />
     Chemical Mechanical Polishing (CMP) is utilized by doping silicon oxide with Boron or Phosphorus to achieve surface planarization.This is followed up by TiN and Tungsten deposition.An aluminum (Al) layer is added and subjected to photolithography and CMP.This is the first interconnect and addditional interconnect layers can be added on top to reach higher level of metal layers.<br />
     At the end a dielectric layer usually Si3N4 is added ontop to protect the chip.<br />
     
![Screenshot from 2023-09-11 12-22-30](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/2255d6c2-6348-40b0-913a-55997138e106)

## Introduction to SKY130 basic layer layout and LEF using inverter

  We can see the layers which are required for CMOS inverter. We also see that the drains of both PMOS and NMOS are connected together.<br />
  NMOS source connected to ground(VGND), PMOS source is connected to VDD(VPWR).<br />
  In Sky130 the first layer is called the local interconnect layer or Locali.<br />

  The below screenshot shows the highlighted part in the layout and the same is shown in the tkcon window.<br />
  ![Screenshot from 2023-09-11 12-56-59](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/10181f6c-9871-45c7-ab67-3dd21ee80b70)

  ### Library exchange format(LEF)

  It is a format that tells us about the boundaries of a cell, the VDD and GND lines. It contains information about the logic of the circuit.<br />
  Tech LEF - has information about the Metal layer,DRC etc..<br />
  Marcro LEF - Contains physical information of cell like size, pin,direction.

## Designing standard cell and SPICE extraction in MAGIC

To extract the SPICE we open tkcon window.<br />
type 'pwd' to check the directory we are extracting to.<br />
The command 'extract all' is is used to to extract to the directory.<br />
To create a spice file using the .ext file,the commmands are.<br />

```
ext2spice cthresh 0 rthresh 0 //mothing is created in the directory with this command
```
Which extracts parasatic capacitances.
<br />
To create a file in the directory, we use the below command.<br />

```
ext2spice
```
The below screenshot illustrates this.<br />
![Screenshot from 2023-09-11 14-14-33](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/c23e4109-6b1f-4898-bfc7-5ebc94e6d450)

</details>

<details>
  <summary>Sky130 Tech file LABS</summary>

  ## Create Final SPICE Deck

  Here we go into the created spice file and make changes to it and simulate.<br />
  In the spicefile the nmos and pmos model details were defined along with the sub circuit details and the other parasitic capacitance information also.<br />

  We are going to be doing a transient analysis so we make the following changes to it.<br />
  1. VGND to VSS 0V
  2. Supply voltage VPWR to GND.
  3. Sweeping a pulse input.
  4. We add library files and change the scale to 0.01u
  5. Add a transient analysis with nessasary stoptime and precision as shown below.
  
![Screenshot from 2023-09-11 15-28-40](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/06db7f15-cc86-4386-89b0-e73b967d07b3)


  ## Using ngspice for SPICE Simulation

  Since the SPICE Deck is done,we run the simulation using ngspice.<br />
  
  ```
  ngspice sky130_inv.spice
  ```

  ![Screenshot from 2023-09-11 15-28-08](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/61e448c7-85ed-43e9-9eb1-604ed6b333f7)

To plot the graph using ngspice we are using the below code after opening ngspice.<br />

```
plot y vs time a
```
The below waveform is plotted hence.<br />
![Screenshot from 2023-09-16 09-21-04](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/181d7f73-f9d6-4fa5-8c39-5a42399b0713)

The spikes shown in the output(red) are caused due to low load capacitance.We can increase the cap value to sort this out.<br />

### Inverter Standard cell characterization

There are four timing parameters used to characterize the inverter standard cell:
1. Rise transition - Time taken for the output to rise from 20% to 80% of max value
2. Fall Transition: Time taken for the output to fall from 80% to 20% of max value
3. Cell Rise delay: difference in time(50% output rise) to time(50% input fall)
4. Cell Fall delay: difference in time(50% output fall) to time(50% input rise) 
<br />
In the ngspice waveform we can note down the values and calculate the above parameters.<br />

```Rise transition: 2.240 - 2.143 = 0.067ns (67ps)```

```Fall Transition: 4.0921 - 4.049 = 0.0431ns (43.1ps)```

```Cell Rise Delay : 2.17333 - 2.13 = 0.0433ns (43.33ps)```

```Cell Fall Delay : 4.076 - 4.0501 = 0.0259ns (25.9ps)```

## LAB exercise and DRC Challenges

### Introduction of Magic and Skywater DRC's

Here the following are done:
- In-depth overview of Magic DRC engine
- Introduction to Google/Skywater DRC rules
- Lab to warm up : Fixing a simple rule error
- Lab of main excersise : Fixing or creating a complex error

To know anything about magic use the following link:

```
http://opencircuitdesign.com/magic/
```
Majorly check out magic tutorails and magic command summary in the Using magic tab.<br />
Also do check out the technlogy file manual in the technology files tab.<br />

## Sky130s pdk intro and Steps to download labs

To view the documentation of Skywater pdks use the link below:

```
https://skywater-pdk.readthedocs.io/en/main/
```

We can view the rules associated with it there.<br />

We are downloading the packaged files to our local pc using the **wget** command. It stands for Web get . The following command is used.<br />

``` wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz ```

After this, extract it using the below command.

```
 tar xfz drc_tests.tgz
```
Once it is done. A drc_test folder is created in the directory which extraction is done.<br />
cd to that folder and run Magic.For better graphic use, the command belwo is used:

```
magic -d XR
```
To load a mag file we can load it using File > Open > .mag from the magic window .<br />
![Screenshot from 2023-09-16 11-00-51](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/c5b8d825-9b45-459e-ba4a-c0324a6c99f2)

Or we can use the terminal comand:

```
magic -d XR <filename>.mag
```

Select a particular block to check the DRC check. using ```drc why``` .<br />
We will use the following command in the tkcon window to see metal cut down.

```
cif see VIA2
```
![Screenshot from 2023-09-16 11-28-21](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/08529320-5525-4ac3-971f-b24b56ae6a04)


## Load Syky130 tech rules for DRC challenges

Here we will load the **poly.mag** file into Magic.
Now we find the error by moving the cursor and find **box** area. We find out that Poly.9 is violated due to the spacing between polyres and poly.We need to fix this.<br />

The polysilicon and polyres distance should be 22u is being shown as around 17u,and no errors. So we should go to the sky130 tech file and modify as below.<br />


```
after line
*******************************************************
spacing npres *nsd 480 touching_illegal \
	"poly.resistor spacing to N-tap < %d (poly.9)"
*******************************************************
we add one more line
*******************************************************
spacing npres allpolynonres 480 touching_illegal \
	"poly.resistor spacing to N-tap < %d (poly.9)"

```

```
after line
*******************************************************
spacing xhrpoly,uhrpoly,xpc alldiff 480 touching_illegal \
	"xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"
*******************************************************
we add one more line
*******************************************************
spacing xhrpoly,uhrpoly,xpc allpolynonres 480 touching_illegal \
	"xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"

```
As shown below.<br />
![Screenshot from 2023-09-16 12-04-23](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/37a1b77d-9091-4b09-a77d-0a7ae6ab7e7c)
![Screenshot from 2023-09-16 12-04-08](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/a90b8117-0229-41e5-8f67-e91e0f9669f2)

We then load the new tech file in the tkcon window and do a DRC check.<br />

![Screenshot from 2023-09-16 12-03-50](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/0a613a99-ea66-4b06-aee6-f39feb96838f)

###  Lab challenge exercise to describe DRC error as geometrical construct

Here we are going to use magic to run nwell.mag and try to descrive the DRC error as a geometrical construct.<br />

![Screenshot from 2023-09-16 12-27-03](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/7919cbf7-f3bf-4f4f-8d4b-8cd2d13e19de)

We see in the sky130 tech file,templayer for the dnwell. This is a supporting layer for the output layer to get a proper output.<br />

After loading the nwell.mag we are going to run the following commands and see the output result for the same.

```
cif  ostyle drc
```
![Screenshot from 2023-09-16 12-29-59](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/dd6ca46a-9610-4322-9aef-d11f90bc1990)

```
cif see dnwell_shrink
```
![Screenshot from 2023-09-16 12-30-23](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/7711975e-d759-4679-bf1e-01d485d24366)

```
feed clear
```
![Screenshot from 2023-09-16 12-31-16](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/ef5ffb99-5339-4e2b-bd82-c1ca9384fb74)
```
cif see nwell_missing
feed clear
```
![Screenshot from 2023-09-16 12-31-31](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/037e2c93-b27c-470b-ab0f-a0dd1a5702a8)

It is important to know that the cif generations are very much resource using so it may slow down or even crash magic. So its best to use general DRC rules whenever possible and put the cif outputs in a seperate style varient which runs on demand.<br />

DRC fast : intended for back end metal layer without checking layers below.<br />
DFC full : It checks for the full layout considering it is relatively small.<br />

![Screenshot from 2023-09-16 12-51-16](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/e20a85ff-b9ec-4cd5-9f28-72cea6d36064)


cif drcs is a set of rules that check layers exaclty as they appear.There are several of these out of which cifwidthmax with the width of 0 is the most conveinent one to use.<br />

</details>

## Day 4: Pre-layout timing analysis and importance of good clock tree

<details>
<summary>Timing modelling using delay tables</summary>

## Grid into track info

Track is a path on which metal layers are drawn for routing.It is used to define the height of the standard cell.

Guidelines to be followed while making a standard cell:
1. Input and output ports must lie on the intersection on Horizontal annd vertical tracks.
2. Width of standard cell must be in the odd multiple of track pitch & Height in the odd multiple of track height pitch.

The information to get the grids is defined in ```tracks.info```.
cd to the particular location and open the file.<br />

```
cd .volare/sky130A/libs.tech/openlane/sky130_fd_sc_hd/tracks.info

```
The content of the file are:

```
li1 X 0.23 0.46  //0.46um is the width  
li1 Y 0.17 0.34  //0.34um is the height 
met1 X 0.17 0.34
met1 Y 0.17 0.34
met2 X 0.23 0.46
met2 Y 0.23 0.46
met3 X 0.34 0.68
met3 Y 0.34 0.68
met4 X 0.46 0.92
met4 Y 0.46 0.92
met5 X 1.70 3.40
met5 Y 1.70 3.40
```

We iput the below command in the tkcon window to get grid on magic.<br />

```
grid 0.46um 0.34um 0.23um 0.17um
```
![Screenshot from 2023-09-16 14-22-54](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/7e36ff49-628b-4290-a908-6d4028bf71fe)


## Create Port Definition

After the layout is made we need to extract the LEF file for the cell. But, certain properties and defenitions have to be set to the pins of the cell which aid the placer and router tool. For LEF files, a cell that contains ports is written as a macro cell,and the ports are the declared PINs of the macro.<br />

Defining port and setting correct class and use attributes to each port is the first step.
<br />
We highlight the port that we want to define in magic, Then Edit > Text and change values as below.<br />
For each layer (to be turned into port), make a box on that particular layer and input a label name along with a sticky label of the layer name with which the port needs to be associated. Ensure the Port enable checkbox is checked and default checkbox is unchecked as shown in the figure:

![Screenshot from 2023-09-16 14-43-12](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/48a231c1-304b-45e5-b4cf-2e815fdef8e1)

![Screenshot from 2023-09-16 14-45-04](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/639090b4-b09f-4f96-92fb-d9a1ccce1e9c)

The same needs to be done for the VPWR and VGND except the Attached to layer must be changed to metal1.<br />

![Screenshot from 2023-09-16 14-56-22](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/72511b42-dcd6-4258-b82e-807c0140a11b)

![Screenshot from 2023-09-16 14-57-02](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/55c95c7e-7271-4bcf-a8e9-0516e796589f)

Before the CMOS Inverter standard cell LEF is extracted,and the purpose of ports must be defined.<br />

Port A:
```
port class input
port use signal
```
Port Y:
```
port class output
port class signal
```
VPWR area:
```
port class inout
port use power
```
VGND area:
```
port class inout
port use ground
```

The below command is also run on tkcon for extracting LEF file into the same directory.
```
lef write // if no name is specified it will be the same name as mag file
```
![Screenshot from 2023-09-16 15-14-32](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/64458ba7-cff8-43f3-a436-5077a7913e03)

This creates the file below:<br />

```
VERSION 5.7 ;
  NOWIREEXTENSIONATPIN ON ;
  DIVIDERCHAR "/" ;
  BUSBITCHARS "[]" ;
MACRO sky130_vsdinv
  CLASS CORE ;
  FOREIGN sky130_vsdinv ;
  ORIGIN 0.000 0.000 ;
  SIZE 1.380 BY 2.720 ;
  SITE unithd ;
  PIN A
    DIRECTION INPUT ;
    USE SIGNAL ;
    ANTENNAGATEAREA 0.165600 ;
    PORT
      LAYER li1 ;
        RECT 0.060 1.180 0.510 1.690 ;
    END
  END A
  PIN Y
    DIRECTION OUTPUT ;
    USE SIGNAL ;
    ANTENNADIFFAREA 0.287800 ;
    PORT
      LAYER li1 ;
        RECT 0.760 1.960 1.100 2.330 ;
        RECT 0.880 1.690 1.050 1.960 ;
        RECT 0.880 1.180 1.330 1.690 ;
        RECT 0.880 0.760 1.050 1.180 ;
        RECT 0.780 0.410 1.130 0.760 ;
    END
  END Y
  PIN VPWR
    DIRECTION INOUT ;
    USE POWER ;
    PORT
      LAYER nwell ;
        RECT -0.200 1.140 1.570 3.040 ;
      LAYER li1 ;
        RECT -0.200 2.580 1.430 2.900 ;
        RECT 0.180 2.330 0.350 2.580 ;
        RECT 0.100 1.970 0.440 2.330 ;
      LAYER mcon ;
        RECT 0.230 2.640 0.400 2.810 ;
        RECT 1.000 2.650 1.170 2.820 ;
      LAYER met1 ;
        RECT -0.200 2.480 1.570 2.960 ;
    END
  END VPWR
  PIN VGND
    DIRECTION INOUT ;
    USE GROUND ;
    PORT
      LAYER li1 ;
        RECT 0.100 0.410 0.450 0.760 ;
        RECT 0.150 0.210 0.380 0.410 ;
        RECT 0.000 -0.150 1.460 0.210 ;
      LAYER mcon ;
        RECT 0.210 -0.090 0.380 0.080 ;
        RECT 1.050 -0.090 1.220 0.080 ;
      LAYER met1 ;
        RECT -0.110 -0.240 1.570 0.240 ;
    END
  END VGND
END sky130_vsdinv
END LIBRARY

```
### Integrating custom cell in OpenLANE

To include the new standard cell in the synthesis, we need to copy the lef file which we have generated to the ```/designs/picorv32a/src``` directory. The **sky130_fd_sc_hd_typical.lib** ,
**sky130_fd_sc_hd__fast.lib** ,**sky130_fd_sc_hd__slow.lib** file from ```vsdstdcelldesign/libs``` directory needs to be copied to the ```designs/picorv32a/src``` directory.

Now we need to modify the the **config.json** file as shown below.<br />

```
"PL_RANDOM_GLB_PLACEMENT": 1,
"PL_TARGET_DENSITY": 0.5,
"FP_SIZING": "relative",
"LIB_SYNTH":"dir::src/sky130_fd_sc_hd__typical.lib",
"LIB_FASTEST":"dir::src/sky130_fd_sc_hd__fast.lib",
"LIB_SLOWEST":"dir::src/sky130_fd_sc_hd__slow.lib",
"LIB_TYPICAL":"dir::src/sky130_fd_sc_hd__typical.lib",
"TEST_EXTERNAL_GLOB":"dir::../picorv32a/src/*",
"SYNTH_DRIVING_CELL":"sky130_vsdinv"
```

Now we invoke OpenLANE as usual to integrate the standard cell in the OpenLANE flow.<br />
Use the following commands in openlane.

```
prep -design picorv32a 
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```

![Screenshot from 2023-09-16 17-16-16](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/bb242503-567f-4d38-a03c-f31b30885b03)

Synthesis report:<br />
![Screenshot from 2023-09-16 17-15-22](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/adc9c1a2-12e9-4a41-927d-d543ca0d7c9b)
<br />

STA report:<br />
![Screenshot from 2023-09-16 17-15-50](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/e82efbf3-e060-4ea1-87f8-66a61f61f1a4)
<br />

This is followed by floorplan and placement.

```
run_floorplan
run_placement
```
To check the layout invoke magic from the directory:
```/runs/RUN_2023.09.16_11.41.17/ ```

```
magic -T /home/emil/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def &

```

Below is the output obtained in magic:
<br />

![Screenshot from 2023-09-16 18-05-01](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/1278d844-c5d7-41df-9032-9100fb07194f)

![Screenshot from 2023-09-16 18-06-17](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/8745804a-68b0-4bd9-b66b-20305965b9e1)


### Introduction to Delay tables

Delay is a parameter that has huge impact on our cells in the design. Delay decides each and 
every other factor in timing. For a cell with different size, threshold voltages, delay model 
table is created where we can it as timing table. Delay of a cell depends on input transition 
and out load. Lets say two scenarios, we have long wire and the cell(X1) is sitting at the end 
of the wire : the delay of this cell will be different because of the bad transition that 
caused due to the resistance and capcitances on the long wire. we have the same cell sitting at 
the end of the short wire: the delay of this will be different since the tarn is not that bad 
comapred to the earlier scenario. Eventhough both are same cells, depending upon the input 
tran, the delay got chaned. Same goes with o/p load also.
<br />
VLSI engineers have figured out some important rules for adding signal boosters to make sure 
the signals stay strong. They've noticed that these boosters need to be a certain size, but 
their speed can change depending on how much work they have to do. To deal with this, they came 
up with the idea of "delay tables." These tables are like charts that show how fast the 
boosters work based on the signal's starting speed and how much work they need to handle. These 
charts help plan how the design should work.
<br />
In order to avoid large skew between endpoints of a clock treE:
1. Buffers on the same level must have same capacitive load to ensure same timing delay or latency on the same level.
2. Buffers on the same level must also be the same size (different buffer sizes -> different W/L ratio -> different resistance -> different RC constant -> different delay)

![Screenshot from 2023-09-16 18-27-53](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/27a56c26-7f16-42eb-851c-7a5fa8a8f009)

Buffers at various levels may have varying sizes and capacitive loads. However, if buffers at 
the same level share the same size and load, the total delay for each path in the clock tree 
will remain consistent, keeping the skew at zero. This implies that different levels will 
exhibit differences in input transitions and output capacitive loads, leading to varying delays.
<br />
Delay tables, which are contained within the liberty file, are employed to record the timing 
characteristics of each cell. The primary determinant of delay is the output slew, which, in 
turn, is influenced by both the capacitive load and the input slew. The input slew, on the 
other hand, is determined by the output capacitance load and input slew of the preceding 
buffer, and it possesses its transition delay table.

</details>

<details>
<summary>Timing analysis with ideal clocks using OpenSTA</summary>

### Post-synthesis timing analysis Using OpenSTA

Timing analysis is carried out outside the OpenLANE flow using OpenSTA tool. For this, 
pre_sta.conf is required to carry out the STA analysis. Invoke OpenSTA outside the openLANE 
flow as follows:

```
sta pre_sta.conf

```
Since clock tree synthesis has not been performed yet, the analysis is with respect to ideal 
clocks and only setup time slack is taken into consideration. The slack value is the difference 
between data required time and data arrival time. The worst slack value must be greater than or 
equal to zero. If a negative slack is obtained, following steps may be followed:
1. Change synthesis strategy, synthesis buffering and synthesis sizing values
2. Review maximum fanout of cells and replace cells with high fanout
3. sdc file for OpenSTA is modified.

base.sdc is located in vsdstdcelldesigns/extras directory. So, I copied it into our design folder using
```cp my_base.sdc /home/emil/OpenLane/designs/picorv32a/src/```

![Screenshot from 2023-09-16 19-34-42](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/638bd393-08f9-49b3-8851-aeecef655c30)

Since there were no timing violations, I skipped this step.Since clock is propagated only once 
we do CTS, In placement stage, clock is considered to be ideal. So only setup slack is taken 
into consideration before CTS.<br />

The clock is produced by a PLL (Phase-Locked Loop) that contains internal circuits and some 
logic. The generation of the clock can vary depending on the specific circuit configuration. 
These variations are collectively referred to as "clock uncertainty." Within clock uncertainty, 
one of the factors is jitter, which means there's uncertainty about whether the clock will 
arrive precisely on time without any deviation. This is why it's called "clock uncertainty." 
Skew, jitter, and margin are all aspects that contribute to this uncertainty in the timing of 
the clock signal.

```Clock Jitter : deviation of clock edge from its original position```
	
</details>

<details>
<summary>Clock tree synthesis TritonCTS and signal integrity</summary>

 Clock Tree Synthesis (CTS) plays a vital role in the creation of integrated circuits (ICs), 
 particularly in the realm of digital electronics, where precise timing is of utmost
 importance. CTS involves the establishment of an organized network or structure of pathways 
 for distributing the clock signal within the IC. This meticulous process guarantees that the 
 clock signal effectively reaches all the sequential components, such as flip-flops and 
 registers, in a synchronized and punctual fashion.

 It can be implemeted in various ways and the choice of the specific technique depends on the 
 design requirements, constraints, and goals.<br />
 Some of the different types of approches to clock tree synthesis are:
 - Balanced Tree CTS: The clock signal is spread out evenly, like branches of a tree. This helps ensure that all parts of the chip get the clock at about the same time, reducing timing problems. It's a straightforward method, but it might not save as much power as other methods.
 - H-tree CTS: It is like a tree shape with the letter "H." It's great for spreading out clock signals across big chips. This tree structure helps make sure the timing is good and saves power, especially in large areas of the chip.
 - Star CTS: In a star CTS, the clock signal is distributed from a single central point (like a star) to all the flip-flops. This approach simplifies clock distribution and minimizes clock skew but may require a higher number of buffers near the source.
 - Mesh CTS: In a mesh CTS, clock wires are arranged in a mesh-like grid pattern, and each flip-flop is connected to the nearest available clock wire. It is often used in highly regular and structured designs, such as memory arrays. Mesh CTS can offer a balance between simplicity and skew minimization.
 - Adaptive CTS: Adaptive CTS techniques adjust the clock tree structure dynamically based on the timing and congestion constraints of the design. This approach allows for greater flexibility and adaptability in meeting design goals but may be more complex to implement.

### Crosstalk in VLSI

Crosstalk in VLSI refers to unwanted interference or coupling between adjacent conductive 
traces or wires on an integrated circuit (IC) or chip. It occurs when the electrical signals on 
one wire influence or disrupt the signals on neighboring wires.Uncontrolled crosstalk can lead 
to data corruption, timing violations, and increased power consumption. Mitigation: VLSI 
designers employ various techniques to mitigate crosstalk, such as optimizing layout and 
routing, using appropriate shielding, implementing proper clock distribution strategies, and 
utilizing clock gating to reduce dynamic power consumption when logic is idle

### Clock net sheilding in VLSI

Clock net shielding in VLSI refers to a technique used to protect the clock signal from 
interference or crosstalk. The clock signal is critical for synchronizing the operations of 
various components on a chip, and any interference can lead to timing issues and performance 
problems.<br />
VLSI designers may use shielding techniques to isolate the clock network from other signals, 
reducing the risk of interference. This can include dedicated clock routing layers, clock tree 
synthesis algorithms, and buffer insertion to manage clock distribution more effectively. 
<br />
VLSI designs often have multiple clock domains. Shielding and proper clock gating help ensure 
that clock signals do not propagate between domains, avoiding metastability issues and 
maintaining synchronization.

### CTS LAB

The below command is used to run CTS in OpenLANE

```
run_cts 
```
![Screenshot from 2023-09-16 19-52-21](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/86eac546-e7f5-4412-8897-9531b0709506)

<br />

![Screenshot from 2023-09-16 19-54-25](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/a1037bc4-172a-4b1c-9d92-fb81eb9448d3)

After CTS run, my slack values are ```setup:12.36, Hold:0.38```
<br />
Here also both values are not violating.<br />

</details>
<details>
<summary>Timing analysis with real clocks</summary>

### Setup Timing Analysis using real clocks

Analyzing setup time is a crucial element of designing digital circuits, especially in 
synchronous digital systems. It pertains to the duration during which a signal must remain 
steady and valid prior to the arrival of the clock edge. Guaranteeing the fulfillment of setup 
time prerequisites is vital for averting data errors and securing the correct functioning of 
the digital circuit.<br />

![Screenshot from 2023-09-16 22-59-09](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/168624e6-ca84-4ff8-96cb-19502aaffba8)

To ensure the setup time requirements are met we need to make sure of some things:
1. Selecting proper Filp flops or latches.
2. Optimize combinational logic
3. Clock Skew Analysis
4. Timing constraints

<br />
Meeting setup time requrirements is cruical for a good digital circuit operation. If not done can result in data errors and multifunctioning of the circuit.

### Holding Timing Analysis using real clock

Analysis of hold time is an equally vital component of digital circuit design, especially in 
synchronous systems. It concerns the minimum duration during which a data input (D) needs to 
maintain its stability and validity after the clock edge before any changes can occur. Ensuring 
that hold time requirements are met is essential to prevent data corruption and ensure the 
proper operation of digital circuits.<br />

![Screenshot from 2023-09-16 23-03-33](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/499f97b7-df4a-4b45-b6b6-f3beb15621ea)

<br />
Since, clock is propagated, from this stage, we do timing analysis with real clocks. From now 
post cts analysis is performed by operoad within the openlane flow

```
openroad
read_lef /home/emil/OpenLane/designs/picorv32a/runs/RUN_2023.09.17_04.44.22/tmp/merged.nom.lef 
read_def /home/emil/OpenLane/designs/picorv32a/runs/RUN_2023.09.17_04.44.22/results/cts/picorv32.def 
read_verilog /home/emil/OpenLane/designs/picorv32a/runs/RUN_2023.09.17_04.44.22/results/synthesis/picorv32.v
write_db pico_cts.db
read_db pico_cts.db
read_verilog /home/emil/OpenLane/designs/picorv32a/runs/RUN_2023.09.17_04.44.22/results/synthesis/picorv32.v
link_design picorv32
read_liberty $::env(LIB_SYNTH_COMPLETE)
read_sdc /home/emil/OpenLane/designs/picorv32a/src/my_base.sdc
set_propagated_clock (all_clocks)
report_checks -path_delay min_max -format full_clock_expanded -digits 4

```

### Hold Slack

![Screenshot from 2023-09-17 10-21-55](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/7ec39dbe-8d6d-439f-a4c0-4dcd9a8a81d7)

### Setup Slack

![Screenshot from 2023-09-17 10-22-14](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/d44628b4-21e8-4bf5-b110-93b88391109b)

</details>

## Day 5:Final steps for RTL2GDS using tritonRoute and OpenSTA

<details>
<summary>Maze routing and Lee's Algorithm</summary>

 Routing is the process of establishing a physical connection between two pins. Algorithms 
 designed for routing take source and target pins and aim to find the most efficient path 
 between them, ensuring a valid connection exists.<br />

 The Maze Routing algorithm, such as the Lee algorithm, is one approach for solving routing 
 problems.Here a grid similar to the one created during cell customization is utilized for 
 routing purposes.<br />
 The Lee algorithm starts with two designated points, the source and target, and leverages the
 routing grid to identify the shortest or optimal route between them.<br />

 Lee's Algorithm has its limitations. It can be time consuming when dealing with millions of 
 pins.It essentially constructs a maze and then numbers its cells from the source to the target.
 here are alternative algorithms that address similar routing challenges.<br />

 Here in this case he shortest path is one that follows a steady increment of one.There might 
 be multiple paths, but the best path that the tool will choose is one with less bends.The 
 route should not be diagonal and must not overlap an obstruction such as macros. The Lee 
 algorithm prioritizes selecting the best path, typically favoring L-shaped routes over 
 zigzags. If no L-shaped paths are available, it may resort to zigzag routes. This approach is 
 particularly valuable for global routing tasks.<br />
 
 This algorithm however has high run time and consume a lot of memory thus more optimized 
 routing algorithm is preferred .

 ![Screenshot from 2023-09-17 11-22-59](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/d3b5d913-42eb-49c1-93e4-1a8e35cdc7a1)

 ### Design Rule Check

 Design rule checks are physical checks of metal width, pitch and spacing requirement for the 
 different layers which depend on different technology nodes.It verifies whether a design meets 
 the predefined process technology rules given by the foundry for its manufacturing.<br />

 The layout of a design must be in accordance with a set of predefined technology rules given 
 by the foundry for manufacturability. After completion of the layout and its physical 
 connection, an automatic program will check each and every polygon in the design against these 
 design rules and report any violations.<br />
 
![268457324-72931273-1da5-4031-a712-766239e59516](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/5ece676c-06fd-4ec5-92fa-49a545dbc5b0)

</details>

<details>
<summary>Power Distribution Network Generation</summary>
<br />
Unlike the general ASIC flow, Power Distribution Network generation is not a part of floorplan 
run in OpenLANE. PDN must be generated after CTS and post-CTS STA analyses:

we can check whether PDN has been created or no by check the current def environment variable:  ```echo $::env(CURRENT_DEF)```

```
prep -design picorv32a -tag <RUN file name>
gen_pdn

```

![Screenshot from 2023-09-17 14-18-13](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/73821f80-aae2-4cee-a41d-db557cd63bf0)

![Screenshot from 2023-09-17 14-21-54](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/fcb9d3cc-800e-4f7e-8ed6-b3dd10192a39)

- **gen_pdn** Generates the power distribution network.
- The power distribution network has to take the design_cts.def as the input def file.
- Power rings,strapes and rails are created by PDN.
- From VDD and VSS pads, power is drawn to power rings.
- Next, the horizontal and vertical strapes connected to rings draw the power from strapes.
- Stapes are connected to rings and these rings are connected to std cells. So, standard cells get power from rails.
- here are definitions for the straps and the rails. In this design, straps are at metal layer 4 and 5 and the standard cell rails are at the metal layer 1. Vias connect accross the layers as required.

  ![268351074-ced030b9-e887-4417-a9bd-039287ed88e5](https://github.com/mrdunker/Advanced_Physical_Design_using_OpenLANE-Sky130/assets/38190245/a71cf1bb-fd37-415b-be51-8e0ef1a212ac)

</details>

<details>
<summary>Routing</summary>	
<br />
	
In the realm of routing within Electronic Design Automation (EDA) tools, such as both OpenLANE 
and commercial EDA tools, the routing process is exceptionally intricate due to the vast design 
space. To simplify this complexity, the routing procedure is typically divided into two 
distinct stages: Global Routing and Detailed Routing.<br />

There are two kinds of routing:
1. Global Routing: In this stage, the routing region is subdivided into rectangular grid cells and represented as a coarse 3D routing graph. This task is accomplished by the "FASTE ROUTE" engine.
2. Detailed Routing: Here, finer grid granularity and routing guides are employed to implement the physical wiring. The "tritonRoute" engine comes into play at this stage. "Fast Route" generates initial routing guides, while "Triton Route" utilizes the Global Route information and further refines the routing, employing various strategies and optimizations to determine the most optimal path for connecting the pins

### Trion Route

Key Features:
- **Initial Detail Routing**: TritonRoute initiates the detailed routing process, providing the foundation for the subsequent routing steps.
- **Adherence to Pre-Processed Route Guides**:TritonRoute places significant emphasis on following pre-processed route guides. This involves several actions:
  	- Initial Route Guide Analysis
  	- Guide Splitting
  	- Guide Merging
  	- Guide Bridging
  	- Assumes route guide for each net satisfy inter guide connectivity Same metal layer with touching guides or neighbouring metal layers with nonzero vertically overlapped area


</details>








