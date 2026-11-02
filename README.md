# Linux-File-IO-Systems-locking
Ex07-Linux File-IO Systems-locking
# AIM:
To Write a C program that illustrates files copying and locking

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux IO Systems locking

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## 1.To Write a C program that illustrates files copying 
~~~

#include <unistd.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdlib.h>
#include <stdio.h>

int main(int argc, char *argv[])
{
    if (argc != 3)
    {
        printf("Usage: %s source destination\n", argv[0]);
        return 1;
    }

    char block[1024];
    int in, out;
    ssize_t nread;

    in = open(argv[1], O_RDONLY);
    if (in == -1)
    {
        perror("Source file error");
        return 1;
    }

    out = open(argv[2], O_WRONLY | O_CREAT | O_TRUNC,
               S_IRUSR | S_IWUSR);

    if (out == -1)
    {
        perror("Destination file error");
        close(in);
        return 1;
    }

    while ((nread = read(in, block, sizeof(block))) > 0)
    {
        if (write(out, block, nread) != nread)
        {
            perror("Write error");
            return 1;
        }
    }

    close(in);
    close(out);

    printf("File copied successfully!\n");
    return 0;
}

~~~






## 2.To Write a C program that illustrates files locking
~~~

#include <unistd.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdlib.h>
#include <stdio.h>

int main(int argc, char *argv[])
{
    if (argc != 3)
    {
        printf("Usage: %s source destination\n", argv[0]);
        return 1;
    }

    char block[1024];
    int in, out;
    ssize_t nread;

    in = open(argv[1], O_RDONLY);
    if (in == -1)
    {
        perror("Source file error");
        return 1;
    }

    out = open(argv[2], O_WRONLY | O_CREAT | O_TRUNC,
               S_IRUSR | S_IWUSR);

    if (out == -1)
    {
        perror("Destination file error");
        close(in);
        return 1;
    }

    while ((nread = read(in, block, sizeof(block))) > 0)
    {
        if (write(out, block, nread) != nread)
        {
            perror("Write error");
            return 1;
        }
    }

    close(in);
    close(out);

    printf("File copied successfully!\n");
    return 0;
}

~~~



## OUTPUT
<img width="927" height="881" alt="image" src="https://github.com/user-attachments/assets/4caa57bf-973c-4179-ae3b-bfe761bc3b54" />





# RESULT:
The programs are executed successfully.
