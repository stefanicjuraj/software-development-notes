# Binary Code Analysis

_What if source code is not available?_ This is particularly true when evaluating closed source, proprietary applications. You can reverse engineer the binary.

Binary auditing requires a more expansive skill set than source code auditing requires:

- in assembly language,
- executable file formats,
- compiler behavior,
- operating system internals, and
- various other, lower-level skills

Usually performed to reverse engineer the binary by making use of some tools that are categorized as:

- **Disassemblers**

Used to convert binary code into assembly code (convert machine language into a user-friendly format).

- **Debuggers**

Expand the functionality of a disassembler by allowing you to step through the code one line at a time, during runtime.

- **Decompilers**

Attempt to generate source code from a compiled binary. Languages that offer the best opportunity for decompilation are those that are compiled to an intermediate, machine independent form as in Java or Python.

For example, the Java byte code contains a significant amount of descriptive information which makes the decompilation easier than in C code.

- **Hex Editors**

Allow the binary to be viewed in the editor, to view the actual bytes as a sequence of hexadecimal (or decimal, binary or ASCII character) values and change it as required.

There are different types of hex editors available that are used for different functions.

- **PE** and **Resource Viewer**

**The Portable Executable (PE)** format is a file format for _executables_, _object code_, _DLLs_, _FON Font_ files, and others used in 32-bit and 64-bit versions of Windows operating systems (usually installers).

PE formatted binary code has a specific section of data at the beginning that tells the OS how to set up and initialize the program.

Analogous formats to PE are **ELF** (used in Linux and other versions of Unix) and **Mach-O** (used in Mac OS X).

These bytes are important to reverse engineering as it provides useful information based on which you will generally want/need to:

- Make the program do something different than originally designed
- Change the code back into its original form (e.g. before code protection measures).

---

[**`View Static Code Analysis`**](static-code-analysis)
[**`View Dynamic Code Analysis`**](dynamic-code-analysis)
