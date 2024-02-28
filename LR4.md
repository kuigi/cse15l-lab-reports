# Lab Report 4

## Step 4 - Log Into ieng6

First, we need to log into our ieng6 account. Since the `ssh` command is already in our history, we can use command history to access it.
`<Up> <Enter>` accesses the `ssh lbartulo@ieng6.ucsd.edu` command and logs us in to ieng6.

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/f7b00ccc-d24d-4bd2-a9db-23c3c4ab044c)

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/f93cdbf8-7384-4303-a8c4-6bf6ca64810e)



## Step 5 - Clone Repo
We need to insert the command `git clone git@github.com:kuigi/lab7.git` in order to clone my forked repo with the ssh key.
Since `git clone git@github.com:kuigi/lab7.git` is in my clipboard already, I just need to paste it into the command line by doing:
`<Right-Click> <Enter>`
![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/842f09b0-6e4f-4807-b7c0-24a69a787980)


## Step 6 - Run Tests

In order to run the tests, first I needed to `cd` into the `lab7/` directory by doing: 
`<c> <d> <Space> <l> <Tab> <Enter>`
Next, I used command history and autocomplete to run the `test.sh ` file using bash by doing:
`<Ctrl+R> <b> <a> <Enter>`
This autocompletes the command `bash test.sh` and uses that script to run the tests.

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/a3b2c057-d8de-45ca-85c1-751fae7323b4)



## Step 7 - Edit File in Vim

When we run the tests, we see that we need to correct `ListExamples.java` to pass all the tests.
We already have the command to open `ListExamples.java` using Vim in our command history, so we use command history and 
search/autocomplete to bring the command `vim ListExamples.java` back by pressing:
`<Ctrl-R> <v> <Enter>`

Once this command is executed and we enter the file through Vim, to reach the part that we need to fix the fastest, we access the last instance
of "x1" in order to access `index1 ` in the line `index1 += 1;` and change that to `index2`.

We do this by inputting in Vim:

`<?> <x> <1> <Enter> <l> <l>` to access `1`
`<i> <Bksp> <2> <Esc>` to enter Insert mode, delete `1` and replace it with `2`, then exit Insert mode
`<Shift+;> <w> <Enter> <Shift+;> <q> <Shift+1> <Enter>` in order to save our changes and exit Vim.

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/bcda60e2-e77f-4a90-aed0-e9f5281a7f2c)

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/9addc674-3595-42a2-8145-2bfc00da0589)


## Step 8 - Run Tests to Confirm

To confirm our `ListExamples.java` file is now all good and will pass our tests, we run the tests again using `bash test.sh`. 
Since it is already in our command history, we simply access it from there and run it.

`<Up> <Up> <Enter>` access that command from the command history and runs it.

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/3c2b5272-917c-4634-aab1-f88eee50ef4f)


## Step 9 - Add + Commit through Git

Now, all we need to do is add our changes to our commit and push our commit, all from the command line.
The commands we are using are already in our command history, so we simply use search/autocomplete to access
and use the commands `git add --all` and `git commit`. When committing, our commit message will simply be "hi" :)

`<Ctrl+R> <a> <d> <Enter>` finds and runs the command `git add -all` from our command history.
`<Ctrl+R> <c> <o> <m> <m> <Enter>` finds and runs the command `git commit` 
`<I> <h> <i> <Esc> <Shift+;> <w> <Shift+;> <q> <Shift+1> <Enter>` adds our commit message, then saves the 
commit message and exists, pushing our changes to the forked repo. 
And we're done!

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/b7654565-c5f4-4a55-8007-c5de7af28aba)

Now the changes we made in Vim are saved in our forked repo.
