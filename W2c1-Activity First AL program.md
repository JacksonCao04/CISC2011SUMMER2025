Assembly Language Lab 
![Assembly Program Flowchart](./Activity%20-%20First%20assembly%20language%20code%20(1).jpg)

```nasm
section .data
    msg db 'I came,', 0xA, 'I saw,', 0xA, 'I conquered.', 0xA, 0xA
    msglen equ $ - msg

section .text
    global _start

_start:
    mov eax, 4
    mov ebx, 1
    mov ecx, msg
    mov edx, msglen
    int 0x80

    mov eax, 1
    mov ebx, 0
    int 0x80
