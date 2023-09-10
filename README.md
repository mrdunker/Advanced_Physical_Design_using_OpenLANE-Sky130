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

