![ Flowchart](<Screenshot 2025-07-23 210028.png>)
```nasm

# MIDTERM.asm - Fixed Assembly Programming Solutions
#Jackson Cao
#==============================================================================
# TASK 1: Equation Calculator - result = (var1 + 2) / (var3 - var2)
#==============================================================================
# Variable values:
# var1 = 10
# var2 = 3  
# var3 = 8
# Calculation: result = (10 + 2) / (8 - 3) = 12 / 5 = 2 remainder 2
# Quotient stored in EAX = 2
# Remainder stored in EDX = 2

.section .data
    # Task 1 Variables
    var1: .long 10          # First variable
    var2: .long 3           # Second variable  
    var3: .long 8           # Third variable
    result: .long 0         # Result storage
    
    # Task 3 Variables
    test_number: .long 17   # Number to test for odd/even
    
    # Display Messages
    task1_msg: .ascii "TASK 1 - Equation Calculator\n"
    task1_msg_len = . - task1_msg
    
    result_msg: .ascii "Result: "
    result_msg_len = . - result_msg
    
    quotient_msg: .ascii "Quotient (EAX): "
    quotient_msg_len = . - quotient_msg
    
    remainder_msg: .ascii "Remainder (EDX): "
    remainder_msg_len = . - remainder_msg
    
    task3_msg: .ascii "\nTASK 3 - Odd/Even Detector\n"
    task3_msg_len = . - task3_msg
    
    testing_msg: .ascii "Testing number: "
    testing_msg_len = . - testing_msg
    
    even_msg: .ascii "even number\n"
    even_msg_len = . - even_msg
    
    odd_msg: .ascii "odd number\n"  
    odd_msg_len = . - odd_msg
    
    newline: .ascii "\n"

.section .bss
    buffer: .space 12

.section .text
.globl _start

_start:
    #==========================================================================
    # TASK 1: EQUATION CALCULATION
    #==========================================================================
    
    # Display Task 1 header
    movl $4, %eax           # sys_write system call
    movl $1, %ebx           # stdout file descriptor
    movl $task1_msg, %ecx   # message address
    movl $task1_msg_len, %edx # message length
    int $0x80               # system call
    
    # Calculate numerator: var1 + 2
    movl var1, %eax         # Load var1 (10) into EAX
    addl $2, %eax           # Add 2: EAX = 10 + 2 = 12
    movl %eax, %ebx         # Store numerator (12) in EBX
    
    # Calculate denominator: var3 - var2  
    movl var3, %eax         # Load var3 (8) into EAX
    subl var2, %eax         # Subtract var2 (3): EAX = 8 - 3 = 5
    movl %eax, %ecx         # Store denominator (5) in ECX
    
    # Perform division: numerator / denominator
    movl %ebx, %eax         # Move numerator (12) to EAX
    movl $0, %edx           # Clear EDX for division
    idivl %ecx              # Divide EAX by ECX (12 ÷ 5)
                           # Quotient (2) in EAX, Remainder (2) in EDX
    
    # Store result (quotient)
    movl %eax, result       # Store quotient in result variable
    
    # At this point: EAX=2 (quotient), EDX=2 (remainder)
    # This is where you should set your GDB breakpoint
    
    # Display "Result: "
    pushl %edx              # Save remainder
    pushl %eax              # Save quotient
    
    movl $4, %eax           # sys_write
    movl $1, %ebx           # stdout
    movl $result_msg, %ecx  # message
    movl $result_msg_len, %edx # length
    int $0x80
    
    # Display result value
    popl %eax               # Restore quotient
    call print_number
    
    # Print newline
    movl $4, %eax
    movl $1, %ebx
    movl $newline, %ecx
    movl $1, %edx
    int $0x80
    
    # Display "Quotient (EAX): "
    movl $4, %eax
    movl $1, %ebx
    movl $quotient_msg, %ecx
    movl $quotient_msg_len, %edx
    int $0x80
    
    # Display quotient value (already in result)
    movl result, %eax
    call print_number
    
    # Print newline
    movl $4, %eax
    movl $1, %ebx
    movl $newline, %ecx
    movl $1, %edx
    int $0x80
    
    # Display "Remainder (EDX): "
    movl $4, %eax
    movl $1, %ebx
    movl $remainder_msg, %ecx
    movl $remainder_msg_len, %edx
    int $0x80
    
    # Display remainder value (saved on stack)
    popl %eax               # Get remainder from stack
    call print_number
    
    # Print newline
    movl $4, %eax
    movl $1, %ebx
    movl $newline, %ecx
    movl $1, %edx
    int $0x80
    
    #==========================================================================
    # TASK 3: ODD/EVEN NUMBER DETECTION (WITHOUT AND/OR)
    #==========================================================================
    
    # Display Task 3 header
    movl $4, %eax
    movl $1, %ebx
    movl $task3_msg, %ecx
    movl $task3_msg_len, %edx
    int $0x80
    
    # Display "Testing number: "
    movl $4, %eax
    movl $1, %ebx
    movl $testing_msg, %ecx
    movl $testing_msg_len, %edx
    int $0x80
    
    # Display the test number
    movl test_number, %eax
    call print_number
    
    # Print newline
    movl $4, %eax
    movl $1, %ebx
    movl $newline, %ecx
    movl $1, %edx
    int $0x80
    
    # CORE LOGIC: Determine odd/even using division method
    movl test_number, %eax  # Load test number into EAX
    movl $0, %edx           # Clear EDX for division
    movl $2, %ebx           # Divisor = 2
    idivl %ebx              # Divide by 2
                           # Quotient in EAX, Remainder in EDX
    
    # Check remainder to determine odd/even
    cmpl $0, %edx           # Compare remainder with 0
    je display_even         # If remainder = 0, number is even
    jmp display_odd         # Otherwise, number is odd

display_even:
    movl $4, %eax           # sys_write
    movl $1, %ebx           # stdout
    movl $even_msg, %ecx    # "even number" message
    movl $even_msg_len, %edx
    int $0x80
    jmp exit_program

display_odd:
    movl $4, %eax           # sys_write
    movl $1, %ebx           # stdout
    movl $odd_msg, %ecx     # "odd number" message
    movl $odd_msg_len, %edx
    int $0x80

exit_program:
    # Exit program
    movl $1, %eax           # sys_exit
    movl $0, %ebx           # exit status
    int $0x80

#==============================================================================
# UTILITY FUNCTIONS
#==============================================================================

# Function to print a number in EAX
print_number:
    pushl %ebp
    movl %esp, %ebp
    pushl %ebx
    pushl %ecx
    pushl %edx
    pushl %edi
    pushl %esi
    
    movl %eax, %esi         # Save original number
    
    # Handle zero case
    cmpl $0, %esi
    jne not_zero
    movl $4, %eax           # sys_write
    movl $1, %ebx           # stdout
    movl $48, %ecx          # ASCII '0'
    pushl %ecx
    movl %esp, %ecx         # Point to the '0' on stack
    movl $1, %edx           # Length 1
    int $0x80
    addl $4, %esp           # Remove from stack
    jmp print_done
    
not_zero:
    movl $buffer, %edi      # Point to buffer
    addl $11, %edi          # Point to end of buffer
    movb $0, (%edi)         # Null terminate
    movl $10, %ebx          # Base 10
    
convert_loop:
    decl %edi               # Move backward in buffer
    movl %esi, %eax         # Get number
    movl $0, %edx           # Clear EDX
    idivl %ebx              # Divide by 10
    movl %eax, %esi         # Save quotient
    addl $48, %edx          # Convert remainder to ASCII
    movb %dl, (%edi)        # Store digit
    cmpl $0, %esi           # Check if quotient is 0
    jne convert_loop        # Continue if not zero
    
    # Calculate length and print
    movl $buffer, %eax
    addl $11, %eax
    subl %edi, %eax         # Length = end - start
    
    movl $4, %eax           # sys_write
    movl $1, %ebx           # stdout
    movl %edi, %ecx         # string start
    movl %eax, %edx         # string length
    int $0x80
    
print_done:
    popl %esi
    popl %edi
    popl %edx
    popl %ecx
    popl %ebx
    popl %ebp
    ret

#==============================================================================
# REGISTER USAGE TABLE FOR TASK 1:
#==============================================================================
# Register | Purpose                    | Final Value
#----------|----------------------------|-------------
# EAX      | Division quotient result   | 2
# EDX      | Division remainder result  | 2  
# EBX      | Temporary numerator storage| 12
# ECX      | Temporary denominator storage| 5
#==============================================================================
