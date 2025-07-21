W6a-Activity Procedures (GRADED)
![Assembly Program Flowchart](<Activity - Procedures.jpg>)

```nasm
section .data
    newline     db  10

section .bss
    letter      resb 1

section .text
    global _start

_start:
    mov     byte [letter], 'A'
    
print_loop:
    call    print_letter
    call    print_newline
    
    inc     byte [letter]
    cmp     byte [letter], 'Z'
    jle     print_loop
    
    call    exit_program

print_letter:
    mov     rax, 1
    mov     rdi, 1
    mov     rsi, letter
    mov     rdx, 1
    syscall
    ret

print_newline:
    mov     rax, 1
    mov     rdi, 1
    mov     rsi, newline
    mov     rdx, 1
    syscall
    ret

exit_program:
    mov     rax, 60
    xor     rdi, rdi
    syscall
