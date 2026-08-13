# Bash Playground

# Common Commands
tab complete - hitting tab completes your search, only as accurate as the info you give it

### echo - prints to the terminal screen or standard output

<pre><code>
#!/bin/bash

# echo something
echo foo
foo

# write std output to a file (overwrites)
touch myfile.txt
echo hello > myfile.txt
cat myfile.txt
hello

# append std output to a file (does not overwrite)
echo hello again >> myfile.txt
cat myfile.txt
hello
hello again



</pre></code>

### cd - change directory
- use `../` to back out n times out of a directory
- `cd .` will leave you in the same directory, as `.` which is the current working directory
- `cd -` makes cd go into the previous directory you were in


### ls - list
- `ls -a` lists ALL the files... 

### pwd - print working directory
- args

### touch - create a file
- touch myfile.txt
mv - move a file
### mv myfile.txt thatfile.txt
### rm - remove a file
- rm myfile.txt
- use -i for interactive, questions you on the deletion of a file
- use -f to force a file removal
- use -r to remove recursively
- chain arguments like rm -rfi

### alias - lets you map bash commands to strings
- usage `alias rm='rm -i'` //if rm is called, it invokes rm with the -i flag, so rm is an ***alias*** for rm -i`
- run `alias rm` to see its alias binding

### history - prints the command line history
- super useful to see what you ran prior, lets you check all the previous input commands

!!! note
    hidden files must have their name prepended with a `.`
    they can be seen by using `ls -a`

## grep
### Command line utility for searching text that matches an expression

- Arguments can be chained after calling grep.

- -o only print the line that matches
<pre><code>
#!/bin/bash
echo >> luca file.txt
grep luca file.txt
luca
grep -o '^l.' file.txt
lu
# Remember, ^ is for searching how a line starts, and `.` means any character.
# Since only `l.` matched the first line in the first 2 characters, it returned only what matched exactly what was requested.
</pre></code>

- -i returns case insensitive lines
<pre><code>
#!/bin/bash
echo >> luca file.txt
echo >> LUCA file.txt
grep luca file.txt
luca
grep -i luca file.txt
luca
LUCA
</pre></code>

<pre><code>
#!/bin/bash
grep luca /path/of/dir
# returns files that contain `luca` in the given search directory
</pre></code>

- By adding single quotes to the search string you can feed the search parameter conditional arguments<br>
<pre><code>
#!/bin/bash
grep '^luca' /path/of/dir 
# searches for all files that **start** with luca
</pre></code>
<br>

<pre><code>
#!/bin/bash
grep `luca$` /path/to/dir 
# searches for all files that **end** with `luca`
</pre></code>

- Search within a file for a specific line

<pre><code>
#!/bin/bash
grep b file.txt
# searches for all lines that contain b in file.txt
</pre></code>

- Search within a file for a specific line and print what comes one line after/before. A = after, B = before, C = context the number is how many lines back/forward you want. They cannot be chained like the standard grep arguments

<pre><code>
#!/bin/bash
grep -A1 b file.txt
# Searches for b in file.txt and prints 1 line AFTER the found line
</pre></code>

<pre><code>
#!/bin/bash
grep -B1 b file.txt
# Searches for b in file.txt and prints 1 line AFTER the found line
</pre></code>

<pre><code>
#!/bin/bash
grep -C1 b file.txt
# Searches for b in file.txt and prints 1 line before and after the found line. C stands for context, so it gives you the lines above and below.
</pre></code>