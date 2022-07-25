## What is a shell ? 
Is a program that `passes` or commands to the OS(or Kernel) for execution. Note : BASH stands for 'Bourne Again Shell'. Bash is a reference to `Stever Bourne` 
the first person to create a shell.

## Printing something in the screen : 
``` powershell
root@7e01079dc012:/# echo Hello Docker
Hello Docker
```
## Who is the current log in user : 
``` powershell
root@7e01079dc012:/# whoami
root
```

## Checking where the bash program itself is : 
``` powershell
root@7e01079dc012:/# echo $0
bash
```

## Checking the commands that used so far : 
``` powershell
root@7e01079dc012:/# history
    1  history
    2  echo Hello Docker
    3  history
```

## Using a command from the history : 
``` powershell
root@7e01079dc012:/# !2
echo Hello Docker
Hello Docker
```
