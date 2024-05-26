in the name of GOD
question 2
Amirhossein karami 
/Mahdi mohammadi 
golnaz jalvandi
1. addi a0, x0, 64: Load the input value (64 in this case) into the a0 register.
2. li t0, 1: Initialize the guess (t0) to 1.
3. loop: Start of the loop.
4. mul t2, t0, t0: Calculate the square of the current guess and store it in t2.
5. bge t2, a0, end_loop: If the square of the guess (t2) is greater than or equal to the input value (a0), exit the loop.
6. addi t0, t0, 1: Increment the guess by 1.
7. j loop: Jump back to the start of the loop.
8. end_loop: End of the loop.
9. sub a0, t0, x0: Store the final guess (integer square root) in a0.
10. ebreak: Exit the program.

## Note

This program uses a simple iterative approach and may not be the most efficient way to calculate the integer square root. More advanced algorithms, such as Newton's method or binary search, can be used for faster and more accurate calculations.

## Contributing

Contributions are welcome! Please feel free to open an issue or submit a pull request.

This README includes:

- A brief description of the program
- Usage instructions
- Detailed code explanation with line-by-line comments
- A note about the algorithm's efficiency
- A contributing section
- A license badge and link to the license file

The styling includes:

- Header formatting with different heading levels
- Code block formatting with syntax highlighting
- A license badge from Shields.io
- Links to the license file and contributing guidelines

Feel free to customize the content and styling according to your needs. Make sure to replace yourusername/repo with your actual GitHub username and repository name
https://raw.githubusercontent.com/mahdimmd81/phoeniX_test/main/image1.png
https://raw.githubusercontent.com/mahdimmd81/phoeniX_test/main/image2.png
https://raw.githubusercontent.com/mahdimmd81/phoeniX_test/main/image3.png
https://raw.githubusercontent.com/mahdimmd81/phoeniX_test/main/image4.png

question 1

# Quicksort Algorithm in RISC-V Assembly

# MAIN
addi sp, sp, 1000      # Allocate space on the stack
addi a0, x0, 0          # Set array base address

# Initialize array with values {10, 80, 30, 90, 40, 50, 70}
addi t0, x0, 10         # Initialize t0 with value 10
sw t0, 0(a0)            # Store t0 at array[0]
addi t0, x0, 80         # Initialize t0 with value 80
sw t0, 4(a0)            # Store t0 at array[1]
addi t0, x0, 30         # Initialize t0 with value 30
sw t0, 8(a0)            # Store t0 at array[2]
addi t0, x0, 90         # Initialize t0 with value 90
sw t0, 12(a0)           # Store t0 at array[3]
addi t0, x0, 40         # Initialize t0 with value 40
sw t0, 16(a0)           # Store t0 at array[4]
addi t0, x0, 50         # Initialize t0 with value 50
sw t0, 20(a0)           # Store t0 at array[5]
addi t0, x0, 70         # Initialize t0 with value 70
sw t0, 24(a0)           # Store t0 at array[6]

addi a1, x0, 0          # Set start index
addi a2, x0, 6          # Set end index

# Call the Quicksort function
jal ra, QUICKSORT

# Exit program
jal ra, EXIT

# Quicksort Algorithm
QUICKSORT:
addi sp, sp, -20        # Allocate space on the stack for saving registers
sw ra, 16(sp)           # Save return address
sw s3, 12(sp)           # Save s3 register
sw s2, 8(sp)            # Save s2 register
sw s1, 4(sp)            # Save s1 register
sw s0, 0(sp)            # Save s0 register

addi s0, a0, 0          # Set s0 to array base address
addi s1, a1, 0          # Set s1 to start index
addi s2, a2, 0          # Set s2 to end index
blt a2, a1, START_GT_END  # If end index is less than start index, exit

jal ra, PARTITION       # Call the PARTITION function
addi s3, a0, 0          # Set s3 to partition index

addi a0, s0, 0          # Set a0 to array base address
addi a1, s1, 0          # Set a1 to start index
addi a2, s3, -1         # Set a2 to partition index - 1
jal ra, QUICKSORT       # Recursively call QUICKSORT for left partition

addi a0, s0, 0          # Set a0 to array base address
addi a1, s3, 1          # Set a1 to partition index + 1
addi a2, s2, 0          # Set a2 to end index
jal ra, QUICKSORT       # Recursively call QUICKSORT for right partition

START_GT_END:
lw s0, 0(sp)            # Restore s0 register
lw s1, 4(sp)            # Restore s1 register
lw s2, 8(sp)            # Restore s2 register
lw s3, 12(sp)           # Restore s3 register
lw ra, 16(sp)           # Restore return address
addi sp, sp, 20         # Deallocate space on the stack
jalr x0, ra, 0          # Return from function

# Partition Function
PARTITION:
addi sp, sp, -4         # Allocate space on the stack for saving return address
sw ra, 0(sp)            # Save return address

slli t0, a2, 2          # Multiply end index by size of integer (4 bytes)
add t0, t0, a0          # Calculate memory address of pivot element
lw t0, 0(t0)            # Load pivot value

addi t1, a1, -1         # Initialize i to start index - 1
addi t2, a1, 0          # Initialize j to start index

LOOP:
beq t2, a2, LOOP_DONE   # Exit loop if j >= end index

slli t3, t2, 2          # Multiply j by size of integer (4 bytes)
add a6, t3, a0          # Calculate memory address of current element (arr + j)
lw t3, 0(a6)            # Load current element value

addi t0, t0, 1          # Increment pivot value
blt t0, t3, CURR_ELEMENT_GTE_PIVOT  # If (pivot <= current element), skip swap
addi t1, t1, 1          # Increment i

slli t5, t1, 2          # Multiply i by size of integer (4 bytes)
add a7, t5, a0          # Calculate memory address of element to swap with current element
lw t5, 0(a7)            # Load value to swap
sw t5, 0(a6)            # Store swapped value at current element's memory address
sw t3, 0(a7)            # Store current element's value at swap destination

CURR_ELEMENT_GTE_PIVOT:
addi t2, t2, 1          # Increment j
j LOOP

LOOP_DONE:
addi t5, t1, 1          # Increment i
addi a5, t5, 0          # Save return value (partition index)
slli t5, t5, 2          # Multiply (i + 1) by size of integer (4 bytes)
add a7, t5, a0          # Calculate memory address of (i + 1) element
lw t5, 0(a7)            # Load value to swap with last element

slli t3, a2, 2          # Multiply end index by size of integer (4 bytes)
add a6, t3, a0          # Calculate memory address of last element
lw t3, 0(a6)            # Load value of last element

sw t5, 0(a6)            # Store last element's value at (i + 1) position
sw t3, 0(a7)            # Store (i + 1

https://raw.githubusercontent.com/mahdimmd81/phoeniX_test/main/image21.png
https://raw.githubusercontent.com/mahdimmd81/phoeniX_test/main/image22.png
https://raw.githubusercontent.com/mahdimmd81/phoeniX_test/main/image23.png