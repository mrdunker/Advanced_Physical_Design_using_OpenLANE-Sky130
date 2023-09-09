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
  <summary>SoC Design using OpenLane</summary>
</details>

