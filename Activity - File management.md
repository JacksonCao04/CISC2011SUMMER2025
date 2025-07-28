Challenges in Performing the Lab
File Descriptor Management: Tracking the file descriptor between create and append operations required careful handling to avoid file access errors.
File Opening Modes: Understanding the octal values for file permissions (0666) and open flags (O_CREAT|O_WRONLY = 0102, O_WRONLY|O_APPEND = 02002) 
String Length Calculation: Using the $ - "label technique to calculate string lengths at assembly time rather than hardcoding values."



```nasm
section .data
    number      dq  17
    msg_even    db  'even', 10
    len_even    equ $ - msg_even
    msg_odd     db  'odd', 10
    len_odd     equ $ - msg_odd

section .text
    global _start

_start:
    mov     rax, [number]
    
    call    check_odd_even
    
    mov     rax, 60
    xor     rdi, rdi
    syscall

check_odd_even:
    push    rax
    
    and     rax, 1
    jz      print_even
    
    call    print_odd
    jmp     check_done
    
print_even:
    mov     rax, 1
    mov     rdi, 1
    mov     rsi, msg_even
    mov     rdx, len_even
    syscall
    jmp     check_done

print_odd:
    mov     rax, 1
    mov     rdi, 1
    mov     rsi, msg_odd
    mov     rdx, len_odd
    syscall

check_done:
    pop     rax
    ret
