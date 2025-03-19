# Quiz 2

## Code
```assembly
section .data
    a dd 5      ; Define a = 5
    b dd 3      ; Define b = 3
    c dd 2      ; Define c = 2
    d dd 4      ; Define d = 4
    x dd 0      ; Storage for result x

section .text
    global _start

_start:
    ; Load 'a' into eax
    mov eax, [a]
    ; Multiply eax by 'b' (eax = a * b)
    imul eax, [b]  

    ; Store (a * b) result in ebx
    mov ebx, eax  

    ; Load 'c' into eax
    mov eax, [c]
    ; Multiply eax by 'd' (eax = c * d)
    imul eax, [d]  

    ; Add (a * b) + (c * d)
    add eax, ebx  

    ; Store final result in 'x'
    mov [x], eax  

    ; Exit program (for Linux systems)
    mov eax, 60   ; syscall: exit
    xor edi, edi  ; status 0
    syscall       ; call kernel
```
