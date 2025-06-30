W3b-Activity Logical  
![ Flowchart](<W3b-Activity Logical instructions .jpg>)


```nasm
section .data
    var1    dd  5
    
section .bss
    result  resd 1
    
section .text
    global _start
    
_start:
    mov     eax, [var1]
    neg     eax
    mov     ebx, 10
    imul    eax, ebx
    mov     [result], eax
    
    mov     eax, 1
    xor     ebx, ebx
    int     0x80
```
```nasm
section .data
    var1    dd  10
    var2    dd  20
    var3    dd  30
    var4    dd  40
    
section .bss
    result  resd 1
    
section .text
    global _start
    
_start:
    mov     eax, [var1]
    add     eax, [var2]
    add     eax, [var3]
    add     eax, [var4]
    mov     [result], eax
    
    mov     eax, 1
    xor     ebx, ebx
    int     0x80


```

```nasm
section .data
    var1    dd  4
    var2    dd  3
    var3    dd  15
    
section .bss
    result  resd 1
    
section .text
    global _start
    
_start:
    mov     eax, [var1]
    neg     eax
    mov     ebx, [var2]
    imul    eax, ebx
    add     eax, [var3]
    mov     [result], eax
    
    mov     eax, 1
    xor     ebx, ebx
    int     0x80****


```

```nasm
section .data
    var1    dd  12
    var2    dd  7
    
section .bss
    result  resd 1
    
section .text
    global _start
    
_start:
    mov     eax, [var1]
    shl     eax, 1
    
    mov     ebx, [var2]
    sub     ebx, 3
    
    cdq
    idiv    ebx
    mov     [result], eax
    
    mov     eax, 1
    xor     ebx, ebx
    int     0x80

```

