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

## License

This project is licensed under the [MIT License](https://github.com/yourusername/repo/blob/main/LICENSE).
```

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
