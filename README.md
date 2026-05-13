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
#include <stdlib.h>
#include <unistd.h>
int main() {
    int pid = fork();
    if (pid == 0) { 
        printf("I am child, my PID is %d\n", getpid()); 
        printf("My parent PID is: %d\n", getppid()); 
        sleep(2);  // Keep child alive for verification
    } else { 
        printf("I am parent, my PID is %d\n", getpid()); 
        wait(NULL); 
    }
}

```












##OUTPUT
<img width="791" height="117" alt="Screenshot 2026-05-13 083656" src="https://github.com/user-attachments/assets/d69f01e7-75de-4000-9a74-003fa0be0914" />
<img width="641" height="95" alt="Screenshot 2026-05-13 083709" src="https://github.com/user-attachments/assets/ae734453-2474-4c80-8bb5-d618b3003bb0" />







## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family
````
#include <stdio.h>
#include <stdlib.h>
#include <sys/wait.h>
#include <sys/types.h>
int main()
{       int status;
        printf("Running ps with execlp\n");
        execl("ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                puts("child did not exit successfully\n");
        printf("Done.\n");
printf("Running ps with execlp. Now with path specified\n");
        execl("/bin/ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                puts("child did not exit successfully\n");
        printf("Done.\n");
        exit(0);}
        ```
##OUTPUT
<img width="898" height="748" alt="Screenshot 2026-05-13 083632" src="https://github.com/user-attachments/assets/43831e02-523a-485d-951d-277691d950c6" />

##C Program to execute Linux system commands using Linux API system calls exec() family
```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;
    printf("Running ps with execl\n");
    if (fork() == 0) {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);
    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    } 
    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);
    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    printf("Done.\n");
    return 0;
}


```
























##OUTPUT
<img width="821" height="187" alt="Screenshot 2026-05-13 083727" src="https://github.com/user-attachments/assets/de6fb12b-1b4b-4895-8b61-5f4515ad0bc9" />
<img width="717" height="113" alt="Screenshot 2026-05-13 083742" src="https://github.com/user-attachments/assets/b7c438cd-c2ad-4eb2-bb0d-a9965abfcff8" />
<img width="808" height="56" alt="Screenshot 2026-05-13 083808" src="https://github.com/user-attachments/assets/6bef3a5d-fc29-4d8e-8580-6d48a1fa0fc1" />


















# RESULT:
The programs are executed successfully.
