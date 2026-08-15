# Bash Playground
By Luca Lanzillotta
- Using [this](https://www.youtube.com/playlist?list=PL-my9REMIFtGgiQAXqKPJ5UrLdSkxcLBT) guide to learn bash
- Linux [manual](https://man7.org/linux/man-pages/man1/type.1p.html) page

# Common Commands
- Below is an accumulation of programs within bash that are invoked by their respective commands. 
This serves as a way to document my process in learning how to navigate bash and feeling more comfortable in the shell.

### tab complete 
- hitting tab completes your search, only as accurate as the info you give it

### help
- help gives the manual for the desired program that is natively built into bash.
<pre><code>
help echo
</pre></code>

### man pages
- man invokes the programs manual. It is opened using less, and can be navigated using less commands
<pre><code>
#!/bin/bash
man git
*prints the git manual*
</pre></code>

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

### pipes - inputs the argument to the right of the pipe to the output of the shell argument to its left
<pre><code>
echo helloworld >> file.txt
cat file.txt | grep -o 'h....'
hello
</pre></code>

!!! note
    hidden files must have their name prepended with a `.`
    they can be seen by using `ls -a`

### grep - Command line utility for searching text that matches an expression

- Arguments can be chained after calling grep.
For example `grep -io` is the same as `grep -i -o`

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

### less - Display the contents of a file in a terminal
<code><pre>
less /usr/share/dict/words
</code></pre>

- prints contents of the file
- Navigate up/down with arrow keys, or use j and k
- if you hit `:h' the help window will open

### more - Display the contents of a file in a terminal (less is better)
- same as less but more only allows forward scrolling
<pre><code>
more /usr/share/dict/words
</pre></code>

### type - Tells you how a shell interprets a specific command name
- Type indicates how each argument would be interpreted if used as a command name
- Tells you if commands are aliased to other things if they are shell functions, and more.
<pre><code>
#!/bin/bash
type -a rm
rm is /bin/rm
</pre></code>

### compgen - lists all the possible completion matches for strings of text
<pre><code>
!#/bin/bash
compgen -b #lists built in shell commands
</pre></code>

### file - identifies what type of file something is
<pre><code>
#!/bin/bash
echo hello world >> helloworld.txt
file hello_world.txt
helloworld.txt: ASCII text
</pre></code>

or a little more freaky...

<pre><code>
file /bin/rm
/bin/rm: Mach-O universal binary with 2 architectures: [x86_64:Mach-O 64-bit executable x86_64] [arm64e:Mach-O 64-bit executable arm64e]
/bin/rm (for architecture x86_64):      Mach-O 64-bit executable x86_64
/bin/rm (for architecture arm64e):      Mach-O 64-bit executable arm64e
</pre></code>

### tr - translate a character into another character
- useful for changing how data is displayed. For example, in this example colons have been turned into newlines
<pre><code>
echo $PATH
/Users/luquito/.rd/bin:/Users/luquito/.nvm/versions/node/v20.20.2/bin:/Users/luquito/.vscode-server/data/User/globalStorage/github.copilot-chat/debugCommand:/Users/luquito/.vscode-server/data/User/globalStorage/github.copilot-chat/copilotCli:/opt/homebrew/bin:/opt/homebrew/sbin:/Library/Frameworks/Python.framework/Versions/3.14/bin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin:/pkg/env/global/bin:/Users/luquito/.vscode-server/data/User/globalStorage/github.copilot-chat/debugCommand:/Users/luquito/.vscode-server/data/User/globalStorage/github.copilot-chat/copilotCli:/Users/luquito/.vscode-server/cli/servers/Stable-a5b500951314efd502d07465bd138dfbd714a960/server/bin/remote-cli:/Users/luquito/.rd/bin:/Users/luquito/.nvm/versions/node/v20.20.2/bin:/opt/homebrew/Caskroom/miniconda/base/condabin

echo $PATH | tf : '\n' #you must quote things with special characters to escape it btw

/Users/luquito/.rd/bin
/Users/luquito/.nvm/versions/node/v20.20.2/bin
/Users/luquito/.vscode-server/data/User/globalStorage/github.copilot-chat/debugCommand
/Users/luquito/.vscode-server/data/User/globalStorage/github.copilot-chat/copilotCli
/opt/homebrew/bin
/opt/homebrew/sbin
/Library/Frameworks/Python.framework/Versions/3.14/bin
/usr/local/bin
/System/Cryptexes/App/usr/bin
/usr/bin
/bin
/usr/sbin
/sbin
/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin
/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin
/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin
/pkg/env/global/bin
/Users/luquito/.vscode-server/data/User/globalStorage/github.copilot-chat/debugCommand
/Users/luquito/.vscode-server/data/User/globalStorage/github.copilot-chat/copilotCli
/Users/luquito/.vscode-server/cli/servers/Stable-a5b500951314efd502d07465bd138dfbd714a960/server/bin/remote-cli
/Users/luquito/.rd/bin
/Users/luquito/.nvm/versions/node/v20.20.2/bin
/opt/homebrew/Caskroom/miniconda/base/condabin
</pre></code>

# Scripting and Variables
- Bash uses characters to expand variable contents
### PATH - variable
- Holds all the paths that bash will check to run an executable

### Ended on chapter 2 section 2