# Assembly Language in ARM Assembler

```assembly
label
	mnemonic operand1, operand2, ... ; Comments
```

- `label` is a reference to an **address location**.
- Generally, the first operand is the destination of the operation.

| Operation       | The role of first operand                                    |
| --------------- | ------------------------------------------------------------ |
| Data Processing | the destination of the operation                             |
| Memory Read     | the register which data is loaded into                       |
| Memory Write    | the value of the first operand is the address of the memory to be written into |

- immediate data are prefixed with `#`
- the text after each semicolon `;` is a comment, which makes programs easier for human to understand
- `'A'` is similar with that in C.
- use `EQU` to define constants, for example `NVIC_IRQ_SETEN EQU 0xE 000E100`
- when using pseudo instructions to load a value into a register, the value requires an `=` prefix, for example: `LDR R0, =NVIC_IRQ_SETEN`
- constants is similar with immediate data, when loading a constants into a register, a `#` is needed, for example: `MOVS R1, #NVIC_IRQ0_ENABLE`

Commonly Used Directives for Inserting Data into a Program (**hard-coding static values**)

| Type of Data to Insert            | ARM Assembler | Example                           |
| --------------------------------- | ------------- | --------------------------------- |
| Byte                              | `DCB`         | `DCB 0x12`                        |
| Half-word                         | `DCW`         | `DCW 0x1234`                      |
| Word                              | `DCD`         | `DCD 0x01234567`                  |
| Double-word                       | `DCQ`         | `DCQ 0x12345678FF0055AA`          |
| Floating point (single precision) | `DCFS`        | `DCFS 1E3`                        |
| Floating point (double precision) | `DCFD`        | `DCFD 3.14159`                    |
| String                            | `DCB`         | `DCB "Hello\n" 0,`                |
| Instruction                       | `DCI`         | `DCI 0xBF00; Breakpoint (BKPT 0)` |

Commonly Used Directives

| Directive                                    | ARM Assembler                                                |
| -------------------------------------------- | ------------------------------------------------------------ |
| `THUMB`                                      | Specify assembly code as Thumb instruction in Unified Assembly Language (UAL) format. |
| `CODE16`                                     | Specify assembly code as Thumb instruction in legacy pre-UAL syntax. |
| `AREA <section_name>, attr1, attr2, ...`     | Instructs the assembler to assemble a new code or data section. **Section are independent, named, indivisible chunks of code or data that are manipulated by the linker**. |
| `SPACE <num_of_bytes>`                       | Reserves a block of memory and fills it with zeros.          |
| `FILL <num_of_bytes>, <value>, <value_size>` | Reserves a block of memory and fills it with the specified value. The size of the value can be byte, half-word, or word, specified by value_sizes (1/2/4). |
| `ALIGN <expr>, <offset>, <pad>, <padsize>`   | Aligns the current location to a specified boundary by padding with zeros or NOP instructions |
| `EXPORT <symbol>`                            | Declare a symbol that can be used by the linker to resolve symbol references in separate object or library files. |
| `IMPORT <symbol>`                            | Declare a symbol reference in separate object or library files that is to be resolved by linker. |
| `LTORG`                                      | Instructs the assembler to assemble the current literal pool immediately. Literal pool contains data such as constants data such as constant values for `LDR` pseudo instruction. |

Suffixes for Cortex-M Assembly Language

| Suffixes                                                     | Descriptions                                                 | Example       |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------- |
| `S`                                                          | Update APSR (Application Program Status Register, such as Carry, Overflow, Zero and Negative flags) | `ADDS R0, R1` |
| `EQ`, `NE`, `CS`, `CC`, `MI`, `PL`, `VS`, `VC`, `HI`, `LS`, `GE`, `LT`, `GT`, `LE` | Conditional Execution. EQ = Equal, NE = not Equal, LT = Less Than, GT = Greater Than, etc. | `BEQ label`   |
| `.N`, `.W`                                                   | Specify the use of 16-bit (narrow) instruction or 32-bit (wide) instruction |               |
| `.32`, `.F32`                                                | Specify the operation is for 32-bit single-precision data. In most toolchains, the `.32` suffix is optional. |               |
| `.64`, `.F64`                                                | Specify the operation is for 64-bit double-precision data. In most toolchains, the `.64` suffix is optional. |               |

