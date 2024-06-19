# 🌀 get_next_line

## **General Description**

*The get_next_line project from the 42 School aims to implement a function in C that reads a single line from a file each time it is called, efficiently handling file I/O operations. The function should be capable of handling varying buffer sizes and managing memory properly. This project helps in understanding file manipulation and efficient memory management in C.*

## **Project Objective**

Implement the function get_next_line with the following prototype: </br>
``` c
char *get_next_line(int fd);
```
 **Parameter:**

- **fd:** The file descriptor from which to read the line.

 **Return Value:**
- The line read from the file, including the terminating newline character \n (unless it's the end of the file without a newline).
- NULL if there is nothing more to read or if an error occurred.
 **Expected Behavior:**
- The function should allow reading a file line by line with successive calls.
- It should work both for regular files and for the standard input (stdin).
## **Common Instructions**
To meet the requirements of the 42 School, the project must adhere to specific rules and restrictions:

 **Norm Compliance:** </br>
The code must conform to the 42 Norm, which includes coding style, function usage, and code organization.
All bonus files must also follow the Norm.

  **Stability and Safety:** </br>
The function should not fail unexpectedly (e.g., segmentation faults, bus errors, double frees).
All dynamically allocated memory must be properly freed, with no memory leaks.

  **Compilation:** </br>
Must use cc and the flags -Wall -Wextra -Werror.
The project must compile with various BUFFER_SIZE values defined using -D BUFFER_SIZE=n.

  **Allowed Functions:** </br>
The only allowed external functions are read, malloc, and free.

  **No Globals or libft:** </br>
Global variables are not allowed.
Can not use libft in this project.

## **Mandatory Part:**
_The get_next_line function must be organized into the following files:_

- **get_next_line.c:**
The main implementation of the get_next_line function. </br>
- **get_next_line_utils.c:**
Auxiliary functions that support the main implementation. </br>
- **get_next_line.h:**
Declarations and prototypes required for the get_next_line function. </br>

_Expected behavior for get_next_line includes:_
- Continuous reading from a file until all lines are processed.
- Returning the line read, including the \n character, except at the end of the file.
- Efficient memory management to ensure no leaks.
- Functioning with different BUFFER_SIZE values, from very small to very large, and handling buffer size changes dynamically.
