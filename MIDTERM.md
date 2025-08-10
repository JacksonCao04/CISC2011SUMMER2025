![ Flowchart](<Screenshot 2025-07-23 210028.png>)
```nasm

# MIDTERM.asm - Fixed Assembly Programming Solutions
#Jackson Cao
#==============================================================================
# TASK 1: Equation Calculator - result = (var1 + 2) / (var3 - var2)
#==============================================================================
section .text
    global _start

_start:
    mov eax, [var1]
    add eax, 2
    
    mov ebx, [var3]
    sub ebx, [var2]
    
    mov edx, 0
    div ebx
    
    mov [result], eax
    
    mov eax, 1
    int 0x80

section .data
    var1 dd 10
    var2 dd 3
    var3 dd 8

section .bss
    result resb 4



#==============================================================================
# TASK 2:  K-map simplification of Y = a.b + ā.b + a.b̄
#==============================================================================
b'    b
a'   0     1  
a    1     1



#==============================================================================
# TASK 3: COde identifies an odd or an even number
#==============================================================================
section .text
    global _start

_start:
    mov eax, [number]
    and eax, 1
    jz even_num
    
odd_num:
    mov edx, 3
    mov ecx, odd_msg
    mov ebx, 1
    mov eax, 4
    int 0x80
    jmp exit
    
even_num:
    mov edx, 4
    mov ecx, even_msg
    mov ebx, 1
    mov eax, 4
    int 0x80
    
exit:
    mov eax, 1
    int 0x80

section .data
    number dd 25
    odd_msg db 'odd', 0x0A
    even_msg db 'even', 0x0A
