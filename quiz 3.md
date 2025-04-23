section .data
    x       dd 5          ; Number to calculate factorial of
    result  dd 1          ; Final result (starts as 1)

section .text
    global _start

_start:
    mov ecx, [x]          ; ECX = counter (5)
    mov eax, 1            ; EAX = accumulator, starting from 1

factorial_loop:
    cmp ecx, 1
    jl done               ; if counter < 1, we're done
    imul eax, ecx         ; eax *= ecx
    dec ecx               ; ecx--
    jmp factorial_loop

done:
    mov [result], eax     ; store result in memory

    ; exit
    mov eax, 1            ; syscall: exit
    int 0x80

section .bss
