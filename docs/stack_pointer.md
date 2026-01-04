# Stack Pointer

**R13** is the **Stack Pointer**: used for **accessing the stack memory** via `PUSH` and `POP` operations.

- **Main Stack Pointer** (MSP, or SP_main): the default Stack Pointer. It is select after reset, or when the processor is in **Handler Mode**.
- **Process Stack Pointer** (PSP, or SP_process): can be only used in **Thread Mode**.
- **Note**: the selection of Stack Pointer is determined by a special register call **CONTROL**.
- **Note**: both MSP and PSP are 32-bit, but the lowest two bits of the Stack Pointers (either MSP or PSP) are always zero, and writers to these two bits are ignored.
- **Note**: For most cases, it is not necessary to use the PSP if the application doesn't require an embedded OS. Many simple applications can rely on the MSP completely. The PSP is normally used when an embedded OS is involved, where the stack for the OS kernel and application task are separated.

> [!WARNING]
>
> The initial value of PSP is undefined, but the initial value of MSP is taken from the first word of the memory during the reset sequence.