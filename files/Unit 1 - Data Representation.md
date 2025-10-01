## 1.1 - Binary Numbers
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

### Base-10 Numbers

Our decimal system is a base-10 system: each digit represents a power of 10.
![[Pasted image 20250930151918.png]]
![[Pasted image 20250930151951.png]]
### Converting Decimal Numbers into Binary

Integers are stored in a computer in binary notation where each digit is a bit:
- Each bit represents a power of 2.
- Also called the base-2 system.
![[Pasted image 20250930083230.png]]

**Two techniques:**
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

**Why use hexadecimals?**:
- Binary numbers can be long and difficult to read.
- Hexadecimal (base-16 numbers are often used to represent quantities in a computer)
**How to use:**
- Often preceded with '0x' such as: 0x61A2F
- Since 2^4 = 16, it is easy to convert a binary number into a hexadecimal:
	1) Divide the binary number into groups of four digits
	2) Translate each four bit digit group 
	![[Pasted image 20251001105739.png]]
**Examples:**

![[Pasted image 20251001105836.png]]

![[Pasted image 20251001110344.png]]

### Binary Addition

**How?**: Works in the same way as base-10 addition
- 0+0 = 0
- 0+1 = 1
- 1+1 = 10

**Examples:**

![[Pasted image 20251001110708.png]]

### Character Representation

**Characters** (letters, digits, symbols) are represented using a code where each bit pattern represents a unique character.

**Two Common Formats** (virtually all machines use either or both formats):
- *ASCII* (American Standard Code for Information Interchange) is a *7-bit code*.
- *Unicode* is as *16-bit code*.
	- First 128 bit patterns are same as ASCII (zero-extended)
	- Includes letters and characters from non-English alphabets
	- Includes more symbols (including math)

**ASCII CARACTER TABLE:**

![[Pasted image 20251001111724.png]]

**Unicode CHARACTER TABLE:**

![[Pasted image 20251001111849.png]]

### Image Representation

**What is image representation?:**
- Images can be thought of as a 2-dimensional array of pixels
- Each pixel is a small dot within the image that has been assigned a color
- With 24 bits - there are 16,777,216 (2^24) possible colors. However, computer monitors are unable to display 16 million colors.
- Color printers use a different color model - CYMK (Cyan, Yellow, Magenta, Black).
- Images are typically stored in a compressed format (such as JPEG).
	- Compression algorithms take advantage of the fact that pixels near one another are often close to the same color.
	- 
**RGB Color Model:**
- A color is commonly represented using an RGB-value.

![[Pasted image 20251001112758.png]]

### Sound Representation

Sounds, in the physical world, are waves of air pressure. 
To digitize the sound wave curve, need to sample the wave periodically, measuring the instantaneous amplitude.

**Sampling:**
- The *Nyquist-Shannon sampling theorem* states that if the highest frequency of a sound is N Hertz, a sampling rate of at least 2N can reconstruct the original sound.
- The human ear can detect sounds up to about 22,000 Hz.
- CD quality sound is captured at 44,100 samples/sec
- Each sample is commonly encoded using 16 bits (a 2's complement number).
- Just like images, audio formats use compression

**Example:**
How much memory is needed to store a 30 second audio file (uncompressed)?
$$ \left( \frac{30\sec}{file}\right)\left( \frac{44100samples}{\sec} \right) \left( \frac {2bytes}{sample} \right)$$