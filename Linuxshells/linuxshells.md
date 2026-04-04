# introduction to linux shells
a shell is a program that allows users to interact with the operating system through commands.

it acts as an interface between the user and the linux kernel

common uses:
- running commands 
- navigating the file system
- automating tasks
- scripting
- system administration

example shell prompt:
```
user@machine:~$

```
the shell reads commands, executes them, and prints the output.

security relevance:
- used heavily during penetration testing
- attackers often gain shell access on compromised machines

# how to interact with a shell
to interact with a shell, you execute commands inside the terminal.

show current directory
```
pwd

output example:
/home/user

```
list directory contents
```
ls
shows files and directories in the current folder

common options:
ls -l = detailed list.

ls -a = shows hidden files

```
change directory
```
cd foldername
```
example:
```
cd /home/user/documents
```
go back one directory:
```
cd ..
```
read file content
```
cat filename.txt
```
example:
``` 
cat notes.txt
```
displays the contents of a file

### search text inside files
```
grep "word" filename
```
example:
```
grep "password" file.txt
```
used in security investigations.

# types of linux shells
different shells provide different features

common shells include:

1. bash(bourne again shell)
most popular shell in linux

features:
- scripting support
- command history
- tab completion

2. sh (bourne shell)
original unix shell

basic functionality

3. zsh (z shell)
advanced shell with extra features
- better tab completion
- plugins
- customization

4. fish shell
user-friendly shell with auto suggestions

list available shells
```
cat /etc/shells
```
example output
```
/bin/bash
/bin/sh
/bin/zsh
```
# shell scripting and components 
shell scripting allows you to automate tasks using scripts

a shell script is simply a text file containing commands

example file:
```
script.sh
```

basic script structure
```
#!/bin/bash

echo "hello world"
```

explanation:
- #!/bin/bash = interpreter declaration
- echo = prints text

run script:
```
bash script.sh

or

./script.sh

(after giving execute permission)
```

give execute permission
```
chmod +x script.sh
```

variables in shell
```
name="raju"
echo $name

output:
raju

```
conditional statements
example:
```
if [$age -gt 18]
then
echo "adult"
fi
```
used for decision making

loops
example:
```
for i in {1..5}
do
echo $i
done
```
loops automate repeated tasks

# the locker script

this task demonstrates a simple security script.

purpose:
- protect files
- simulate password lock system

example script concept:
```
#!/bin/bash

password="secret"
read -p "enter password:" input
if ["$input" == "$password"]
then 
echo "access granted"
else
echo "access denied"
fi
```
security relevance:
- demonstartes authentication logic
- used in automation scripts

# practical exercise
in real systems shell scripts are used to:
- automate system tasks 
- search files
- analyze logs
- monitor processes

example search command:

```
grep -r "error" /var/log
```
searches for the word error in log files

loop example for file processing
```
for file in *.log
do 
echo $file
done
```

used for analyzing multiple files

security use:
- log analysis
- detecting suspicious activity

# conclusion
linux shells allow users to 
- execute commands
- automate tasks
- creates scripts
- manage systems

shell knowledge is essential for:
- system administrators
- cybersecurity analysts
- ethical hackers

important commands for cybersecurity

these are frequently used by ethical hackers.
- pwd
- ls
- cd
- cat
- grep
- chmod 
- ps
- top
- netstat
- ss
