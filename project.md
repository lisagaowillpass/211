```assembly
SECTION .data
filename     db 'output.txt', 0
plaintext    db 'HELLO'
key          db 'world'
encrypted    db 5 dup(0)
decrypted    db 5 dup(0)
newline      db 10

line1        db 'Plain text: HELLO', 10
line2        db 'Key: world', 10
line3        db 'Encrypted text: ', 0
line4        db 'Decrypted text: ', 0

SECTION .bss
fd_out resb 1

SECTION .text
global _start

_start:
    ; Create file
    mov eax, 8          ; sys_creat
    mov ebx, filename
    mov ecx, 0777o      ; permissions
    int 0x80
    mov [fd_out], eax

    ; XOR encryption
    mov ecx, 0
encrypt_loop:
    mov al, [plaintext + ecx]
    xor al, [key + ecx]
    mov [encrypted + ecx], al
    inc ecx
    cmp ecx, 5
    jne encrypt_loop

    ; XOR decryption (same as encryption)
    mov ecx, 0
decrypt_loop:
    mov al, [encrypted + ecx]
    xor al, [key + ecx]
    mov [decrypted + ecx], al
    inc ecx
    cmp ecx, 5
    jne decrypt_loop

    ; Write to file
    ; line1
    mov eax, 4
    mov ebx, [fd_out]
    mov ecx, line1
    mov edx, 18
    int 0x80

    ; line2
    mov eax, 4
    mov ecx, line2
    mov edx, 13
    int 0x80

    ; line3 + encrypted
    mov eax, 4
    mov ecx, line3
    mov edx, 18
    int 0x80

    mov eax, 4
    mov ecx, encrypted
    mov edx, 5
    int 0x80

    mov eax, 4
    mov ecx, newline
    mov edx, 1
    int 0x80

    ; line4 + decrypted
    mov eax, 4
    mov ecx, line4
    mov edx, 18
    int 0x80

    mov eax, 4
    mov ecx, decrypted
    mov edx, 5
    int 0x80

    mov eax, 4
    mov ecx, newline
    mov edx, 1
    int 0x80

    ; Exit
    mov eax, 1
    int 0x80
```
