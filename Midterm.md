# Midterm

## result=(var1+2)/(var3-var2)
## a
```assembly
; Variables:
;   var1 = 10
;   var2 = 3
;   var3 = 8
;   result = (10+2)/(8-3) = 12/5 = 2 

section .data
        var1 dd 10      
        var2 dd 3       
        var3 dd 8       

section .text
        global _start

_start:
        mov eax, [var1]
        add eax, 2
        
        mov ebx, eax
        
        mov eax, [var3]
        sub eax, [var2]
        
        mov ecx, eax
        
        test ecx, ecx
        jz div_by_zero
        
        mov eax, ebx    
        cdq             
        idiv ecx        
        
        add eax, '0'    
        mov [result], eax
        
        mov eax, 1
        int 0x80

div_by_zero:
        mov eax, 'E'
        mov [result], eax
        mov eax, 1
        int 0x80

segment .bss
        result resb 1   
```
## b
```assembly
mov eax, SYS_WRITE
mov ebx, STDOUT
mov ecx, result     
mov edx, 1        
int 0x80
```

# Simplify Equation
<img width="315" alt="image" src="https://github.com/user-attachments/assets/e5015694-8e73-400c-a9fc-fd33707be67f" />

## Y=a+b

# identifies an odd or an even number

## a
### 1)Define a number
### 2)Use the TEST instruction with the value 1 to check the LSB
### 3)Use the Zero Flag (ZF) to determine if the number is odd or even
### 4)If ZF=1 (LSB was 0), the number is even
### If ZF=0 (LSB was 1), the number is odd
### 5)Display output message

## b&c
```assembly
SYS_EXIT  equ 1
SYS_WRITE equ 4
STDOUT    equ 1

section .data
    number dd 8                  ; Test number 
    
    msg_even db 'even number', 0xA, 0xD
    len_even equ $ - msg_even
    
    msg_odd db 'odd number', 0xA, 0xD
    len_odd equ $ - msg_odd

section .text
    global _start

_start:
    ; Load number to test
    mov eax, [number]
    
    test eax, 1          ; Test if LSB is set (affects flags only)
    jz even_number       ; Jump if Zero Flag is set (LSB=0, even number)
    
    ;odd number
    mov eax, SYS_WRITE
    mov ebx, STDOUT
    mov ecx, msg_odd
    mov edx, len_odd
    int 0x80
    jmp exit_program
    
even_number:
    mov eax, SYS_WRITE
    mov ebx, STDOUT
    mov ecx, msg_even
    mov edx, len_even
    int 0x80
    
exit_program:
    mov eax, SYS_EXIT
    xor ebx, ebx         ; Zero return code
    int 0x80
```
