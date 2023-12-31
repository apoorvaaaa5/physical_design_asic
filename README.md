# PHYSICAL_DESIGN_ASIC
The objective of VLSI (Very Large Scale Integration) physical design for ASICs (Application-Specific Integrated Circuits) is to transform a digital circuit's logical representation into a physical layout that meets various performance, power, area, and manufacturability requirements.
# SKILL_OUTCOMES
* Architectural Design
* RTL Design / Behavioral Modeling
* Floorplanning
* placement
* clock Tree Synthesis
* Routing
# INTRODUCTION_TO_BASIC_KEYWORDS
## INTRODUCTION ##
* ISA(Instruction Set Architecture)
   * ISA defines the interface between a computer's hardware and its software, specifically how the processor and its components interact with the software instructions that drive the execution of tasks.
   * It encompasses a set of instructions, addressing modes, data types, registers, memory organization, and the mechanisms for executing and managing instructions.
* RISC-V (Reduced Instruction Set Computing - Five).
     * It is an open-source Instruction Set Architecture (ISA) that has gained significant attention and adoption in the world of computer architecture and semiconductor design.
     * RISC architectures simplify the instruction set by focusing on a smaller set of instructions, each of which can be executed in a single clock cycle. This approach usually leads to faster execution of individual instructions.
## From_Apps_To_Hardware ##
1.__Apps__: Application software, often referred to simply as "applications" or "apps," is a type of computer software that is designed to perform specific tasks or functions for end-users.

2.__System software__: System software refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. It provides essential services, manages hardware resources, and enables the execution of application programs. System software plays a critical role in maintaining the overall functionality, security, and performance of a computer system.'

3.__Operating System__: The operating system is a fundamental piece of software that manages hardware resources and provides various services for both users and application programs. It controls tasks such as memory management, process scheduling, file system management, and user interface interaction. Examples of operating systems include Microsoft Windows, macOS, Linux, and Android.

4.__Compiler__: A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.

5.__Assembler__: An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.

6.__RTL__: RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.

7.__Hardware__: Hardware refers to the physical components of a computer system or any electronic device. It encompasses all the tangible parts that make up a computing or electronic device and enable it to perform various tasks.

## Detail Description of Course Content ##
__Pseudo Instructions__: Pseudo-instructions are used to simplify programming, improve code readability, and reduce the number of explicit instructions a programmer needs to write. They are especially useful for common programming patterns that involve multiple instructions. Ex: li, mv.

__Base Integer Instructions__: The term "base integer instructions" refers to the fundamental set of instructions that form the foundation for performing basic arithmetic, logical, and data movement operations. Ex: add, sub, and, or, xor, sll.

__Multiply Extension Intructions__: The RISC-V architecture includes a set of multiply and multiply-accumulate (MAC) extension instructions that enhance the instruction set to perform efficient multiplication and multiplication-accumulate operations. Ex: mul, mulh, mulhu, mulhsu.

__Single and Double Precision Floating Point Extension__: The RISC-V architecture includes floating-point extensions that provide support for both single-precision (32-bit) and double-precision (64-bit) floating-point arithmetic operations. These extensions are often referred to as the "F" and "D" extensions, respectively. Floating-point arithmetic is essential for handling real numbers with fractional parts and for performing accurate calculations involving decimal values.

__Application Binary Interface__: ABI stands for "Application Binary Interface." It is a set of rules and conventions that govern how software components interact with each other at the binary level. The ABI defines various aspects of program execution, including how function calls are made, how parameters are passed and returned, how memory is allocated and managed, and more.

__Memory Allocation and Stack Pointer__

* Memory allocation refers to the process of assigning and managing memory segments for various data structures, variables, and objects used by a program. It involves allocating memory space from the system's memory pool and releasing it when it is no longer needed to prevent memory leaks.
* The stack pointer is a register used by a program to keep track of the current position of the program's execution on the call stack.
  
# Labwork_for_RISCV_Toolchain
## C_Program
We wrote a C program for calculating the sum from 1 to n using a text editor, leafpad.

leafpad sumton.c

#include<stdio.h>

int main(){

	int i, sum=0, n=26;
 
	for (i=1;i<=n; ++i) {
 
	sum +=i;
 
	}
 
	printf("Sum of numbers from 1 to %d is %d \n",n,sum);
 
	return 0;
 
}


Using the gcc compiler, we compiled the program to get the output.

gcc sumton.c .\a.out
![eea605fb-9b1c-4ac0-a5eb-e0175fca2cc3](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/b3b2f8eb-c94a-4937-82ee-be2fad1c6158)


## RISCV_GCC_Compiler_and_Dissemble
Using the riscv gcc compiler riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sumton.o sumton.c, we compiled the C program.
![9476ab0e-6e25-4e19-93f8-a0144a679f57](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/d2f78638-2429-4884-a54c-04a71ad2d47c)

To get the assembly code for the C program, riscv64-unknown-elf-objdump -d sumton.o | less .

In order to view the main section, type /main.

Here, since we used -O1 optimisation, the number of instructions are 14.

![f320b0d1-b79d-4255-a33f-fc172d5f26ab](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/a7cbf190-2530-49a1-976f-713c79c9f3bd)

When we use -Ofast optimisation, we can see that the number of instructions have been 11

![00fb376e-42d7-4fd6-86e0-50c777c9c53f](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/504b9bec-0d22-4ff2-adce-421265dceacf)

## Spike_Simulation_and_Debug
spike pk sum1ton.o is used to check whether the instructions produced are right to give the correct output.
![9476ab0e-6e25-4e19-93f8-a0144a679f57](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/5846c26b-6a56-4e72-82c7-25610dbdcae2)

spike -d pk sum1ton.c is used for debugging.

The contents of the registers can also be viewed.

![525f4c62-8771-41d9-a3f3-bee8d863767d](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/b21da529-beb9-4918-aa93-fe909cfc31b7)

