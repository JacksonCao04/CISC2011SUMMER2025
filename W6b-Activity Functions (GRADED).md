W6b-Activity Functions (GRADED)
![Assembly Program Flowchart](<W6b-Activity Functions (GRADED).jpg>)

```nasm
section .text
    global _start

_start:
    mov eax, 15
    push eax
    call check_odd_even
    
    add esp, 4
    
    mov eax, 1
    mov ebx, 0
    int 0x80

check_odd_even:
    push ebp
    
    mov ebp, esp
    
    sub esp, 16
    
    mov eax, DWORD[ebp+8]
    mov DWORD[ebp-4], eax
    
    mov eax, DWORD[ebp-4]
    and eax, 1
    mov DWORD[ebp-8], eax
    
    cmp DWORD[ebp-8], 0
    je display_even
    
display_odd:
    mov DWORD[ebp-12], 'odd'
    mov byte[ebp-9], 0x0A
    
    lea ecx, [ebp-12]
    mov edx, 4
    mov ebx, 1
    mov eax, 4
    int 0x80
    jmp function_epilogue
    
display_even:
    mov DWORD[ebp-12], 'even'
    mov byte[ebp-8], 0x0A
    
    lea ecx, [ebp-12]
    mov edx, 5
    mov ebx, 1
    mov eax, 4
    int 0x80
    
function_epilogue:
    leave
    ret
