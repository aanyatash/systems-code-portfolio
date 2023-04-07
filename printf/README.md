Files to look at: printf.c, strings.c, test_strings_printf.c

The purpose of this code is to create a string formatting library. So, this includes a strings library which can concatenate and copy strings and a printf library which supports the %x, %d, %c, %s, %p, %%, %pI format codes. The user inputs to the printf function are assumed to be well-formed.

The most common bugs I ran into with this library were pointer or memory bugs and to debug these I would go into gdb and step through my code to see what was happening. Writing unit tests to account for edge cases and to ensure intended functionality was also how I debugged my code. Since I couldn't print anything out, these were the two methods that were used for debugging.


Coding the disassembler took a lot of time as I had to read through the ARM intrsuction set manual and learn how load/store, branch, and data processing instructions were encoded.

My disassembler handles all data processing and branch/branch link instructions. 

For data processing instructions, the disassembler takes into account all of them and for shift
instructions, it uses instructions in the format mov, r1, r2, lsl #2. My disassembler handles
immediate values that need to be rotated, shift operations on registers, and shift operations on
numbers.

It also handles ldr, str, ldrb, and strb instructions. For these instructions, it takes into account
positive or negative offsets, the write-back bit, and pre and post indexing. It also handles shift by
a number and register shifts with logical shift operations. 

I tested my disassembler against the x/30i 0x8000 gdb command and all of the instructions appeared to be correct,
with any push pop instructions being just the encoding values as I did not implement this.

The instr.s assembly file I made can be used for reference on the types of instructions my disassembler should be able to 
handle. I used this file for testing.
