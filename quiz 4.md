```assembly
section .data
    result_msg db "Result: ", 0
    newline db 0xA

section .bss
    result resd 1

section .text
    global _start

_start:
    ; Assign integers
    mov eax, 5      ; x
    push eax
    mov eax, 10     ; y
    push eax
    mov eax, 7      ; z
    push eax

    ; Call function
    call _sum3
    add esp, 12     ; clean up arguments (3 * 4 bytes)

    ; Store result in variable
    mov [result], eax

    ; Exit
    mov eax, 1      ; syscall: exit
    xor ebx, ebx
    int 0x80

_sum3:
    push ebp
    mov ebp, esp

    mov eax, [ebp+8]   ; z
    add eax, [ebp+12]  ; + y
    add eax, [ebp+16]  ; + x

    pop ebp
    ret
```
