Challenges in Performing the Lab
File Descriptor Management: Tracking the file descriptor between create and append operations required careful handling to avoid file access errors.
File Opening Modes: Understanding the octal values for file permissions (0666) and open flags (O_CREAT|O_WRONLY = 0102, O_WRONLY|O_APPEND = 02002) 
String Length Calculation: Using the $ - "label technique to calculate string lengths at assembly time rather than hardcoding values."



```nasm
section .text
    global _start

_start:
    mov ecx, 0711o
    mov ebx, filename
    mov eax, 8
    int 0x80
    
    mov [fd_out], eax
    
    mov eax, 4
    mov ebx, [fd_out]
    mov ecx, content1
    mov edx, 44
    int 0x80
    
    mov eax, 4
    mov ebx, [fd_out]
    mov ecx, content2
    mov edx, 78
    int 0x80
    
    mov eax, 6
    mov ebx, [fd_out]
    int 0x80
    
    mov eax, 5
    mov ebx, filename
    mov ecx, 2
    mov edx, 0777o
    int 0x80
    
    mov [fd_out], eax
    
    mov eax, 19
    mov ebx, [fd_out]
    mov ecx, 0
    mov edx, 2
    int 0x80
    
    mov eax, 4
    mov ebx, [fd_out]
    mov ecx, content3
    mov edx, 53
    int 0x80
    
    mov eax, 4
    mov ebx, [fd_out]
    mov ecx, content4
    mov edx, 34
    int 0x80
    
    mov eax, 6
    mov ebx, [fd_out]
    int 0x80
    
    mov eax, 1
    int 0x80

section .data
    filename db 'quotes.txt', 0h
    content1 db 'To be, or not to be, that is the question.', 0xa
    content2 db 'A fool thinks himself to be wise, but a wise man knows himself to be a fool.', 0xa
    content3 db 'Better three hours too soon than a minute too late.', 0xa
    content4 db 'No legacy is so rich as honesty.', 0xa

section .bss
    fd_out resb 1
