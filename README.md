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
_This is the header file for the get_next_line project. It contains the function prototypes, necessary includes, and macros used across the implementation files. Below is a detailed breakdown of its components._

``` c
#ifndef GET_NEXT_LINE_H
# define GET_NEXT_LINE_H
```
- **Guard Clause:** This #ifndef ... #define ... #endif pattern is a header guard. It prevents the file from being included multiple times in a single compilation unit, which can cause redefinition errors. If GET_NEXT_LINE_H is not defined, it defines it and includes the content between #define and #endif. If it’s already defined, the file is skipped.

``` c
# include <stdlib.h>
# include <unistd.h>
# include <stddef.h>
# include <sys/types.h>
# include <fcntl.h>
```

- **<stdlib.h>:** Provides functions malloc and free. </br>
- **<unistd.h>:** Includes function read. </br>
- **<stddef.h>:** Defines types and macros like size_t used for memory and array operations.</br>
- **<sys/types.h>:** Defines data types used in system calls.</br>
- **<fcntl.h>:** Provides file control options, like O_RDONLY for opening files in read-only mode.</br>

## Function Prototypes
- **get_next_line Function:** This is the main function of the project. It reads and returns the next line from the file descriptor _fd_.
``` c
char	*get_next_line(int fd);
```
- **ft_strlen Function:** Computes and returns the length of the string _str_.
```c
size_t	ft_strlen(char *str);
```
- **ft_strchr Function:** Searches for the first occurrence of the character _c_ in the string _str_ and returns a pointer to this character within the string.
```c
char	*ft_strchr(char *str, int c);
```
- **ft_strjoin Function:** Allocates memory and concatenates two strings, _s1_ and _s2_, returning a new string that is the result of this concatenation.
```c
char	*ft_strjoin(char *s1, char *s2);
```
- **ft_line_allocation Function:** Reads from the file descriptor _fd_ into a buffer and appends it to _str_, handling the memory allocation. This function likely supports get_next_line by handling the data reading part.
```c
char	*ft_line_allocation(int fd, char *str);
```
- **ft_next_line Function:** Processes the buffer _str_ to identify and return the next line, including managing the remaining buffer after extracting the line.
```c
char	*ft_next_line(char *str);
```
- **ft_rem_line Function:** Handles the memory management for the remaining part of the buffer after the current line has been extracted.
```c
char	*ft_rem_line(char *line);
```
### Overview of Source Files
**get_next_line.c** </br>
This file will contain the main logic for the get_next_line function. It coordinates reading from the file descriptor, managing the buffer, and returning each line one at a time. The functions defined here are responsible for handling the core task of reading and returning lines. </br>
</br>
**get_next_line_utils.c** </br>
This file provides auxiliary functions that support the main get_next_line function. These typically include utility functions for string manipulation and buffer handling, such as calculating the length of a string _(ft_strlen)_, searching for a character in a string _(ft_strchr)_, joining two strings _(ft_strjoin)_, and managing the buffer _(ft_line_allocation, ft_next_line, ft_rem_line)_.

### How they work together
- **Reading and Buffer Management:** _get_next_line_ uses _ft_line_allocation_ to read chunks from the file into a buffer. It manages how much data has been read and when to stop.
- **String Processing:** Functions like _ft_strlen_, _ft_strchr_, and _ft_strjoin_ are used to manipulate the buffer and manage the lines extracted from the file.
- **Memory Management:** Proper memory allocation and deallocation are crucial to avoid leaks. Functions like _ft_rem_line_ handle the cleanup of unused buffer parts.

# get_next_line.c
This file contains the main _get_next_line_ function and one utility function, _ft_strlen_. </br>
Below is a detailed explanation of each function and their roles in the get_next_line project.</br>
</br>
## ft_strlen
```c
size_t	ft_strlen(char *str)
{
	size_t	i;

	i = 0;
	if (!str)
		return (0);
	while (str[i])
		i++;
	return (i);
}
```
### Purpose
Reads the next line from a file descriptor fd and returns it as a string.
### Parameters
**int fd:** The file descriptor from which to read the line.
### Return Value
A string containing the next line from the file, including the terminating newline character _\n_, if present.
Returns _NULL_ if there is nothing more to read or if an error occurred.
### How it works
- The function initializes a counter i to 0.
- It checks if the input string str is NULL. If it is, it returns 0, indicating that there is no string to process.
- It then enters a while loop that increments the counter i until it reaches the end of the string (the null byte \0).
- Finally, it returns the value of i, which is the length of the string.

### Use in get_next_line
This function is used to determine the length of strings throughout the implementation, which is essential for various buffer and string operations

## get_next_line.c
``` c
char	*get_next_line(int fd)
{
	char	*out;
	static char	*str;
	
	if (BUFFER_SIZE <= 0 || fd < 0)
		return (NULL);
	str = ft_line_allocation(fd, str);
	if (!str)
		return (NULL);
	out = ft_next_line(str);
	str = ft_rem_line(str);
	return (out);
}
```

### Purpose
Reads the next line from a file descriptor fd and returns it as a string.
### Parameters
- **int fd:** The file descriptor from which to read the line.
### Return Value
A string containing the next line from the file, including the terminating newline character \n, if present.
Returns NULL if there is nothing more to read or if an error occurred.

### How it works
- **Static Variable Initialization:** </br>
The function uses a static char *str to maintain a buffer between successive calls. This static variable holds any remaining data that was not yet returned as a complete line.
</br>  </br>
- **Validation:** </br>
The function first checks if BUFFER_SIZE is valid (greater than 0) and if the file descriptor fd is non-negative. If either condition is not met, it returns NULL.
</br>  </br>
- **Reading from File Descriptor:** </br>
It calls ft_line_allocation(fd, str), which reads data from the file descriptor and appends it to the existing str buffer. This function is responsible for handling the actual reading and buffer management.
</br>  </br>
- **Check for read data:** </br>
If ft_line_allocation returns NULL, meaning no data was read or an error occurred, get_next_line returns NULL.
</br>  </br>
- **Extracting the Next Line:** </br>
It then calls ft_next_line(str), which processes the buffer to extract the next complete line. This function returns the next line to be output by get_next_line.
</br>  </br>
- **Managing the Buffer:** </br>
After extracting the line, it updates str by calling ft_rem_line(str). This function adjusts the buffer to remove the part that has been returned and keep any remaining data for the next call.
</br>  </br>
- **Returning the Line:** </br>
Finally, the function returns the extracted line (out).
</br>
### Use in get_next_line
This function is the core of the get_next_line project. It manages the process of reading from a file descriptor and returning one line at a time. By using a static variable, it maintains state across multiple calls, allowing it to continue reading from where it left off.
</br>

## Overview and Interaction with Other Functions

### File Structure
- **get_next_line.c:** Contains the main logic of reading and returning lines using the get_next_line function.
- **get_next_line_utils.c:** Include helper functions like ft_line_allocation, ft_next_line, and ft_rem_line.
### Function Interaction
- **ft_line_allocation:** Reads and appends data to the static buffer. This function interacts with read and handles memory allocation and management. </br>
- **ft_next_line:** Processes the buffer to extract the next complete line, including handling newline characters.
- **ft_rem_line:** Adjusts the buffer to retain any remaining data after a line has been extracted, ensuring the static buffer can continue from where it left off.
