# Variables and constants
## Flow chart
<img width="446" alt="image" src="https://github.com/user-attachments/assets/635855c5-4d40-48f2-b8c0-cd43bf5f21f9" />

## Code
```assembly
section .text
    global _start

_start:
    ; Load var1 into eax
    mov eax, [var1]
    
    ; Add var2 to eax
    add eax, [var2]

    ; Store the result into result
    mov [result], eax

    ; Exit syscall
    mov eax, 1          ; sys_exit
    int 0x80

section .data
    var1 dd 10      ; Initialized variable with value 10
    var2 dd 15      ; Initialized variable with value 15

section .bss
    result resd 1   ; Uninitialized variable to store result
```
## What were your challenges in performing the lab (from design to the implementation phases)?
The challenge is keeping track of which register held what value, and I had to write everything down with a pen and paper. Also .data and .bss segments are very easy to mix up.
