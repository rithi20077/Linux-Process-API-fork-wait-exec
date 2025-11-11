# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls
```
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
#include <stdlib.h>

int main() {
    pid_t pid;

    printf("Parent Process: PID = %d\n", getpid());

    pid = fork(); // create child

    if (pid < 0) {
        perror("fork failed");
        return 1;
    } 
    else if (pid == 0) {
        // Child process
        printf("Child Process: PID = %d, Parent PID = %d\n", getpid(), getppid());
        printf("Child executing 'ls -l' command:\n\n");
        execl("/bin/ls", "ls", "-l", NULL); // child runs ls command
        perror("exec failed"); // only runs if execl fails
        exit(1);
    } 
    else {
        // Parent process
        wait(NULL); // wait for child to finish
        printf("\nParent Process Resumed: Child finished execution\n");
    }

    return 0;
}

```

##OUTPUT

<img width="770" height="406" alt="Screenshot from 2025-11-11 11-19-33" src="https://github.com/user-attachments/assets/063443be-25b5-48a4-ae50-7ae0c800c478" />

<img width="635" height="271" alt="Screenshot from 2025-11-11 11-23-02" src="https://github.com/user-attachments/assets/bfbab42f-8f48-426c-9a7b-41872f03f905" />






## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family

```
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
#include <stdlib.h>
#include <string.h>  // <--- Add this line

int main() {
    pid_t pid;
    char command[100];

    printf("Parent Process: PID = %d\n", getpid());

    // Ask user for command
    printf("Enter a Linux command for the child to execute (e.g., ls -l): ");
    fgets(command, sizeof(command), stdin);
    // Remove newline at end
    command[strcspn(command, "\n")] = 0;

    pid = fork(); // create child

    if (pid < 0) {
        perror("fork failed");
        exit(1);
    } 
    else if (pid == 0) {
        // Child process
        printf("Child Process: PID = %d, Parent PID = %d\n", getpid(), getppid());
        printf("Child executing command: %s\n\n", command);

        // Execute the command using execlp
        execlp(command, command, NULL);
        perror("exec failed"); // Only runs if exec fails
        exit(1); // Exit child with error if exec fails
    } 
    else {
        // Parent process
        wait(NULL); // Wait for child
        printf("\nParent Process Resumed: Child finished execution\n");
    }

    return 0;
}
```


##OUTPUT

<img width="635" height="271" alt="Screenshot from 2025-11-11 11-22-22" src="https://github.com/user-attachments/assets/a987f247-ee96-435d-b7ca-d6e492e7dc01" />











# RESULT:
The programs are executed suc
