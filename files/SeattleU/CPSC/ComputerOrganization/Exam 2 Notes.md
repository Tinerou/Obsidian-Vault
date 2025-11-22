#ComputerOrganization 
### Unit 4: Assembly Language Part II  
#### Heap memory  
```Assembly
# code section
# Now you can allocate to heap using &heapPtr!

# heap section
heapPtr: .fill &heap # points to start of heap
heap: .fill 0
```
#### Compilation process  
- [x] compiler, assembler, linker
- **Compiler:** Coding language → assembly code
	- *frontend:*
		- Parses high level language
		- Checks for syntax errors
	- *back-end*
		- Optimizes code
		- Allocates registers
		- Produces assembly code
	- [[4.1 - Heap Memory and Compilation Process#Compiler|Compiler]]
- **Assembler:** Assembly code → object code
	- There is more to this that may be necessary!!!
	- [[4.1 - Heap Memory and Compilation Process#Assembler|Assembler]]
- **Linker:** Stitches object files into a single executable file
	- [[4.1 - Heap Memory and Compilation Process#**Linking Example**|Example]]
	- [[4.1 - Heap Memory and Compilation Process#Linker|Linker]]

- [x] object file format: symbol table, external reference list, relocation records
- **Symbol Table:** A table of `<label, address>` pairs that are visible to other object files.
	- Only "global" labels are in the symbol table
	- Each global name must be unique
	- Example: If object file $A$ has defined function `foo`, an entry to `foo` with its starting address appears in the symbol table.
	- [[4.1 - Heap Memory and Compilation Process#Symbol Table|Symbol Table]]
- **External Reference List:** A list of labels used in this file but are not defined and expected to be defined in another file.
	- Contains list of *functions* called, and *global variables* used, that are not defined in the current file.
	- [[4.1 - Heap Memory and Compilation Process#External Reference List|External Reference List]]
- **Relocation Records:** Contains a list of instructions or data entries that use a label that refers to direct address.
	- Relocation records are *NOT* created for PC-relative targets in branches.
	- Applies to instruction like this: `lli r4 &foo`
	- Does *not* apply to labeled instructions: `foo: sw r6 r7 0`
	- [[4.1 - Heap Memory and Compilation Process#Relocation Records|Relocation Records]]
#### Function calls  & Stack Memory
**Activation Record:**
1) State parameters and variables (when not main `0` is reserved for `previous frame ptr`)
2) create new frame and stack pointer
3) Store return value in `r4`
4) Set to previous stack and frame pointer then jump back to `r5`

**Actual function call:**
1) `lw` necessary variable(s) from main and `sw` to function stack
2) jump to function
3) store return  value `r4`  back to main stack if necessary

### Unit 5: Microarchitecture  
#### Single cycle datapath and control ROM  
- [x] Single cycle datapath and control ROM
- [[5.1 & 5.2 - Single-Cycle Datapath]]
#### Performance  
- [x] **CPU time equation**
	- $$CPU \space Time = \frac{seconds}{program} = \frac{instructions}{program}* \frac{avg \space cycles}{instruction}* \frac{seconds}{cycle}$$

		$\frac{instructions}{program}$ ← "dynamic" instruction count
		
		$\frac{avg \space cycles}{instruction}$ ← Cycles per instruction (CPI)
		
		$\frac{seconds}{cycle}$ ← Inverse of frequency

- [x] **single cycle vs. multiple cycle vs. pipelining performance**
	- Slowest → Fastest:
		- single cycle → multiple cycle → pipelining
			- In general this is true…
#### Pipelining
- [x] **pipeline stages**
	- [[5.3 & 5.4 CPU Performance and Pipelining#5 Stages of ANNA Pipeline|5 Stages of ANNA Pipeline]]
- [x] **data hazards:** A hazard due to an instruction dependent on data produced by an instruction that is later in the pipeline.
	- [[5.3 & 5.4 CPU Performance and Pipelining#Data Hazards|Data Hazards]]
- [x] **control hazards:** Occurs anytime a branch or jump instruction is executed
- [x] **time graphs:**
	- Plenty of examples in: [[5.3 & 5.4 CPU Performance and Pipelining]]
### Unit 6: System Architecture  
#### Input / Output  
- [x] **Input / Output:**
	- [[6.1  - Input Output#Input / Output|Input/Output]]
#### Interrupts  
- [x] **Interrupts:** A change in flow that is external to the program.
	- Key difference between traps and interrupts:
		- Traps are *synchronous*: occur at a well-defined point in the program.
		- Interrupts are *asynchronous*: occur unexpectedly with respect to ongoing activity of the system.
- https://www.youtube.com/watch?v=G7bqvpAw7HE (Watch up to `3:25`)
- [[6.1  - Input Output#Interrupts|Interrupts]]
#### Performance  
- [x] **Bottlenecks:** Portions of a task that slow down the task.
	- Performance is often dictated by bottlenecks
	- [[6.2 - Performance and Parallel Computing#Bottlenecks|Bottlenecks]]
- [x] **Improving performance:** improving inefficient implementations, optimize for the common case, reduce sharing delays
	- [[6.2 - Performance and Parallel Computing#Efficient Implementations|Efficient Implementations]]
- [x] Amdahl's law (concept, consider percentage we are contributing to the time)
	- Used to determine the performance gains from an optimization
	- [[6.2 - Performance and Parallel Computing#Amdahl's Law|Amdahl's Law]]
### 6 Questions Total
2 from unit 4
- One will be write an ANNA function (Do not have to write main)
- Other is Unknown
2 for unit 5
- 1 Data path/ control ROM
- 1 pipelining
2 - Short answer from unit 4-6