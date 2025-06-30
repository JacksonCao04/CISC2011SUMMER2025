W3a-Activity Arithmetic instructions
![ Flowchart](<W3a-Activity Arithmetic instructions.jpg>)


```nasm
equation1.asm
section .data
    var1 dd 5

section .bss
    result resd 1

section .text
    global _start

_start:
    mov eax, [var1]
    neg eax
    imul eax, 10
    mov [result], eax
    
    mov eax, 1
    xor ebx, ebx
    int 0x80

```
```nasm
equation2.asm
section .data
    var1 dd 10
    var2 dd 20
    var3 dd 30
    var4 dd 40

section .bss
    result resd 1

section .text
    global _start

_start:
    mov eax, [var1]
    add eax, [var2]
    add eax, [var3]
    add eax, [var4]
    mov [result], eax
    
    mov eax, 1
    xor ebx, ebx
    int 0x80

```
```nasm
equation3.asm
section .data
    var1 dd 4
    var2 dd 6
    var3 dd 50

section .bss
    result resd 1

section .text
    global _start

_start:
    mov eax, [var1]
    neg eax
    imul eax, [var2]
    add eax, [var3]
    mov [result], eax
    
    mov eax, 1
    xor ebx, ebx
    int 0x80
```
```nasm
equation4.asm
section .data
    var1 dd 20
    var2 dd 7

section .bss
    result resd 1

section .text
    global _start

_start:
    mov eax, [var1]
    shl eax, 1
    
    mov ebx, [var2]
    sub ebx, 3
    
    cdq
    idiv ebx
    mov [result], eax
    
    mov eax, 1
    xor ebx, ebx
    int 0x80
```
