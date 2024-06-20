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
- NULL if there is nothing more to read or if an error occurred. </br>

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

## get_next_line_utils.c
This file contains several utility functions that support the main get_next_line function. Each function plays a crucial role in handling string operations, memory allocation, and buffer management.
</br>
### ft_strchr
``` c
char	*ft_strchr(char *str, int c)
{
	size_t	i;
	
	i = 0;
	if (!str)
		return (0);
	if (c == '\0')
		return ((char *)&str[ft_strlen(str)]);
	while (str[i])
	{
		if (str[i] == (char) c)
			return ((char *)&str[i]);
		i++;
	}
	return (0);
}
```
### Purpose
Searches for the first occurrence of the character c in the string str.
### Parameters
**char *str:*** The string to be searched. </br>
**int c:** The character to be found in str.
### Return Value
Returns a pointer to the first occurrence of c in str. </br>
If c is \0 (null terminator), it returns a pointer to the end of str (pointing to the null terminator). </br>
Returns NULL if str is NULL or if c is not found in str. </br>
### How it works
- Initializes a counter i to 0.
- Checks if str is NULL. If it is, returns NULL.
- If c is \0, returns a pointer to the end of str using ft_strlen(str).
- Iterates through str using a while loop to search for c.
- Returns a pointer to the first occurrence of c when found.
### Use in get_next_line
Used in ft_line_allocation to check for the presence of a newline character (\n) in the current buffer str, indicating the end of a line.

### ft_strjoin
``` c
char	*ft_strjoin(char *s1, char *s2)
{
	size_t	i;
	size_t	j;
	char	*out;

	if (!s1)
	{
		s1 = (char *)malloc(sizeof(char) * 1);
		s1[0] = '\0';
	}
	if (!s2)
		return (NULL);
	out = (char *)malloc(sizeof(char) * (ft_strlen(s1) + ft_strlen(s2) + 1));
	if (out == NULL)
		return (NULL);
	i = 0;
	j = 0;
	while (s1[i])
		out[j++] = s1[i++];
	i = 0;
	while (s2[i])
		out[j++] = s2[i++];
	out[j] = '\0';
	free(s1);
	return (out);
}
```
### Purpose
Concatenates two strings s1 and s2 and returns a new string.
### Parameters
**char *s1:*** The first string to concatenate. </br>
**char *s2:*** The second string to concatenate.
### Return Value
Returns a newly allocated string that is the concatenation of s1 and s2. </br>
Returns NULL if memory allocation fails or if s2 is NULL.
### How it works
- Handles cases where s1 might be NULL by allocating a minimal string.
- Allocates memory for the resulting string out based on the combined lengths of s1 and s2, plus one for the null terminator.
- Copies characters from s1 and s2 into out using while loops until the null terminators are encountered.
- Frees the memory allocated for s1 since its contents have been copied into out.
### Use in get_next_line
Used in ft_line_allocation to append data read from the file descriptor (buff) to the existing buffer (str), extending str dynamically as needed.

### ft_line_allocation
``` c
char	*ft_line_allocation(int fd, char *str)
{
	char	*buff;
	ssize_t	dim;

	buff = malloc(sizeof(char) * (BUFFER_SIZE + 1));
	if (!buff)
		return (NULL);
	dim = 1;
	while (!(ft_strchr(str, '\n')) && dim > 0)
	{
		dim = read(fd, buff, BUFFER_SIZE);
		if (dim == -1)
		{
			free(buff);
			return (NULL);
		}
		buff[dim] = '\0';
		str = ft_strjoin(str, buff);
	}
	free(buff);
	return (str);
}
```
### Purpose
Reads data from a file descriptor fd and appends it to the buffer str.
### Parameters
**int fd:** The file descriptor from which to read data.
**char *str:*** The current buffer containing previously read data.
### Return Value
Returns an updated buffer str containing the appended data.
Returns NULL if an error occurs during reading or memory allocation fails.
### How it works
- Allocates a temporary buffer buff of size BUFFER_SIZE + 1.
- Reads data from fd into buff using the read function until either a newline character (\n) is found in str or the end of file (dim == 0).
- Checks for errors during reading (dim == -1) and returns NULL if an error occurs.
- Appends buff to str using ft_strjoin, extending str dynamically as needed.
- Frees buff after all data has been read and appended to str.
### Use in get_next_line
Used in get_next_line to read from fd and build up the buffer str with data from the file descriptor, ensuring it handles varying buffer sizes defined by BUFFER_SIZE.

### ft_next_line
``` c
char	*ft_next_line(char *str)
{
	char	*new;
	int	i;
	
	i = 0;
	if (str[i] == 0)
		return (NULL);
	while (str[i] && str[i] != '\n')
		i++;
	new = (char *)malloc(sizeof(char) * (i + 2));
	if (!new)
		return (NULL);
	i = 0;
	while (str[i] && str[i] != '\n')
	{
		new[i] = str[i];
		i++;
	}
	if (str[i] == '\n')
	{
		new[i] = '\n';
		i++;
	}
	new[i] = '\0';
	return (new);
}
```
### Purpose
Extracts the next complete line from the buffer str.
### Parameters
**char *str:*** The buffer containing data read from a file descriptor.
### Return Value
Returns a newly allocated string that contains the next complete line from str, including the terminating newline character \n.
Returns NULL if there are no complete lines left in str or if memory allocation fails.
### How it works
- Checks if str is empty (str[i] == 0). If so, returns NULL.
- Iterates through str until it finds either a newline character (\n) or reaches the end of str.
- Allocates memory for new to hold the extracted line plus the newline character (if present).
- Copies characters from str into new until it encounters \n or reaches the end of str.
- If \n is found, copies it to new.
- Terminates new with \0 and returns it as the next complete line.
### Use in get_next_line
Used in get_next_line to extract each complete line from the buffer str and return it as the output of get_next_line.

