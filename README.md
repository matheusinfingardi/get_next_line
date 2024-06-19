# 🟦: get_next_line

## **General Description**

*The get_next_line project from the 42 School aims to implement a function in C that reads a single line from a file each time it is called, efficiently handling file I/O operations. The function should be capable of handling varying buffer sizes and managing memory properly. This project helps in understanding file manipulation and efficient memory management in C.*

## **Project Objective**

You need to implement the function get_next_line with the following prototype: </br>
``` c
char *get_next_line(int fd);
```
### **Parameter:**

   fd: The file descriptor from which to read the line.

### **Return Value:**

    The line read from the file, including the terminating newline character \n (unless it's the end of the file without a newline).
    NULL if there is nothing more to read or if an error occurred.

### **Expected Behavior:**

    The function should allow reading a file line by line with successive calls.
    It should work both for regular files and for the standard input (stdin).
