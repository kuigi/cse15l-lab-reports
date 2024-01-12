# Lab Report 1

## Command `cd` 


**Using no arguments:**


![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/c8ee5baa-d13b-48d6-b0e4-b47d5492cefb)


The working directory was `/home` when the command was run. 
The command is used to enter a directory given by the argument following `cd`. Since there was no argument following cd, we did not enter a directory.
The output is not an error.


**Using a path to directory `/home/lecture1/`:**


![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/1f6e82f4-2f4d-4c8b-a1d9-4726ec75c7e3)


The working directory was `/home` when the command was run. 
This time, we provided an argument to `cd`, which was `/home/lecture1/`. 
This provides a directory for us to enter using `cd`, and through this we can now see on the left side that we are now accessing the `/home/lecture1/` directory.
This is not an error.


**Using a path to file `/home/lecture1/README`:**


![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/60b242ab-7e91-4b59-8bec-bf2a5f54324d)


The working directory was `/home` when the command was run. 
The argument passed to `cd` this time was a file path. Since `cd` can only be used to access directories, this results in an error.
The terminal states that `/home/lecture1/README` is "Not a directory" and does not let us access it using cd.


## Command `ls` 


**Using no arguments**


![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/a213ed36-9508-4833-ba0f-5c8177e6db1a)


The current working directory is `/home` when command is run.
The command `ls` lists all of the files and folders at the path given by the following argument. However, since we do not provide a path argument, it simply provides the files/folders in the current directory. Here, it is only the folder lecture1.
This is not an error.


**Using a path to directory `/home/lecture1/`**


![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/b56879f0-ff4d-4518-a310-7ed7580405f9)


The cwd is `/home` when file is run.
This time, we provide a directory that `ls` can access and display all of the file and folder names of. It displays the file and folder names contained inside the directory `/home/lecture1/`.
There is no error.


**Using a path to file `/home/lecture1/README`**


![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/665f3baa-c4fa-4882-b9ce-5b863dd2e2ac)


The cwd is `/home` when file is run.
Using the `ls` command, we provide the path of a single README file this time. The output is not a file name, but rather the file path.
I am not sure if this is an error, or if this is the intended output of using the `ls` command with a file path.


## Command `cat`


**Using no arguments**


![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/23b10146-bf00-4030-a4b1-18ca79f0e476)


The current working directory is `/home`.
The command `cat` is used to print the contents of one or more files of the paths given as an argument. Since we pass in no arguments, nothing is printed.
This is not an error.


**Using a path to directory `/home/lecture1/`**


![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/2723b9bd-28e3-4226-9edf-7a3eb54fc256)


The current working directory is `/home`.
This time, we pass in the path for a directory, `/home/lecture1/`. However, since this is not a path to a file, the `cat` command does not print out its contents, instead saying the path "Is a directory".
This is not an error. 


**Using a path to file `/home/lecture1/README`**


![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/63e0dbf3-c8ed-4131-90fa-6f2475fdf827)


The current working directory is `/home`.
Finally, we pass in the path for a single README file. The `cat` command reads this valid file argument and prints out the contents inside the file.
This is not an error.




