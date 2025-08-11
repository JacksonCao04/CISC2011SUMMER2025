Project (GRADED)
![Assembly Program Flowchart](<Project.jpg>)

```nasm
#Jackson Cao
#Project (GRADED)
#==============================================================================
# TASK 1
#==============================================================================
section .text
    global _start

_start:
    call encrypt_message
    call write_to_file
    call exit_program

encrypt_message:
    push ebp
    mov ebp, esp
    
    mov ecx, 5
    mov esi, 0
    
encrypt_loop:
    mov al, [plaintext + esi]
    mov bl, [key + esi]
    xor al, bl
    mov [encrypted + esi], al
    inc esi
    loop encrypt_loop
    
    leave
    ret

decrypt_message:
    push ebp
    mov ebp, esp
    
    mov ecx, 5
    mov esi, 0
    
decrypt_loop:
    mov al, [encrypted + esi]
    mov bl, [key + esi]
    xor al, bl
    mov [decrypted + esi], al
    inc esi
    loop decrypt_loop
    
    leave
    ret

write_to_file:
    push ebp
    mov ebp, esp
    
    mov eax, 8
    mov ebx, filename
    mov ecx, 0644o
    int 0x80
    mov [fd], eax
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, label1
    mov edx, label1_len
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, plaintext
    mov edx, 5
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, newline
    mov edx, 1
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, label2
    mov edx, label2_len
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, key
    mov edx, 5
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, newline
    mov edx, 1
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, label3
    mov edx, label3_len
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, encrypted
    mov edx, 5
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, newline
    mov edx, 1
    int 0x80
    
    call decrypt_message
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, label4
    mov edx, label4_len
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, decrypted
    mov edx, 5
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, newline
    mov edx, 1
    int 0x80
    
    mov eax, 6
    mov ebx, [fd]
    int 0x80
    
    leave
    ret

exit_program:
    mov eax, 1
    mov ebx, 0
    int 0x80

section .data
    plaintext db 'HELLO'
    key db 'world'
    label1 db 'Plain text: '
    label1_len equ $ - label1
    label2 db 'Key: '
    label2_len equ $ - label2
    label3 db 'Encrypted text: '
    label3_len equ $ - label3
    label4 db 'Decrypted text: '
    label4_len equ $ - label4
    newline db 0x0A
    filename db 'output.txt', 0

section .bss
    encrypted resb 5
    decrypted resb 5
    fd resb 4

#==============================================================================
# TASK 2a
#==============================================================================
section .text
    global _start

_start:
    push 20000
    call count
    add esp, 4
    
    call write_output
    
    mov eax, 1
    mov ebx, 0
    int 0x80

count:
    push ebp
    mov ebp, esp
    sub esp, 4
    
    mov ecx, [ebp+8]
    mov dword [ebp-4], 0
    
count_loop:
    inc dword [ebp-4]
    loop count_loop
    
    mov eax, [ebp-4]
    mov [result], eax
    
    leave
    ret

write_output:
    push ebp
    mov ebp, esp
    
    mov eax, 8
    mov ebx, filename
    mov ecx, 0644o
    int 0x80
    mov [fd], eax
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, msg1
    mov edx, msg1_len
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, msg2
    mov edx, msg2_len
    int 0x80
    
    mov eax, 6
    mov ebx, [fd]
    int 0x80
    
    leave
    ret

section .data
    filename db 'counter_fun.txt', 0
    msg1 db 'Function Counter Implementation', 0x0A
    msg1_len equ $ - msg1
    msg2 db 'Counter completed: 20000 iterations', 0x0A
    msg2_len equ $ - msg2

section .bss
    result resb 4
    fd resb 4
#==============================================================================
# TASK 2b
#==============================================================================
section .text
    global _start

_start:
    push 20000
    call count_recursive
    add esp, 4
    
    call write_output
    
    mov eax, 1
    mov ebx, 0
    int 0x80

count_recursive:
    push ebp
    mov ebp, esp
    
    mov eax, [ebp+8]
    
    cmp eax, 0
    je base_case
    
    dec eax
    push eax
    call count_recursive
    add esp, 4
    
base_case:
    leave
    ret

write_output:
    push ebp
    mov ebp, esp
    
    mov eax, 8
    mov ebx, filename
    mov ecx, 0644o
    int 0x80
    mov [fd], eax
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, msg1
    mov edx, msg1_len
    int 0x80
    
    mov eax, 4
    mov ebx, [fd]
    mov ecx, msg2
    mov edx, msg2_len
    int 0x80
    
    mov eax, 6
    mov ebx, [fd]
    int 0x80
    
    leave
    ret

section .data
    filename db 'counter_rec.txt', 0
    msg1 db 'Recursive Counter Implementation', 0x0A
    msg1_len equ $ - msg1
    msg2 db 'Counter completed: 20000 iterations', 0x0A
    msg2_len equ $ - msg2

section .bss
    fd resb 4
