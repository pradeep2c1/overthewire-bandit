# overthewire-bandit
Commands and explanantion

### General Help
To know how to use a command: `man <command>`  
Note: The `man` command also has a manual.  
Press 'q' to quit the man command.  

If there is no man page, the command might be a "shell built-in".  
In that case use the `help <X>` command. E.g. `help cd`.

---
## Level 0
**Command**: `ssh`  
**Description**: `ssh` (SSH client) is a program for logging into a remote machine and for executing commands on a remote machine.  
It is intended to provide secure encrypted communications between two untrusted hosts over an insecure network.  
Command used: ```ssh bandit0@bandit.labs.overthewire.org -p 2220```
(`ssh <username>@<computer name or IP address> -p 0000`)

  ---
## Level 0 --> Level 1
0. `man` - an interface to the system reference manuals  
1. `ls` - list directory contents
List  information about the FILEs (the current directory by default).  Sort entries alphabeti‐cally if none of -cftuvSUX nor --sort is specified.  
2. `cd` Change the shell working directory.  
  Change the current directory to DIR.  The default DIR is the value of the HOME shell variable.
  
  The variable CDPATH defines the search path for the directory containing
    DIR.  Alternative directory names in CDPATH are separated by a colon (:).
    A null directory name is the same as the current directory.  If DIR begins with a slash (/), then CDPATH is not used.
  
3. `cat` - concatenate files and print on the standard output
  Concatenate FILE(s) to standard output.
  With no FILE, or when FILE is -, read standard input.
  
  EXAMPLES
       `cat f - g`
              Output f's contents, then standard input, then g's contents.
  
4. `file` — determine file type  
  `file` tests each argument in an attempt to classify it.  There are three sets of tests, performed in this order: filesystem tests, magic tests, and language tests.  The first test that succeeds causes the file type to be printed.
  
5. `du` - estimate file space usage
  Summarize disk usage of the set of FILEs, recursively for directories.
  
6. `find` - search for files in a directory hierarchy
  `find` searches the directory tree rooted at each given starting-point by evaluating the given expression  from  left  to  right, according  to the rules of precedence (see section OPERATORS), until the outcome is known (the left hand side is false for and operations, true for or), at which point find moves on to  the next file name.  If no starting-point is specified, '.' is assumed.
  
### Approach
  On using `ls` command, got to know about the only file 'readme' in the directory. Then checked its type, using `file` command to be 'ASCII text'  
  Then used the `cat readme` command to print the content text, which was the desired password, copied it, to log in to the 'bandit1'  
  And then `exit` command to logout from bandit0.
  
  ---
## Level 1 --> Level 2
### Approach
On using the command `ls`, got to know of a file '-'.  
But directly using the `file -` doesn't work, so we need to use `file ./-`, which gives the file type as 'ASCII text'.  
Then again using `cat ./-` gives the desired password.

---
## Level 2 --> Level 3
### Approach
There is a file in named 'spaces in this filename'.  
Now, the command, `file spaces in this filename` didn't work, because of the spaces in the filename. 
So, use `file spaces\ in\ this\ filename`, or `file "spaces in this filename"`, or `file 'spaces in this filename'`, which gives the file format as 'ASCII text'.  
Then, use the command, `cat spaces\ in\ this\ filename`, to print the text.

---
## Level 3 --> Level 4
### Approach
There is a 'inhere' directory, which doesn't show any files in it on using the `ls` command.  
So, in order to see the hidden files, use `ls -a` instead, which shows the 'hidden' file, again an ASCII text file, which has the password.

---
## Level 4 --> Level 5
### Approach
In the directory, 'inhere', there are a total of 10 files, of which -file07, on observing using the command `file ./-file07`, can be observed to be an ASCII text file.  
On printing it using `cat ./-file07`, gives the password for Bandit 5.
