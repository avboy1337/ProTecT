# ProTecT
Copyright 1995-1996 Philippe Paquet

### Description

ProTecT is an MS-DOS packer designed to protect executables from analysis.

The protector is written in Turbo Pascal with original comments in French. The stub code and the modules are written in x86 assembly.

### It's from 1995! Why should I care?

This packer use a number of interesting techniques that are still relevant today and can be leveraged to defend against analysis:
* __Executing code backward__
  * Using the single step mode of the microprocessor, we can adjust the instruction pointer as instructions are executed and run code backward
  * Any analysis tool that also use the single step mode of the microprocessor will interfere with proper execution
  * Decompilers will have a particularly hard time with this technique
* __Return oriented programming__
  * If you think that ROP was invented in 2012, think again...
  * A full call-stack is created early on and the rest of the code just returns to the right location
  * This allows the use of functions without a visible code structure
  * A return instruction could be a jump or the end of a function
    * It is impossible to know without knowing the call-stack
  * Decompilers will have a particularly hard time with this technique
* __Pointing the stack to critical code or data while the stack is not being used__
  * Any analysis tool that use the stack will destroy critical code or data
* __Using a single buffer to decrypt and execute code__
  * This make analysis harder:
    * You never have all the code mapped to its execution location in memory
    * You never have all the code decrypted in memory
* __Calculating decryption keys from debugger detections__
  * This allow to decouple the consequence from the point of detection
* __Jumping to instructions hidden inside other instructions__
  * This break instruction decoding by the debugger
  * Debugger have improved significantly but, surprisingly, this is still somewhat effective

### Test executable

`test_u.exe` is the unprotected test executable
`test_p.exe` is the protected test executable

### Contact

If you have any questions, feel free to contact me at philippe@paquet.email
