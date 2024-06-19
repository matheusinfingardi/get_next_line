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
The get_next_line function must be organized into the following files:

- **get_next_line.c:**
The main implementation of the get_next_line function. </br>
- **get_next_line_utils.c:**
Auxiliary functions that support the main implementation. </br>
- **get_next_line.h:**
Declarations and prototypes required for the get_next_line function. </br>

Expected behavior for get_next_line includes:
- Continuous reading from a file until all lines are processed.
- Returning the line read, including the \n character, except at the end of the file.
- Efficient memory management to ensure no leaks.
- Functioning with different BUFFER_SIZE values, from very small to very large, and handling buffer size changes dynamically.

## **Bonus Part:**
**Single Static Variable:**
Implement get_next_line using only one static variable.

**Support Multiple File Descriptors:**
The function should handle reading from multiple file descriptors simultaneously without confusing their reading positions.
For example, it should be able to read from fd 3, then fd 4, then fd 3 again without losing the reading position in any file descriptor.

For the bonus part, create additional files:
- **get_next_line_bonus.c:** The implementation of get_next_line with support for multiple file descriptors and using a static variable. </br>
- **get_next_line_bonus.h:** Declarations and prototypes specific to the bonus part. </br>
- **get_next_line_utils_bonus.c:** Auxiliary functions specific to the bonus part. </br>

## **Detailed Explanation**
### **Main Function (get_next_line):**
**Objective:** Manage reading lines from the file described by fd.</br>
**Process:** Detailed breakdown of how it reads in parts and constructs the final line to be returned.</br>
### **Auxiliary Functions:**
**Objective:** Facilitate operations such as buffer manipulation, copying, and character searching.</br>
**Process:** Explanation of each auxiliary function, its specific role, and how it integrates with the main function.
### **File Structure:**
- **get_next_line.c:** Contains the core logic for reading lines.
- **get_next_line_utils.c:** Provides supporting utilities.
- **get_next_line.h:** Defines the prototype of the function and any necessary headers.


# get_next_line.h
