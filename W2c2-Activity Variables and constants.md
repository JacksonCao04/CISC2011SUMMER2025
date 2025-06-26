# W2c2-Activity Variables and constants  
![ Flowchart](<W2c2-Activity Variables and constants.jpg>)


# W2c2-Activity Variables and constants  
```nasm
section .text
global _start

_start:
mov eax, [var1]
mov ebx, [var2]
add eax, ebx
mov [result], eax

mov eax,1
int 0x80

segment .bss
result resd 1

segment .data
var1 dd 10
var2 dd 15