# Integer Number Representation
## Unsigned Numbers
* Unsigned numbers, also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.
* Range: 0 to 2^(N) - 1.
## Signed Numbers
* Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.
* Range : -(2^(N-1)) to 2^(N-1) - 1.
## Labwork
### Unsigned 64-bit Number
#include <stdio.h>
#include <math.h>

int main(){

	unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
 
	unsigned long long int min = (unsigned long long int) (pow(2,64) *(-1));
 
	printf("lowest number represented by unsigned 64-bit integer is %llu\n",min);
 
	printf("highest number represented by unsigned 64-bit integer is %llu\n",max);
 
	return 0;
}


![4c1b9763-f327-42a2-9e01-b2cabd2d4bb1](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/c11446f5-b85d-41d9-b2f9-15065a4ad845)

### Signed 64-bit Number
#include <stdio.h>
#include <math.h>

int main(){

	long long int max = (long long int) (pow(2,63) -1);
 
	long long int min = (long long int) (pow(2,63) *(-1));
 
	printf("lowest number represented by signed 64-bit integer is %lld\n",min);
 
	printf("highest number represented by signed 64-bit integer is %lld\n",max);
 
	return 0;
}


![5deac719-8be3-4e35-8d74-127167b288ab](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/3bc3beeb-4801-4913-9c5b-a21bf19b008f)

# Application Binary Interface
## Introduction to ABI
* An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.
* The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.
## Memmory Allocation for Double Words
64-bit number (or any multi-byte value) can be loaded into memory in little-endian or big-endian. It involves understanding the byte order and arranging the bytes accordingly
1. Little-Endian: In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
2. Big-Endian: In big-endian representation, you store the most significant byte (MSB) at the lowest memory address and the least significant byte (LSB) at the highest memory address.
   
For example, consider the 64-bit hexadecimal value 0x0123456789ABCDEF.
In Little-Endian representation, it would be stored as follows in memory:

![261368957-307fabf6-7f58-4337-8171-6d62d99a4386](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/785dce04-3042-4f5f-ad81-b78d7d9bfd9b)

In Big-Endian representation, it would be stored as follows in memory:

![261369046-aa53e082-5878-4e3f-948a-f6f080ed0ed2](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/11ef4771-687c-494f-b034-7cd66984f1cd)

## Load, Add and Store Instructions
Load, Add, and Store instructions are fundamental operations in computer architecture and assembly programming. They are often used to manipulate data within a computer's memory and registers.
 1. Load Instructions: Load instructions are used to transfer data from memory to registers. They allow you to fetch data from a specified memory address and place it into a register for further processing.
Example ld x6, 8(x5)

In this Example
* ld is the load double-word instruction.
* x6 is the destination register.
* 8(x5) is the memory address pointed to by register x5 (base address + offset).

2. Store Instructions: Store instructions are used to write data from registers into memory.They store values from registers into memory addresses
  Example sd x8, 8(x9)

In this Example
* sd is the store double-word instruction.
* x8 is the source register.
* 8(x9) is the memory address pointed to by register x9 (base address + offset).

3. Add Instructions: Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.
Example add x9, x10, x11

In this Example
* add is the add instruction.
* x9 is the destination register.
* x10 and x11 are the source registers.

## 32-Registers and their ABI Names
The choice of the number of registers in a processor's architecture, such as the RISC-V RV64 architecture with its 32 general-purpose registers, involves a trade-off between various factors. While modern processors can have more registers but increasing the number of registers could lead to larger instructions, which would take up more memory and potentially slow down instruction fetch and decode.
### ABI Names
ABI names for registers serve as a standardized way to designate the purpose and usage of specific registers within a software ecosystem. These names play a critical role in maintaining compatibility, optimizing code generation, and facilitating communication between different software components.

![261481755-b735fc44-0c08-40e8-8303-c338647dbd9f](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/96f20c7b-2ebc-48f2-b84c-8b06ce76fc65)

# Labwork using ABI Function Calls
## Algorithm for C Program using ASM
* Incorporating assembly language code into a C program can be done using inline assembly or by linking separate assembly files with your C code.
* When you call an assembly function from your C code, the C calling convention is followed, including pushing arguments onto the stack or passing them in registers as required.
* The program executes the assembly function, following the assembly instructions you've provided.
  
![261504893-1d76b7ef-cac9-4331-9190-31af36525e0c](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/f0ee3483-1d99-41c1-9f2c-1a2d0430ed3e)

## Review ASM Function Calls
* You write your C code in one file and your assembly code in a separate file.
* In the assembly file, you declare assembly functions with appropriate signatures that match the calling conventions of your platform.
  
  __C PROGRAM__
  
  ![6f49376f-d8c4-4abc-8dd1-48135d693f38](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/523c50af-3617-45b3-a812-59d19b52463a)
  
__Asseembly File__

![013479e4-03d3-41b5-a798-f0bb4207fcab](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/9c47dff4-9ca5-4462-aefc-5c3d94362f45)

## Simulate C Program using Function Call
__Compilation__: To compile C code and Asseembly file use the command riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o custom1to9.o custom1to9.c load.s this would generate object file custom1to9.o.
__Execution__: To execute the object file run the command spike pk custom1to9.o

![8aef424e-986d-4681-8062-5bfd16df84c0](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/76d79352-a151-479c-b788-c6f40a829926)

## Lab to Run C-Program on RISCV-CPU
git clone https://github.com/kunalg123/riscv_workshop_collaterals.git

cd riscv_workshop_collaterals

ls -ltr

cd labs

ls -ltr

chmod 777 rv32im.sh

./rv32im.sh


![Screenshot from 2023-08-25 14-04-26](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/febd31f6-5ec7-433c-b712-db9952fc73d8)

# Introduction to Open-Source Simulator iVerilog
## Introduction to iVerilog Design Testbench
### Simulator
* It is a tool used for simulating the design. It looks for the changes on the input signals to evaluate the outputs.
* If there is no change in the inputs, the simulator doesn't evaluate the outputs.
* RTL is checked for adherence to the spec by simulating the design.
* The tool used here is iverilog .

