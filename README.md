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
