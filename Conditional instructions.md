 Conditional instructions
![ Flowchart](<Conditional instructions.jpg>)


```nasm
section .data
    num1 dd 45
    num2 dd 78
    num3 dd 23
    num4 dd 91
    num5 dd 56

section .bss
    largest resd 1

section .text
    global _start

_start:
    mov eax, [num1]
    
    cmp eax, [num2]
    jge check_num3
    mov eax, [num2]
    
check_num3:
    cmp eax, [num3]
    jge check_num4
    mov eax, [num3]
    
check_num4:
    cmp eax, [num4]
    jge check_num5
    mov eax, [num4]
    
check_num5:
    cmp eax, [num5]
    jge store_largest
    mov eax, [num5]
    
store_largest:
    mov [largest], eax
    
    xor ecx, ecx
    
even_loop:
    cmp ecx, 20
    jg exit_program
    add ecx, 2
    jmp even_loop
    
exit_program:
    mov eax, 1
    xor ebx, ebx
    int 0x80