### iVerilog
* It is an open-source Verilog simulator used for testing and simulating digital circuit designs described in the Verilog hardware description language (HDL).
* Both the design and the testbench are fed to the simulator and it produces a vcd (value change dump) file.
* In order to view the vcd file, we use the GTKwave where we can see the wave forms.
  
<img width="567" alt="263460822-37b643b5-e41e-425d-85f0-a55d7e190571" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/75d06a84-a530-4ff2-8120-38549b7bee1c">

###   Design
* It is the actual verilog code or set of verilog codes which ahs the intended functionality to meet with the required specifications.
* Verilog is used to describe the behavior and structure of digital circuits at different levels of abstraction, from high-level system descriptions down to low-level gate-level representations.

### Testbench
* A testbench is a specialized Verilog module or program used to verify the functionality and behavior of another Verilog module, circuit, or design. Testbenches are essential for testing and simulating digital designs before they are synthesized or manufactured as physical chips.

* It is a setup to apply stimulus to the design to check its functionality.
  
<img width="526" alt="263461152-72e6ffe4-abba-41f1-b79f-240f125b410b" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/eabc652b-3a84-4db9-8643-b5620dbe545f">

# Labs using iVerilog and GTKwave
## Introduction to Lab
* Make a directory named vsd mkdir vsd.
* cd vsd.
* git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
* Creates a folder called sky130RTLDesignAndSynthesisWorkshop in the vsd directory.
  
![95a4c360-2705-4aa2-b014-644029aad20d](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/58dfadeb-5983-4bba-9b0c-1eb87b65af38)

* my_lib : contains all the library files

* lib : contains sky130 standard cell library used for our synthesis

* verilog_model : contains all the standard cell verilog modules of the standard cells contained in the .lib

* verilog_files : contains all the verilog source files and testbench files which are required for labs

  ## iVerilog GTKwave Part-1
  * cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

* we have loaded the source code along with the testbench code into the iverilog simulator

* iverilog good_mux.v tb_good_mux.v

* We can see that an output file a.out has been created.

* ./a.out

* The output of the iverilog, a vcd file, is created which is loaded into the simualtor gtkwave.

* gtkwave tb_good_mux.vcd
  
![2fac1505-0348-4915-8a46-f846fedcac2e](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/d5446913-3358-416d-9202-6d004689074a)
<img width="497" alt="263481758-e7627aaf-6048-445a-aaae-1117212d9670" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/7437ce56-2e23-49d0-bb4c-a113e0896c04">

## iVerilog GTKwave Part-2
* In order to view the contents in the files,

* gvim tb_good_mux.v -o good_mux.v
  
  <img width="367" alt="263726055-ef3c8e61-2e45-4087-9584-f84fd3584cd3" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/fe448d11-f0b4-466d-9f6f-6c25bd87bc43">

# Introduction to Yosys and Logic Synthesis
## Introduction to Yosys
* Synthesizer
   * It is a tool used for converting RTL design code to netlist.
   * Here, the synthesizer used is Yosys.

* Yosys
    * It is an open-source framework for Verilog RTL synthesis and formal verification.
    * Yosys provides a collection of tools and algorithms that enable designers to transform high-level RTL (Register Transfer Level) descriptions of digital circuits into optimized gate-level representations suitable for physical implementation on hardware.

      <img width="561" alt="263507834-5f879aaa-ec65-4362-9f91-f39999069732" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/55e6d592-ec83-4de0-bda5-472861ace63f">

* Design and .lib files are fed to the synthesizer to get a netlist file.
* Netlist is the representation of the design in the form of standard cells in the .lib
* Commands used to perform different opertions:
   * read_verilog to read the design
   * read_liberty to read the .lib file
   * write_verilog to write out the netlist file

*   To verify the synthesis
    
<img width="566" alt="263507983-fd73f6b8-f594-4e4f-bb1a-b600fb4475f8" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/acc5668c-a3f6-4469-89b2-6cf9f30e8a69">

* Netlist along with the tesbench is fed to the iverilog simulator.
* The vcd file generated is fed to the gtkwave simulator.
* The output on the simulator must be same as the output observed during RTL simulation.
* Same RTL testbench can be used as the primary inputs and primary outputs remain same between the RTL design and synthesised netlist.

## Introduction to Logic Synthesis
* Logic Synthesis
  * Logic synthesis is a process in digital design that transforms a high-level hardware description of a digital circuit, typically in a hardware description language (HDL) like Verilog or VHDL, into a lower-level representation composed of logic gates and flip-flops.
  * The goal of logic synthesis is to optimize the design for various criteria such as performance, area, power consumption, and timing.

* .lib
  * It is a collection of logical modules like And, Or, Not etc.
  * It has different flavors of same gate like 2 input AND gate, 3 input AND gate etc with different performace speed.

* Why different flavors of gate?
   * In order to make a circuit faster, the clock frequency should be high.
   * For that, the time period of the clock should be as low as possible.

<img width="269" alt="263508891-bc2242db-49e8-4c19-a06e-8f8e82f55729" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/9dce3ead-1391-44a5-bd1c-a1e77ff794c8">

* In a sequential circuit, clock period depends on:
   * Clock to Q of flip-flop A.
   * Propagation delay of combinational circuit.
   * Setup time of flip-flop B.

<img width="142" alt="263509150-112de4cd-6e0c-46ec-ad94-0cb6540af7e1" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/b4b666b1-51b7-47fc-b43b-e7c5aed7e601">

* Why need fast and slow cells?
   * To ensure that there are no HOLD issues at flip-flop B, we require slow cells.
   * For a smaller propagation time, we need faster cells.
   * The collection forms the .lib

* Faster Cells vs Slower Cells
   * Load in digital circuit is of Capacitence.
   * Faster the charging or dicharging of capacitance, lesser is the cell delay.
   * However, for a quick charge/ discharge of capacitor, we need transistors capable of sourcing more current i.e, we need wide transistors.
   * Wider transistors have lesser delay but consume more area and power.
   * Narrow transistors have more delay but consume less area and performance.
   * Faster cells come with a cost of area and power.