### ft_rem_line
``` c
char	*ft_rem_line(char *line)
{
	char	*str;
	int	i;
	int	j;

	i = 0;
	while (line[i] && line[i] != '\n')
	{
		i++;
	}
	if (!line[i])
	{
		free(line);
		return (NULL);
	}
	str = (char *)malloc(sizeof(char) * (ft_strlen(line) - i + 1));
	if (!str)
		return (NULL);
	i++;
	j = 0;
	while (line[i])
		str[j++] = line[i++];
	str[j] = '\0';
	free(line);
	return (str);
}
```
### Purpose
Adjusts the buffer line to remove the current line that has been read and return the remaining data.
### Parameters
**char *line:*** The buffer containing data read from a file descriptor.
### Return Value
Returns an updated buffer str containing the remaining data after removing the current line.
Returns NULL if all lines have been read or if memory allocation fails.
Returns NULL if there are no complete lines left in str or if memory allocation fails.
### How it works
- Finds the position of the newline character (\n) in line using a while loop.
- If no newline character is found (!line[i]), frees line and returns NULL.
- Allocates memory for str to hold the remaining data in line after the newline character.
- Copies remaining characters from line into str starting from the position after the newline character.
- Frees line after copying and returns str as the updated


# Overview get_next_line_bonus.c
This file contains the implementation of the get_next_line function for the bonus part, which supports reading from multiple file descriptors (fd). It uses a static array str to maintain the buffer for each file descriptor separately.

## get_next_line (bonus)
``` c
char	*get_next_line(int fd)
{
	char	*out;
	static char	*str[4096];

	if (BUFFER_SIZE <= 0 || fd < 0)
		return (NULL);
	str[fd] = ft_line_allocation(fd, str[fd]);
	if (!str[fd])
		return (NULL);
	out = ft_next_line(str[fd]);
	str[fd] = ft_rem_line(str[fd]);
	return (out);
}
```
### Purpose
Reads and returns the next line from the file descriptor fd.
### Parameters
**int fd:** The file descriptor from which to read.
### Return Value
Returns a string containing the next line read from fd, including the newline character \n.
Returns NULL if there are no more lines to read or if an error occurs.
### How it works
- Checks if BUFFER_SIZE is valid (> 0) and if fd is valid (>= 0).
- Uses a static array str to store the buffer for each file descriptor fd. This allows get_next_line to handle - multiple file descriptors simultaneously.
- Calls ft_line_allocation to read from fd and append data to str[fd].
- If ft_line_allocation fails (returns NULL), returns NULL.
- Calls ft_next_line to extract and return the next complete line from str[fd].
- Calls ft_rem_line to remove the returned line from str[fd] and update str[fd] with the remaining data.
- Returns the extracted line out
### Use in get_next_line
get_next_line_bonus operates similarly to get_next_line, but it manages multiple file descriptors by storing each buffer str[fd] separately.

# Questions and Answer (Q&A)
## get_next_line.c
### Q1- Static Variables and how it works in get_next_line
``` c
static char	*str;
```
In the context of the get_next_line function, the static variable static char *str plays a crucial role in maintaining the state between successive calls to the function. Here’s how it works:
- **Purpose:** The static variable str is used to store the leftover or remaining data from previous reads that haven’t been fully processed into lines yet.
- **Memory Persistense:** Unlike local variables, which are created and destroyed each time a function is called, static variables retain their values between function calls. This means str retains the last state across multiple invocations of get_next_line.
- **Usage:**
	- Initially, str is NULL before the first call to get_next_line.
	- When get_next_line is called, it reads from the file descriptor (fd) and appends data to str.
	- Subsequent calls to get_next_line continue reading from where the previous call left off, utilizing str to store and manage the buffer of data.
- **Important Considerations:**
	- Static variables are shared across all instances of a function, so changes made to str in one call persist and affect subsequent calls.
	- Careful management is required to ensure str is properly updated and freed when no longer needed, especially to avoid memory leaks.

### Q2- Why does get_next_line return NULL if !str?
``` c
	if (!str)
		return (NULL);
``
The condition if (!str) in the get_next_line function is crucial for error handling and indicating the end of file or failure to read a line. Here’s why it returns NULL:
After calling ft_line_allocation, get_next_line checks if str is NULL (if (!str)).
If str is NULL, it means:
- There was an error during the allocation or reading process.
- There are no more lines left to read from the file descriptor.

In such cases, returning NULL from get_next_line signals to the caller that no line could be read or that an error occurred.

# Conclusion
These functions collectively provide the core functionality needed for the get_next_line project. They ensure efficient handling of file I/O operations, dynamic memory allocation, and proper management of buffers to read and return lines from file descriptors. Understanding these functions and their interactions is crucial for implementing the project successfully and adhering to the requirements specified by the 42 School.
