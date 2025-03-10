### Solution

```assembly
section .data
    msg db "I came,", 0xA, "I saw,", 0xA, "I conquered.", 0xA
    len equ $ - msg

section .text
    global _start

_start:
    mov eax, 4          ; syscall number (sys_write)
    mov ebx, 1          ; file descriptor (stdout)
    mov ecx, msg        ; message to write
    mov edx, len        ; message length
    int 0x80            ; perform syscall

    mov eax, 1          ; syscall number (sys_exit)
    xor ebx, ebx        ; exit status 0
    int 0x80            ; perform syscall

section .data
msg db "I came,", 0xA, "I saw,", 0xA, "I conquered.", 0xA
len equ $ - msg
```