* Selection of the Cells
   * We have to guide the Synthesizer to choose the flavour of cells that is optimum for implementation of logic circuit.
   * More use of faster cells leads to bad circuit in terms of power and area and also hold time violations.
   * More use of slower cells leads to sluggish circuits amd may not meet the performance needs.
   * Hence the guidance is offered to the synthesiser in the form of constraints.

  # Labs using Yosys and Sky130 PDKs
  ## Yosys good_mux
  * To invoke yosys
     * cd
     * cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
     * Type yosys
    
![1c4373c0-898e-4f4a-9f82-5e78d12a183c](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/793508a1-8c72-4f30-965e-68978648c85a)

*   To read the library

 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

* To read the design

read_verilog good_mux.v

* To syntheis the module

 synth -top good_mux
 
![45bc27ee-bf82-4332-8457-d536104e718a](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/7af092ce-be7b-4cf4-b383-a59307475640)

 ![3ad010f9-ae2a-45c5-b6cd-b7f8175a82f5](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/126f06b7-e116-46e4-8d1a-2d8605d1c894)

* To generate the netlist

abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

![05d9f248-2b79-4668-8971-930a9cd06e6e](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/a770da67-0499-4174-b07a-8b7da0b43fcd)

It gives a report of what cells are used and the number of input and output signals.

* To see the logic realised

show

![23f7db1a-ff37-41bc-aa65-8a23e257ebb4](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/14565e1e-334a-4af5-ab25-f502330ef1b9)

The mux is completely realised in the form of sky130 library cells.

* To write the netlist

  * write_verilog good_mux_netlist.v

  * !gvim good_mux_netlist.v

  * To view a simplified code

  * write_verilog -noattr good_mux_netlist.v

  * !gvim good_mux_netlist.v
    
 <img width="224" alt="263511429-74fc2a01-3c35-4db1-8220-96595c6c236e" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/0d0012e2-bb51-43a6-b72a-8a17280f4c86">

  ![437ec67e-1b6d-4465-979c-f445cd5bdf5b](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/7dfcdadb-dd9f-49b2-be51-130e1b311459)

# Introduction to Timing Dot Libs

## Introduction to Dot Lib
* To view the contents in the .lib

gvim ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

<img width="443" alt="263514623-91edd5d4-bb82-48ec-b0bd-ca233d8a8063" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/cb973116-e2a1-475e-b208-642a61646e8f">

* The first line in the file library ("sky130_fd_sc_hd__tt_025C_1v80")  :

  * tt : indicates variations due to process and here it indicates Typical Process.
  * 025C : indicates the variations due to temperatures where the silicon will be used.
  * 1v80 : indicates the variations due to the voltage levels where the silicon will be incorporated.

* It also displays the units of various parameters.
<img width="284" alt="263515297-d01d750e-fc1c-4de0-8e72-e6842c14f90b" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/7efec7d3-bc11-4a8b-b57a-9983588974a6">

  <img width="229" alt="263515621-39f26ac7-7302-4dc7-a517-6a5a031e2cae" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/43cad51f-0c81-4025-af09-d79ffb5069ad">

* It gives the features of the cells

* To enable line number :se nu

* To view all the cells :g//

* To view any instance :/instance

* Since there are 5 inputs, for all the 32 possible combinations, it gives the delay, power and all the other parameters for each cell.

* The below image shows the power consumption and area comparision.

<img width="911" alt="263518651-2a6b20a3-33d1-47e0-814f-6cff100ec2a7" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/c45f2e63-ce6a-438a-8b77-cddce54e59c9">

# Hierarchical vs Flat Synthesis
## Hierarchical Synthesis Flat Synthesis
Hierarchical Synthesis Hierarchical synthesis is an approach in digital design and logic synthesis where complex designs are broken down into smaller, more manageable modules or sub-circuits, and each module is synthesized individually. These synthesized modules are then integrated back into the overall design hierarchy. This approach helps manage the complexity of large designs and allows designers to work on different parts of the design independently.

* The file we used in this lab is multiple_modules.v

  * cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
  *  gvim multiple_modules.v
    
    ![b5ed1033-7736-4020-a2d4-4f3181c2c291](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/de43880d-7445-4f7b-b80f-815939279571)

* multiple_modules instantiates sub_module1 and sub_module2

* Launch yosys

* read the library file read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

* read the verilog file  read_verilog multiple_modules.v

* synth -top multiple_modules to set it as top module
  
  ![ca59a918-2af8-4cb4-8334-0ff321582c83](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/dbed2887-5357-4770-9352-a1245f8483de)
![a83418ae-c4b0-4e2c-ac6a-1f3ea341f1f6](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/0e3c5b85-a236-4fb5-8671-77b224080890)

* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

* To view the netlist show multiple_modules

![bcbec4fc-327e-4e2f-a8d4-7974ddd0b5e7](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/6fa494b2-0955-43e5-b2f8-899fb3038590)

* Here it shows sub_module1 and sub_module2 instead of AND gate and OR gate.
* write_verilog -noattr multiple_modules_hier.v
* !gvim multiple_modules_hier.v
  ![3f7ef3bf-7a28-4513-9ce3-c76d6e73e7da](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/21544438-17e1-46f1-8a8c-4e3d82835845)
![69161862-f9c1-4376-9e2f-933b17f6e823](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/081ee167-5b52-4502-967a-e998ea9fb9a3)

Flattened Synthesis Flattened synthesis is the opposite of hierarchical synthesis. Instead of maintaining the hierarchical structure of the design during synthesis, flattened synthesis combines all modules and sub-modules into a single, flat representation. This means that the entire design is synthesized as a single unit, without preserving the modular organization present in the original high-level description.
* Launch yosys
* read the library file read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read the verilog file  read_verilog multiple_modules.v
* synth -top multiple_modules to set it as top module
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* flatten to write out a flattened netlist
* show
  <img width="924" alt="263521846-bd069e1f-4da5-473a-b041-562cbef042f0" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/a05f9038-b45b-4f36-9ae7-df60b43238a3">

