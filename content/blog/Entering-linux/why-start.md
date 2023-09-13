---
title: My first post
date: "2023-09-08T23:46:37.121Z"
description: "context"
---

# why did I start

Let me preface this section. If i want to get into cloud engineering job I need to know linux. nearly every system in the world is connected to runn ing some kind of linux distro. Bash is the language help me script in all those situations and previously in my last job great for automation. this is me refreshing some of the things because i've been using mac-os zsh customizations. I hope to get comfortable with vim eventually. That is the goal for today using the microsoft resource given. 

https://www.youtube.com/playlist?list=PLlrxD0HtieHh9ZhrnEbZKhzk0cetzuX7l



#cheatsheet #linux 

## Finding out info for a bash command

descriptions and flags found using the commands for help and manual
> Examplecmd --help
> man Examplecmd

TODO: check how to use pushd and popd for advanced navigating

## Command:  ls

displays only files with letters s with wildcard:
> ls s* 

return back results with more than one letter with a character set combined with wildcard:
> ls [cs]* 

return back with same file type:
> ls *.md 

use "?" for any character in a search. example returns and file name with 2 character extensions like .md or .js:
>  ls *.?? 

Used for finding anything with a capital letter:
> ls [\[:uppper:]]*

Same for anything lower case
> ls [\[:lower:]]* 

## Command:  whereis

Locate the binary, source, and manual-page files for a command.
> whereis bash

## Command:  which

Only  returns  the  pathnames of the files (or links) which would be executed in the current environment
> which bash

## Command:  find

search for files in a directory

> find . -name \*.md

> find /home -name file.txt


# TEXT AND FILE MANIPULATION
## Command:  mkdir
just make a new directory(folder)

example where parent folder doesnt exist
> mkdir -p newFolder/Subfolder

## Command:  mv 
just move files
> project1/file.txt newFolder/Subfolder

## Command:  cp 
copy files over
> cp project02/file.txt project01/file01.txt

## Command:  rm 
delete file or files
> rm file01.txt
> rm \*.md

## Command:  rmdir
delete directories. Without args/wildcards, it will delete the last folder in the pathname given
> rmdir sub1/sub2


## Command:  cat
stands for concatenate although can be used as a print line tool on the terminal
> cat quotes01.txt 
> cat quotes01.txt quotes02.txt 


## Command:  head
shows the first 10 lines instead of everything very useful tip
> head longOutput001.log

Use -n to choose how many lines you want to print out 
>head -n 3 fake001.log 

## Command:  tail
shows the last 10 lines instead of everything
> tail longOutput001.log

## Command:  more and less
lets you navigate the textfiles

less lets you scroll with spacebar and b 
and use search params

## Command: grep 
to parse though and match a result in a text file 
> grep "123.26.119.140" fake002.log

# ENVIRONMENT VARIABLE CONTROLS
## Command: env 
Set each NAME to VALUE in the environment and run COMMAND.

## Command: echo 
prints the value of the variable 
to print variable value you will need to start with "$" to access the values 
some useful examples for any new instances:
> echo $SHELL
> echo $HOME
> echo $USER

Super useful to find location of executables which will need to be updated when a new program is added. like a new CLI, this will help the system locate the binary to use the cli command:
> echo $PATH 


## Command: export 
create environment/shell values:
> export newVar=value

"newVar" is only available in that terminal session that it is created in, they do not persist in new sessions

global configuration would solve this issue under: "/etc/profile"
It would effect every user logged in the machine

".profile",".bashrc" files can be edited and will be loaded into every different session
would be a different effect for every user in a machine



# REDIRECTION 

## Command: >
The command is redirecting the output into the file name give. if it does not exist it will create the file 
> ls-l > outputfile.txt
> echo "this is some strings2" > raiyansoutput.txt

## Command: >> 
This command redirects and appends the file with output instead of always overwriting like the above.
> ls-l >> outputfile1.txt

## redirect standard errors to an output

the same command to redirect(>) can do so for standard errors like below 

> ls -l ./dir > error.txt 2>&1

is the same as 

> ls -l &> output2.txt

TODO: not sure why the 2and &1 is needed with the redirect command. it isnt working without it. looks like its something about redirecting stream 2 into 1. need more info aboiut i/o streams

## combining files 

using cat command again we can now use it for combining different files. this example shows 2 text files concatenated and the its output redirected to file name paragraph.txt. insanely useful for automating and scripting.
> cat part1.txt part2.txt > paragraph.txt

# PIPELINES

Sometimes you don't want the command to push output into a different file. pipelines will help to push your outputs into another command using pipelines.

below this will pollute your terminal with a large out of all the file names. a common way to have a nicer view is to pipeline the out into the less command
>ls -l /usr/bin
>ls -l /usr/bin | less

another common example is searching through the directory :
>ls -l /usr/bin | grep echo

