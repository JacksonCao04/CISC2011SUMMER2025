W3b-Activity Logical  
![ Flowchart](<W3b-Activity Logical instructions .jpg>)


```nasm
section .data
    value1 db 0x5A
    value2 dw 0x1234
    value3 dd 0xDEADBEEF

section .bss
    result resd 1

section .text
    global _start

_start:
    mov al, [value1]
    xor al, al
    mov [result], al
    
    mov ax, [value2]
    xor ax, ax
    mov [result], ax
    
    mov eax, [value3]
    xor eax, eax
    mov [result], eax
    
    mov ebx, 0x12345678
    xor ebx, ebx
    mov [result], ebx
    
    mov eax, 1
    xor ebx, ebx
    int 0x80
```
TEST 
```nasm
section .data
    flags db 0b10101100
    mask1 db 0b00000001
    mask2 db 0b00001000
    mask3 db 0b10000000
    counter dd 5

section .bss
    result resd 1

section .text
    global _start

_start:
    mov al, [flags]
    test al, [mask1]
    jz bit0_clear
    mov dword [result], 1
    jmp check_bit3
bit0_clear:
    mov dword [result], 0

check_bit3:
    mov al, [flags]
    test al, [mask2]
    jz bit3_clear
    mov dword [result], 1
    jmp check_bit7
bit3_clear:
    mov dword [result], 0

check_bit7:
    mov al, [flags]
    test al, [mask3]
    jz bit7_clear
    mov dword [result], 1
    jmp test_zero
bit7_clear:
    mov dword [result], 0

test_zero:
    xor eax, eax
    test eax, eax
    jnz not_zero
    mov dword [result], 1
    jmp test_loop
not_zero:
    mov dword [result], 0

test_loop:
    mov ecx, [counter]
loop_start:
    test ecx, ecx
    jz loop_end
    mov [result], ecx
    dec ecx
    jmp loop_start
loop_end:
    mov eax, 1
    xor ebx, ebx
    int 0x80
