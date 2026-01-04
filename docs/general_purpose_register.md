# General Purpose Register

Registers R0 to R12 are general purpose registers.

- low registers (R0 to R7): due to the limited available space in the instruction set, many 16-bit instructions can only access the low registers.
- high registers(R8 - R12): those registers can be used with 32-bit instructions, and a few with 16-bit instructions, like `MOV` (move).

> [!WARNING]
>
> The initial value of R0 to R12 are undefined.