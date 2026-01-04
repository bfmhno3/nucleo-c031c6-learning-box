# Link Register

**R14** is the **Link Register**: used for **holding the return address when calling a function or subroutine**.

- At the end of the function or subroutine, the program control can return to the calling program and resume by loading the value of **LR**  into the **Program Counter** (PC).

> [!NOTE]
>
> If a function needs to call another function or subroutine, it needs to save the value of LR in the stack first. Otherwise, the current value in LR will be lost when the function call is made.

> [!NOTE]
>
> During exception handling, the LR is also updated automatically to a special **EXEC_RETURN** (Exception Return) value, which is then used for triggering the exception return at the end of the exception handler.

> [!NOTE]
>
> Although the return address values in the Cortex-M processors are always even (**bit 0 is zero because the instructions must be aligned to half-word address**), bit 0 of LR is readable and writeable. Some of the branch / call operations require that bit 0 of LR (or any register being used) be set to 1 to indicate Thumb state.