write_verilog -noattr multiple_modules_flat.v
!gvim multiple_modules_flat.v

![9c1ca36a-f8b9-4764-bc4b-35a3a403651d](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/80e7e6c3-4055-4cf5-95a2-4d300b3beef4)

![6fec196f-b176-4595-9405-2c3871f99c92](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/cfcec9ea-2fe1-4343-8f1f-a95d41a750d0)


# Various Flop Coding Styles and Optimization
## Why Flops and Flop Coding Styles
### D Flip-Flop with Asynchronous Reset
* When the reset is high, the output of the flip-flop is forced to 0, irrespective of the clock signal.
* Else, on the positive edge of the clock, the stored value is updated at the output.
gvim dff_asyncres_syncres.v

![40012d2b-93a2-415a-b330-46ccf94c0f8d](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/a997d5e0-5299-48d9-b2e8-76fd6e3081e9)
### D Flip_Flop with Asynchronous Set
* When the set is high, the output of the flip-flop is forced to 1, irrespective of the clock signal.
* Else, on positive edge of the clock, the stored value is updated at the output.
  gvim dff_async_set.v

  ![fd2d43eb-294b-4455-b922-818dcaa6893f](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/8161118b-d719-465f-a6ef-1d92e82cbfa2)

### D Flip-Flop with Synchronous Reset
* When the reset is high on the positive edge of the clock, the output of the flip-flop is forced to 0.
* Else, on the positive edge of the clock, the stored value is updated at the output.
  gvim dff_syncres.v

  ![abf0aaf5-c8f5-44a7-b2d9-1e28c98867b1](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/dd371ce7-1c57-46c1-b354-7a0a4158b8a2)

### D Flip-Flop with Asynchronous Reset and Synchronous Reset
* When the asynchronous resest is high, the output is forced to 0.
* When the synchronous reset is high at the positive edge of the clock, the output is forced to 0.
* Else, on the positive edge of the clock, the stored value is updated at the output.
* Here, it is a combination of both synchronous and asynchronous reset DFF.

gvim dff_asyncres_syncres.v

<img width="439" alt="263527791-8ee2f2a5-31e9-447c-a23f-b347fc7b642c" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/3a398d52-6767-4088-bcf8-eb02c61770ad">

## Lab Flop Synthesis Simulations
### D Flip-Flop with Asynchronous Reset
#### Simulation
* cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
* iverilog dff_asyncres.v tb_dff_asyncres.v
* ./a.out
* gtkwave tb_dff_asyncres.vcd

  ![59bdebb7-4d93-46bb-8f7e-9e98184a33fe](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/0e558325-5967-45e4-a1fe-760690ba0cf8)

![2d51cd09-bcbe-4f51-88fe-bddf3c4767e0](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/ac06519a-7673-451a-a1ac-0f35159c8407)

#### Synthesis
* cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

* yosys

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

* read_verilog dff_asyncres.v

* synth -top dff_asyncres

* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

* show
  ![c64213ea-63b8-46a3-a5c3-76133522e9f0](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/cc917d4a-4d20-414d-9f47-3ce0ea653945)

### D Flip_Flop with Asynchronous Set
#### Simulation 
* cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
* iverilog dff_async_set.v tb_dff_async_set.v
* ./a.out
* gtkwave tb_dff_async_set.vcd
  ![576fadc1-fc5e-47e9-b272-72af17615f52](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/cdf21d95-d417-4f44-a3b5-3583211f7925)

![ecda1a4e-26ba-433e-9085-d64a0e465a2f](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/9ad0064a-4855-4f17-8027-80b8bb126ee5)

#### Synthesis
cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show

![239dfdae-71a0-45ac-8867-85ae4bf805e8](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/46098658-352c-4d80-9799-070604e62478)


### D Flip-Flop with Synchronous Reset
#### Simulation
cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
gtkwave tb_dff_syncres.vcd
![576fadc1-fc5e-47e9-b272-72af17615f52](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/98f7cff5-984b-44de-84cd-abbd92758dfc)
![21f0f0cf-4810-48b7-b097-df20434362d0](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/6724d0e8-22f9-4d8c-b163-3edf396f6e95)


#### Synthesis
* cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
* yosys
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_syncres.v
* synth -top dff_syncres
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

<img width="925" alt="263532077-ff5b11e7-11a8-40c9-9e08-e090eeb0f547" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/622d1d89-b0c9-497d-af9b-c8e678434ab4">

### Interesting Optimisations
gvim mult_2.v
![95bfdb80-0d56-47fa-a050-b2f52ecece6e]
(https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/d350e949-4612-4fff-baa2-e0dd49be8397)

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mult_2.v
synth -top mul2

![e1dd1c29-d78d-497d-8b1f-dfb273ab5472](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/7f0ac279-bb5f-4718-92ee-86656f2a16a4)

abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show

![ccd01ca1-4a86-4d9d-9c58-ee6543f1e16e](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/e1a71952-55c0-4870-9018-1239f4005357)

write_verilog -noattr mul2_netlist.v
!gvim mul2_netlist.v

![d6eba8cd-01d0-41ce-b3a3-68b89c82fbf5](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/fa07cee6-260c-44f8-9667-3f0b93731ba3)

* gvim mult_8.v
  
![e143b7e2-867b-433f-ba6e-1472727910fd](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/9b85f794-70c5-490f-893c-6fc61daee7b1)

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  

read_verilog mult_8.v

synth -top mult8

![60dc3bdb-a6a7-4530-8c0a-51b97837a250](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/a233f77a-0167-4f32-9883-0f77d9b27d78)

abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show

![d40a1e66-7f9a-4e79-b2da-f11b65efb6a3](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/9ca28175-d0ec-4c83-a5cd-c4477f2b7bea)