and pipe it to even another command after:
>ls -l /usr/bin | grep echo | sort

print just the first line alternative with pipeline example:
> cat part1.txt | head -n 1


# Modify file permissions 

## reading permissions
running the line "ls -l" will show you the permissions with output like this:
> -rw-rw-rw-  1 vscode root 3070 Sep  7 14:31 README.md

(-rw) first 3 tell me if it a file or directory (- or d) with wr being the users read/write permissions 
(-rw) characters 3-6 tell me the same but for group instead of user
(rw-) the others permissions 

(1) number of linked hard links

(vscode) the user
(root) the group

(3070) size of the file
(Sep  7 14:31 ) date modified
(README.md) The file name

## Command: chown 
changes the permission of any file with another setting
this example is only changing the user permission:
> sudo chown root newFile.txt

to change the permision of the group with semi colon
> sudo chown :root newFile.txt

## Command: chgrp
change the group ownership
> chgrp vscode newFile.txt

## Command: chmod
change the read/write permission 
This example makes my script.sh executabkle in all the permission types
> chmod +x script.sh

you can write all the permissions with octal numbers instead r=4 w=2 x=1:
> chmod 664 script.sh

# BASH SCRIPTING
Start writing the bash commands in an executabkle file with can be saved and shared for later uses.

when creating a bash script start the file at the top with a shebang (#!)
The line tells the environment that we are in, what interpreter to use. In this example it is going to be bash:
>#!/bin/bash

comments in bash are just a hashtag(#)

Once you make a script you can move it to a directory in your $PATH variable 

## Make an executable command from your bash script

1. looking for a path executables 
   >$ echo $PATH
   >
/vscode/bin/linux-x64/8b617bd08fd9e3fc94d14adb8d358b56e3f72314/bin/remote-cli:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/vscode/.local/bin

2. I can see "/home/vscode/.local/bin" is a possible option. create the directories if it doesn't exist
>mkdir -p /home/vscode/.local/bin

3.  Now I can paste the script in the directory and run it directly as a command in my terminal 
> $ cp hello_world /home/vscode/.local/bin
> $ hello_world 
> Hello World!

# VARIABLES IN BASH

> hello_message='Hello Worlds!'
> echo $hello_message

if you want to assign the output of a command to a variable, you can in bash

> current_dir=$(pwd)
> echo $current_dir


## Single vs double quotes

To get the output with varible values shown always use double quotes
>echo "$hello_message and $current_dir"

results:Hello Worlds! and /workspaces/bash-for-beginners/what-is-a-bash-script

if you want the variable names to be printed and not computed use single quotes
>echo '$hello_message and $current_dir'

results:$hello_message and $current_dir


## Constants
immutable values that cannot be changed after being declared
> readonly variable_wont_change="blue"


## Doing maths
Arithmetic expansion allows the evaluation of an arithmetic expression and the substitution of the result. The format for arithmetic expansion is:

>$(( expression ))
>$((number % 2)) -eq 0

# Conditional statement
if statements work in the format below with if,then,else but needs to be closed with fi 

>if [ $((number % 2)) -eq 0 ];
>then
>echo "The number $number is even!";
>else
>echo "The number $number is odd!"
>fi

difference in equality checkers:
>`=` and `==` are for string comparisons  
>`-eq` is for numeric comparisons
>**_-ne_** for not equal numbers
>**_-gt** for greater than
>

## Command: read
use the command to take input. example below has -p flag for prompt and then the variable to store the input.

>read -p "Enter a number: " n

# case statements

start with case (variable) in 
and then end with case spelt backwards

>case $n in
> ???)
>echo "3 characters found";;
>1|2)
>echo "One or two found";;
>aa)
>echo "double aa found";;
>\*.txt)
>echo "a text file found";;
>*)
>echo "Other";;
>esac


# Functions

functions and variables defined before being called like c.
looks like normal format:
> myFunction () { ...enter code...}

and then call your function with a parameter like this:
> myFunction $number 

the params are called inside the function as $1 $2 $3.... for however many params you send.
$0 is reserved for the function's name when defined in the terminal. When defined in a bash script, **`$0`** returns the script's name and location.
example below will print out whatever value of $number as $1
> myFunction () { 
> echo $1
> }

if you need write variables in a function and you don't want global scope. declare variables as:
> local myNum=5


# Loops

while loops format, remember to end with done:

you can also use break keyword in the loop to stop iterating

> while [\[ ...conditional statement]];  do
> 	write a function here
> done

until loops same thing until condition is true unlike while

for loops(traditional like c#)

>services=("loadbalancer" "virtualmachine" "storage")
>for i in "${services[@]}"
>do
>echo $i
>done


for loops (newer like c)

> for (( i=0; i<5; i=i+1 )); do
> echo "The counter is at: $i"
> done