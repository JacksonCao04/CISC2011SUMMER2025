section .data
    a dd 5
    b dd 3
    c dd 2
    d dd 4

section .bss
    x resd 1

section .text
    global _start

_start:
    mov eax, [a]
    imul eax, [b]
    mov ebx, eax
    
    mov eax, [c]
    imul eax, [d]
    
    add eax, ebx
    mov [x], eax
    
    mov eax, 1
    xor ebx, ebx
    int 0x80