write_verilog -noattr mult8_netlist.v
!gvim mult8_netlist.v

![84375996-b70b-4572-8017-9a4c8daab8ad](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/9174fd8f-d841-45e6-b96d-dad678f0c9fd)

# Introduction to Optimisations
## Combinational Optimisation
* Combinational logic refers to logic circuits where the outputs depend only on the current inputs and not on any previous states.
* Combinational optimization is a field of study in computer science and operations research that focuses on finding the best possible solution from a finite set of options for problems that involve discrete variables and have no inherent notion of time.
* Optimising the combinational logic circuit is squeezing the logic to get the most optimized digital design so that the circuit finally is area and power efficient.
Techniques for Optimisations:
   * Constant propagation is an optimization technique used in compiler design and digital circuit synthesis to improve the efficiency of code and circuit implementations by replacing variables or expressions with their constant values where applicable.
   * Boolean logic optimization, also known as logic minimization or Boolean function simplification, is a process in digital design that aims to simplify Boolean expressions or logic circuits by reducing the number of terms, literals, and gates required to implement a given logical function.

## Sequential Logic Optimisations
* Sequential logic optimizations involve improving the efficiency, performance, and resource utilization of digital circuits that include memory elements like flip-flops and latches.
* Optimizing sequential logic is crucial in ensuring that digital circuits meet timing requirements, consume minimal power, and occupy the least possible area while maintaining correct functionality.
* Optimisation methods:
  * Sequential constant propagation, also known as constant propagation across sequential elements, is an optimization technique used in digital design to identify and propagate constant values through sequential logic elements like flip-flops and registers. This technique aims to replace variable values with their known constant values at various stages of the logic circuit, optimizing the design for better performance and resource utilization.
  * State optimization, also known as state minimization or state reduction, is an optimization technique used in digital design to reduce the number of states in finite state machines (FSMs) while preserving the original functionality.
  * Sequential logic cloning, also known as retiming-based cloning or register cloning, is a technique used in digital design to improve the performance of a circuit by duplicating or cloning existing registers (flip-flops) and introducing additional pipeline stages. This technique aims to balance the critical paths within a circuit and reduce its overall clock period, leading to improved timing performance and better overall efficiency.
  * Retiming is an optimization technique used in digital design to improve the performance of a circuit by repositioning registers (flip-flops) along its paths to balance the timing and reduce the critical path delay. The primary goal of retiming is to achieve a shorter clock period without changing the functionality of the circuit.

    # Combinational Logic Optimisations
    ## opt_check
    * gvim opt_check.v
    * 
    ![cab459e9-e7eb-40fd-a1ea-6c642f96c2d7](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/c3c173a8-eb70-4b21-9927-32dfbb72d534)

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

* read_verilog opt_check.v

* synth -top opt_check

* opt_clean -purge

* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

* show
  
![23cffd72-0669-44d7-8363-e4dc15f68ee1](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/c91e07ac-a8a3-4aa9-8a2d-4904d9f3a788)
![5161d771-b8ca-455c-96dd-a2ae621dda29](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/e7cef776-06e1-49ea-94f3-13707c0807a9)

## opt_check2
* gvim opt_check2.v
  ![5e7ced59-e5b4-4383-a10e-c8968b7a81f2](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/8ce28299-6493-49bf-b3cf-b48b72128475)
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

* read_verilog opt_check2.v

* synth -top opt_check2

* opt_clean -purge

* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

* show
 ![9d5e779f-ca51-4af0-95b8-5c18dc3f35dc](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/69ddb1ef-53a2-4736-b883-34b200de36e2)

 ![ed8455b4-5fea-49f8-a532-0d29638fffc5](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/d4b472f9-8713-4e27-a502-df2350ef0a90)

## opt_check3
* gvim opt_check3.v
* ![1927cd49-68f8-4f81-9617-38e119841eb8](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/058f471f-6e68-4762-9d30-e91f321b9143)
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog opt_check3.v
* synth -top opt_check3
* opt_clean -purge
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show
  ![a55e5f3e-ec48-4b34-a8e9-a7446c89beae](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/903556f7-556c-425e-87aa-596fe5231f63)

![38a1f2a0-a7b4-4bf7-a3cd-66d47f0176a3](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/ace92b83-9ab7-4485-86ca-3ce4ca60f3dc)

## opt_check4
* gvim opt_check4.v
* ![ffe71554-8d6f-47aa-ac99-1d58fcd6e93c](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/250ef33c-78db-4726-ae64-6fa2b0f5299b)

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog opt_check4.v
* synth -top opt_check4
* opt_clean -purge
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show
* ![87e1281b-5c25-40c1-882a-d35b20db9ccf](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/37220ee0-21ba-4c1c-85e4-9a15a5ec3689)
![92635bd4-a454-41a9-a316-a6dfad75ecd2](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/d864f493-4b62-42cc-bce8-1c3ba37c6655)

## multiple_module_opt
* gvim multiple_module_opt.v
* ![a7e8a067-cea7-474d-bca3-0f99c4a49782](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/a1cb3353-2c1e-47c5-ad30-20b65fc6f97c)
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog multiple_module_opt.v
* synth -top multiple_module_opt
* opt_clean -purge
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show
* ![cdf38699-9ee2-4560-905d-12edf312c7f2](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/00d86c50-d1a4-4bef-8001-d8363a142ce7)
<img width="301" alt="263543923-1344d22d-51f5-439e-bc34-96b2a742474e" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/afd2efa8-5d48-4c2a-a63a-ebead25fd25a">

# Sequential Logic Optimisations
## dff_const1
* gvim dff_const1.v
* ![b2f0c5e2-167a-40c7-8a94-9ecbeb113842](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/f6c859ff-c569-4f82-aebe-bb9dd0eec8c0)
### Simulation 
* iverilog dff_const1.v tb_dff_const1.v
* ./a.out
* gtkwave tb_dff_const1.vcd
  ![3d07ced2-4e37-4944-a787-eae81daab66b](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/cbcc3957-d6c6-4373-a6dd-80a56ecc4b19)

