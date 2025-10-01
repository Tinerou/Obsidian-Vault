## Binary Numbers

### Bits and Bytes

**Bit (b)**: Most basic unit of information on a computer.
	Two states:
- 1: on, true
- 0: off, false

**Byte (B)**: A group of 8 bits

**word**: A contagious group of bytes.
- The precise size of a word is machine-dependent
- Typically refers to the size of an address or integer
- The most common sizes are 32 bits (4 bytes) and 64 bits (8 bytes)

### Converting Binary Numbers into Decimals

Integers are stored in a computer in binary notation where each digit is a bit:
- Each bit represents a power of 2.
- Also called the base-2 system.
![[Pasted image 20250930083230.png]]

### Base-10 Numbers

Our decimal system is a base-10 system: each digit represents a power of 10.
![[Pasted image 20250930151918.png]]
![[Pasted image 20250930151951.png]]
### Converting Decimal Numbers into Binary

Two techniques:
- Subtraction Method
- Division/Remainder Method
The subtraction method is more intuitive than the division/remainder method but requires familiarity with the powers of 2.

**Subtraction Method:**
Iteratively subtract the larges power of 2.

Algorithm to convert decimal number *n* to binary number *b*:
1) Set *b* = 0
2) Find *x*: largest power of 2 that does not exceed *n*
3) Mark a 1 in the position represented by *x* in *b*
4) *n* = *n* - *x*
5) If *n* != 0, repeat steps 2-4.

![[Pasted image 20250930152520.png]]

**Division / Remainder Method**:
Continuously divide by two and record the remainder.

Algorithm to convert decimal number *n* into binary number *b*:
1) Set *k* = 0, *b* = 0
2) Divide *n* = *n* / 2 storing the remainder (0 or 1)
3) Bit 2^k of *b* is set to *r*
4) *k* = *k* + 1
5) If *n* != 0, repeat steps 2-4

![[Pasted image 20250930153439.png]]

### Hexadecimal Numbers

Problem: Binary numbers can be long and diffcult to read.