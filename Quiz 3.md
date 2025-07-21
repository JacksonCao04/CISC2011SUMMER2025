.data
    number:     .quad   5
    result:     .quad   1
    buffer:     .space  20
    newline:    .byte   10

.text
.global _start

_start:
    ldr     x0, =number
    ldr     x1, [x0]
    mov     x2, #1
    
factorial_loop:
    cmp     x1, #1
    ble     factorial_done
    
    mul     x2, x2, x1
    sub     x1, x1, #1
    b       factorial_loop
    
factorial_done:
    ldr     x0, =result
    str     x2, [x0]
    
    mov     x0, x2
    ldr     x1, =buffer
    add     x1, x1, #19
    mov     w2, #0
    strb    w2, [x1]
    sub     x1, x1, #1
    
convert_loop:
    mov     x3, #10
    udiv    x4, x0, x3
    msub    x5, x4, x3, x0
    add     w5, w5, #'0'
    strb    w5, [x1]
    sub     x1, x1, #1
    mov     x0, x4
    cbnz    x0, convert_loop
    
    add     x1, x1, #1
    
    mov     x2, x1
    ldr     x3, =buffer
    add     x3, x3, #19
    sub     x2, x3, x2
    
    mov     x8, #64
    mov     x0, #1
    svc     #0
    
    mov     x8, #64
    mov     x0, #1
    ldr     x1, =newline
    mov     x2, #1
    svc     #0
    
    mov     x8, #93
    mov     x0, #0
    svc     #0