### Synthesis
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_const1.v
* synth -top dff_const1
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show
* ![1525412d-cf61-4b0e-bd31-953d9580aeae](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/ae4925b2-6a90-4d7c-b06e-1431189663e6)
![f6c9b553-1bed-4ab8-bdea-1146f5ed12d1](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/1f5065fa-a57f-4ee3-be1c-d5bfd8a6505b)

## dff_const2
* gvim dff_const2.v
* ![82b316fa-03a3-41fe-a915-0c0bf507a206](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/94afc941-b3bd-4912-b45c-8455cc2d5dfe)
### Simulation 
* iverilog dff_const2.v tb_dff_const2.v
* ./a.out
* gtkwave tb_dff_const2.vcd
* ![c1cb8106-1222-4c8a-b2ae-04c3c1de1965](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/d1490bf9-e7a4-4f36-a425-364348b1951d)
### Synthesis
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_const2.v
* synth -top dff_const2
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show
* ![03f7196f-608c-46c7-812f-0a0bee22919e](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/0b8033d4-ccf4-494a-b353-2e5da68ea295)
![b7584a1c-2012-459c-b2bb-16d784278163](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/1f7edc3a-1e3f-470f-b1e6-5a616a736553)

## dff_const3
* gvim dff_const3.v
* ![550626e9-5382-4919-9a83-c7fa58079ef0](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/61ac8ff0-ca80-4860-8b57-06edbc5f6835)
  ### Simulation
  * iverilog dff_const3.v tb_dff_const3.v
* ./a.out
* gtkwave tb_dff_const3.vcd
* ![425db6ff-57dc-47c7-b973-4c6c3cc26b9c](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/79ac6b4e-a1a2-4509-aa62-eda64dde063c)
### Synthesis
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_const3.v
* synth -top dff_const3
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show
* ![c3b2358c-2422-425b-ae70-74c3fb0b7bd3](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/6a3da587-5895-4527-91c1-41babc305653)
![669de15b-501b-4537-98d4-65f2267dcb73](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/cae84712-7c52-4695-9081-866a8653b8ec)

## dff_const4
* gvim dff_const4.v
* ![c495e8ed-3bb6-4421-a7bb-d45a4bf32450](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/adf7f2fa-9c47-444c-b2e9-4b741da5db7e)

### Simulation 
* iverilog dff_const4.v tb_dff_const4.v
* ./a.out
* gtkwave tb_dff_const4.vcd
* ![805fd18d-e805-46b6-8f5d-0f15a1f6bc35](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/99f8abb1-855d-448e-9da3-a9b2e7d907b9)

### Synthesis
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_const4.v
* synth -top dff_const4
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show
* ![ec49c474-2dcf-4cf5-b78e-4fee578bce17](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/1b2cb29d-14bc-41ea-9f6f-cdeb1c32daef)
![095b675c-0453-4898-87dd-225f67795eae](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/e96f6fa4-1f86-4541-9e02-fda89d8b6a94)

# Sequential Optimisations for Unused Outputs
## counter_opt
* gvim counter
* ![250e225d-60d7-45b5-82e0-b593ca93512f](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/d093a87c-6b71-45e9-abfe-1db1681eec0a)
_opt.v
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog counter_opt.v
* synth -top counter_opt
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show
![3f1d0e7d-92ba-454b-a86b-7d4acebdfafd](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/73cb89f8-d2ad-4bb5-bab9-e40a65b2ee7f)
![7af22a9d-de83-46fe-a6f0-4cf54e23099c](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/8c97d0b9-36c6-43e8-a0eb-27837873a126)

## counter_opt2
* gvim counter_opt2.v
* ![841542c3-3e8d-41df-a149-d26efa5f5bf7](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/6e3e86db-16d4-4dfc-acc7-ce172ff14b72)
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog counter_opt2.v
* synth -top counter_opt2
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show
* ![3f1d0e7d-92ba-454b-a86b-7d4acebdfafd](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/bd5332cf-3120-49db-a669-ce95abe40fe4)
![d5e05216-fca8-4d45-8448-268650419428](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/87b23de1-4386-48f0-a3c5-1db754aef4fd)

# GLS Synthesis-Simulation Mismatch and Blocking Non-blocking Statements
## GLS Concepts And Flow Using Iverilog
* Gate Level Simualtion
   * Gate-level simulation is a technique used in digital design and verification to validate the functionality of a digital circuit at the gate-level implementation.
  * It involves simulating the circuit using the actual logic gates and flip-flops that make up the design, as opposed to higher-level abstractions like RTL (Register Transfer Level) descriptions.
  * This type of simulation is typically performed after the logic synthesis process, where a high-level description of the design is transformed into a netlist of gates and flip-flops.
  * We perform this to verify logical correctness of the design after synthesizing it. Also ensuring the timing of the design is met.
    <img width="608" alt="263759047-6298b067-2f45-4dbc-ad25-762ac3d8be63" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/90cab3cc-aee7-4359-a98a-8964435f11d5">
* Synthesis-Simulation Mismatch
   * A synthesis-simulation mismatch refers to a situation in digital design where the behavior of a circuit, as observed during simulation, doesn't match the expected or desired behavior of the circuit after it has been synthesized.
   * This discrepancy can occur due to various reasons, such as timing issues, optimization conflicts, and differences in modeling between the simulation and synthesis tools.
  * This mismatch is a critical concern in digital design because it indicates that the actual hardware implementation might not perform as expected, potentially leading to functional or timing failures in the fabricated chip.
  ## Blocking Statements
  * Blocking statements are executed sequentially in the order they appear in the code and have an immediate effect on signal assignments.
  * Example:
     module BlockingExample(input A, input B, input C, output Y, output Z);
  wire temp;

  // Blocking assignment
  assign temp = A & B;

  always @(posedge C) begin
      // Blocking assignment
      Y = temp;
      Z = ~temp;
  end
 endmodule

