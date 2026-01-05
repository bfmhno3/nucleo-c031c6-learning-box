# Program Status Registers

The **Program Status Register** is composed of three status registers:

- Application PSR (APSR)
- Execution PSR (EPSR)
- Interrupt PSR (IPSR)

|      |  31  |  30  |  29  |  28  |  27  | 26:25  |  24  | 23:20 | 19:16 | 15:10  |  9   |       8:0        |
| :--: | :--: | :--: | :--: | :--: | :--: | :----: | :--: | :---: | :---: | :----: | :--: | :--------------: |
| APSR |  N   |  Z   |  C   |  V   |  Q   |        |      |       |  GE*  |        |      |                  |
| IPSR |      |      |      |      |      |        |      |       |       |        |      | Exception Number |
| EPSR |      |      |      |      |      | ICI/IT |  T   |       |       | ICI/IT |      |                  |

Description of bit fields in program status registers:

| Bit              | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| N                | Negative flag                                                |
| Z                | Zero flag                                                    |
| C                | Carry (or NOT borrow) flag                                   |
| V                | Overflow flag                                                |
| Q                | Sticky saturation flag (not available in ARMv6-M)            |
| GE[3:0]          | Greater-Than or Equal flags for each byte lane (ARMv7E-M only; not available in ARMv6-M or Cortex-M3) |
| ICI/IT           | Interrupt-Continuable Instruction (ICI) bits, IF-THEN instruction status bit for conditional execution (not available in ARMv6-M) |
| T                | Thumb state, always 1; trying to clear this bit will cause a fault exception |
| Exception Number | Indicates which exception the processor is handling.         |

Use `MSR` and `MRS` to write and read values in registers:

```assembly
MRS r0, PSR ; Read the combined program status word
MSR PSR, r0 ; write combined program state word

MRS r0, APSR ; Read Flag state into R0
MRS r0, IPSR ; Read Exception / Interrupt state
MSR APSR, r0 ; Write Flag state
```

- use `PSR` when accessing xPSR
- The ERSR cannot be accessed by software code directly using `MRS` (read as zero) or `MSR`.
- The IPSR is read only and can be read from combined PSR (xPSR)

> [!IMPORTANT]
>
> Some of the bit fields in the APSR and EPSR are not available in ARMv6-M architecture (e.g., the Cortex-M0 processor).