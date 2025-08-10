W6a-Activity Procedures (GRADED)
![Assembly Program Flowchart](<Activity - Procedures.jpg>)

```nasm
section .text
    global _start

_start:
    mov ecx, 26
    mov eax, 65

print_loop:
    push ecx
    push eax
    
    mov [char], eax
    call print_char
    call print_newline
    
    pop eax
    pop ecx
    
    inc eax
    loop print_loop
    
    call exit

print_char:
    mov edx, 1
    mov ecx, char
    mov ebx, 1
    mov eax, 4
    int 0x80
    ret

print_newline:
    mov edx, 1
    mov ecx, newline
    mov ebx, 1
    mov eax, 4
    int 0x80
    ret

exit:
    mov eax, 1
    mov ebx, 0
    int 0x80

section .data
    newline db 0x0A

section .bss
    char resb 1