* Non-Blocking Statements
   * Non-blocking assignments are used to model concurrent signal updates, where all assignments are evaluated simultaneously and then scheduled to be updated at the end of the time step.
  * Example:
    module NonBlockingExample(input clock, input D, input reset, output reg Q);

 always @(posedge clock or posedge reset) begin
     if (reset)
         Q <= 0;  // Reset the flip-flop
     else
         Q <= D;  // Non-blocking assignment to update Q with D on clock edge
 end
endmodule
* Caveats with Blocking Statements
   * Blocking statements in hardware description languages like Verilog have their uses, but there are certain caveats and considerations to be aware of when working with them. Here are some important caveats associated with using blocking statements:
Procedural Execution: Blocking statements are executed sequentially in the order they appear within a procedural block (such as an always block). This can lead to unexpected behavior if the order of execution matters and is not well understood.
  * Lack of Parallelism: Blocking statements do not accurately represent the parallel nature of hardware. In hardware, multiple signals can update concurrently, but blocking statements model sequential behavior. As a result, using blocking statements for modeling complex concurrent logic can lead to incorrect simulations.
  * Race Conditions: When multiple blocking assignments operate on the same signal within the same procedural block, a race condition can occur. The outcome of such assignments depends on their order of execution, which might lead to inconsistent or unpredictable behavior.
  * Limited Representation of Hardware: Hardware systems are inherently concurrent and parallel, but blocking statements do not capture this aspect effectively. Using blocking assignments to model complex combinational or sequential logic can lead to models that are difficult to understand, maintain, and debug.
  * Combinatorial Loops: Incorrect use of blocking statements can lead to unintentional combinational logic loops, which can result in simulation or synthesis errors.
Debugging Challenges: Debugging code with many blocking assignments can be challenging, especially when trying to track down timing-related issues.
  * Not Suitable for Flip-Flops: Blocking assignments are not suitable for modeling flip-flop behavior. Non-blocking assignments (<=) are generally preferred for modeling flip-flop updates to ensure accurate representation of concurrent behavior.
  * Sequential Logic Misrepresentation: Using blocking assignments to model sequential logic might not capture the intended behavior accurately. Sequential elements like registers and flip-flops are better represented using non-blocking assignments.
  * Synthesis Implications: The behavior of blocking assignments might not translate well during synthesis, leading to potential mismatches between simulation and synthesis results.

 # Labs on GLS and Synthesis-Simulation Mismatch
  ## ternary_operator_mux
    * gvim teranry_operator_mux.v
    <img width="370" alt="263764297-8539ab94-8f5a-4bff-8465-eb8bb6ca83b8" src="https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/39673c7e-9344-4557-afbf-9d224466f75e">

### Simulation
* iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
* ./a.out
* gtkwave tb_ternary_operator_mux.vcd
* ![c8c9bd44-7d5c-4b10-b8bc-5844ca7b00c0](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/b4cc1a83-2152-4026-93cb-9d701c386e4e)
### synthesis
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog ternary_operator_mux.v
* synth -top ternary_operator_mux
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show
* ![1ca47dd0-1336-46be-a890-78e6214e64b2](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/68765e4b-5711-4997-aa7d-5586ace0a770)
![62917943-6e8d-444a-909c-c613dcb1526a](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/a6161550-c8ee-4ed4-9698-8e870dbb5c34)

## GLS to Gate-Level Simulation
* iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_bad_mux.vcd
![c8c9bd44-7d5c-4b10-b8bc-5844ca7b00c0](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/523c2017-3136-4e1e-a786-32a27ab291ee)

### bad_mux
* gvim bad_mux.v
* ![e7fe700f-1b39-4837-b5a2-e311f28c3929](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/f6641b98-97ac-4b5c-84e3-9712f10404d5)
  #### Simulation
* iverilog bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
![73ce45f4-6b97-45e5-9b07-0c1c89b0660b](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/3268dde1-6097-469f-91da-f40fa2b25597)
#### Synthesis
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

read_verilog bad_mux.v

synth -top bad_mux

abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

show
![0756b53e-07c9-4c5c-977e-bcb1c149f4fa](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/4777d770-2713-4ea6-8ab0-3466687969f8)
![a01f00ce-3e60-4b0c-8ebf-cd477cc4f14b](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/240ca440-3919-468b-a374-4f72b225b0d9)

### GLS to Gate-Level Simulation
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
![73ce45f4-6b97-45e5-9b07-0c1c89b0660b](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/3b30f361-cd91-42da-9439-b1cf285b71c0)

# Labs on Synth-Sim Mismatch for Blocking Statement
## blocking_caveat
* gvim blocking_caveat.v
* ![1acb54fb-113a-46e4-9e0e-6bb9f470313a](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/4bcf2529-b792-44f1-bfa3-005b0302d18f)
## Simulation
* iverilog blocking_caveat.v tb_blocking_caveat.v
  
./a.out

gtkwave tb_blocking_caveat.vcd
![134a6fc1-741c-4902-859e-6f804d68ef33](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/1efc499e-271e-4260-a1f9-42c65fd8edd2)
## Synthesis
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog blocking_caveat.v
* synth -top blocking_caveat
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show
* ![4a440cef-aaed-4c84-b6ff-0b466318ac3a](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/dc849ec2-0820-4ecb-86d8-0a25cced8a18)
  ![a439e7e6-e323-4a96-92a1-5e7879dd7b91](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/859c2657-7ded-4c67-a8ff-e8d284dff94a)

## GLS to Gate-Level Simulation
* iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
* ./a.out
* gtkwave tb_blocking_caveat.vcd
* ![4e198f69-baea-4d04-80d9-a3eac231a3dd](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/5bffba66-2b95-467e-8c4b-9838b78d44b5)
![197b3e49-0445-4198-a6a7-2df7e0f3c416](https://github.com/apoorvaaaa5/physical_design_asic/assets/117642634/94c6a781-bb3b-4d3d-a6fc-048b101bc00c)
