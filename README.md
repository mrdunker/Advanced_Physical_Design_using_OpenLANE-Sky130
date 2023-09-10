# Advanced_Physical_Design_using_OpenLANE-Sky130

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

</details>


