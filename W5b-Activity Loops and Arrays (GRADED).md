W5b-Activity Loops and Arrays (GRADED)
![Assembly Program Flowchart](<Activity - Loops and arrays instructions (1).jpg>)

```nasm
section .data
    array dd 45, 89, 23
    
section .text
    global _start

_start:
    mov ecx, 10
    xor ebx, ebx
counter_loop:
    inc ebx
    loop counter_loop
    
    xor eax, eax
    mov ebx, 1
    xor edx, edx
    mov ecx, 10
    
fib_loop:
    add edx, eax
    mov edi, eax
    add edi, ebx
    mov eax, ebx
    mov ebx, edi
    dec ecx
    jnz fib_loop
    
    mov eax, 3
    mov ebx, [array]
    mov ecx, array
    add ecx, 4
    
find_max:
    cmp ebx, [ecx]
    jge skip
    mov ebx, [ecx]
skip:
    add ecx, 4
    dec eax
    jnz find_max
    
    mov eax, 1
    xor ebx, ebx
    int 0x80
