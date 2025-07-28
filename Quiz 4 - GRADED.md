```nasm

section .data
    x dd 10
    y dd 20
    z dd 30
    result dd 0
    fmt db "x = %d, y = %d, z = %d", 10, "Sum (x + y + z) = %d", 10, 0

section .text
    global main
    extern printf

add_three_numbers:
    push rbp
    mov rbp, rsp
    
    mov eax, edi
    add eax, esi
    add eax, edx
    
    mov rsp, rbp
    pop rbp
    ret

main:
    push rbp
    mov rbp, rsp
    
    mov edi, [x]
    mov esi, [y]
    mov edx, [z]
    
    call add_three_numbers
    
    mov [result], eax
    
    mov rdi, fmt
    mov esi, [x]
    mov edx, [y]
    mov ecx, [z]
    mov r8d, [result]
    xor eax, eax
    call printf
    
    xor eax, eax
    
    mov rsp, rbp
    pop rbp
    ret
