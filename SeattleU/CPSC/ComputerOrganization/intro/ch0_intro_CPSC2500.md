
### Computers and Programs

**What is a Computer?**
- Hard to define
- Interesting to think about

**Computer Components**
- A *processor* to interpret and execute programs.
- a *memory* to store both data and programs
- An *input/output* mechanism for transferring data to and from the outside world.

**What is a Program?**
From the computer system point-of-view, a *program* is a list of ordered machine instructions.

**Generations of Programming Languages**
1) *1st Generation*: Machine Language
	- Purely binary
	- hard for humans to understand
2) *2nd Generation*: Assembly Language
	- human-readable form of machine language
	- easy translation to machine language
	- very machine dependent
3) *3rd Generation*: High level Languages
	- common programing constructs are provided
	- machine independent (for the most part)
	- strict syntax and rules
	- compilers convert to assembly

### Computer Level Hierarchy

**Basics:**
- A *hierarchical design* divides a computer system into manageable layers.
- Each layer can be implemented without intimate knowledge of the other layers.
- Each layer is an *abstraction* of the level below it.
- Each layer executes their own particular instructions, calling upon lower layers to perform tasks as required.
- Computer circuits ultimately carry out all the work.

![[Pasted image 20250926181423.png]]

*Level 5:* Problem-oriented language level
- Programs like C++, Python, Java
*Level 5 to Level 4:* Assembly language level
- Compiler converts source code into assembly code
- Even "interpreted" languages are compiled into assembly code
*Level 4:* Assembly language level
- Assembly language is a human readable form of machine language.
	- Difficult (time-consuming, error-prone) to program.
	- Most assembly language is produced by a compiler
*Level 4 to Level 3:* Operating system machine level
- An assembler will convert the assembly language code into machine language.
*Level 3:* Operating system machine level
- OS controls executing processes, manages, memory, and protects I/O devices.
*Level 3 to Level 2:* Instruction set architecture level
- Inserts necessary system library code
- Most assembly language instructions pass through level 3 w/o modification
*Level 2:* Instruction set architecture level
- consists of machine instructions that are particular to the architecture of the machine.
- Serves as the input to the microprocessor.
*Level 2 to Level 1:* Microarchitectural level
- Each instruction is translated into set of control signals that directs each component in the processor.
- Control can also be implemented using a microprogram using a language internal to the processor.
*Level 1:* Microarchitectural level
- Consists of the various components inside a CPU:
	- Memory (called registers)
	- Arithmetic-logic unit (ALU)
	- Datapath: wires that connect to the various components
*Level 1 to Level 0:* Digital logic level
- These CPU components are made of basic hardware components called gates.
*Level 0:* Digital logic level
- Consists of basic digital logic components such as AND, OR, and NOT gates.
*Level 0 to Level -1 and below?*
- These gates are actually made of transistors.
- Transistors are constructed using semiconductors such as silicon
- Both of these topics are out-of-scope for this course (more computer engineering shiznit)

### Equivalence of Hardware and Software
- Anything that can be done with software can also be done with hardware.
	- Any operation can be built directly into hardware.
- Anything that can be done with hardware can be done with software.
	- Any instruction executed by hardware can be simulated in software
- Need to consider speed and cost tradeoffs.
	- Hardware is almost always faster and more expensive

### Course Overview

![[Pasted image 20250926183946.png]]
### Syllabus

![[Syllabus.pdf#invert_B]]

