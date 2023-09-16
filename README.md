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



</details>
