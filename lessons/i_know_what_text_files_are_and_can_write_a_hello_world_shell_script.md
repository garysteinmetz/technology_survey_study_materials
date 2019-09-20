# I know what text files are and can write a hello world shell script

## Text files? They're boring.

Yes, that's the point.

## Why are we talking about them?

Software developers interact with them all day. Whether it's a web page, source code, database script,
infrastructure file, or something else, actual development usually takes place in a 'plain old' text file.

How the coding takes place in a text file may be special (e.g. HTML encoding), but the developers interaction
with a text file is very generic.

## What is a text file anyway?

It's a file where all or most every character can easily be found on the keyboard -
numbers, letters, punctuation, and other common symbols (like '#', '&', and '{'). They may contain
special formatting (like HTML), but the basic layout isn't hard to read.

For text files consisting of just characters from the English character
set (including letters 'a' through 'z'), each character corresponds
to one byte (eight bits) in memory. Each additional character increases
the size of the file by one bit. For instance, if in a new file, someone
types the numbers '1' through '8' and then saves it, that file will
by 8 bytes in size (quite small). If the '8' is deleted and then the
file is resaved, then the size of the file would by 7 bytes.

Characters that cannot be seen (like spaces, tabs, and the 'return' key)
are collectively called 'white space' and each of these characters
also use one byte of memory (with the exception of the Windows 'return' key
which inserts two characters - a 'carriage return' and a 'line feed').

## How do developers interact with text files?

They use a text editor, like Mac's `TextEdit` or Microsoft's `Notepad`
(Unix users frequently use a program called `vi`). They `do not` interact with text files using a word processor which would add special formatting.

## Why would a developer want to just deal with a boring medium like text files?

Developers want a very direct 'cause-and-effect' conversation with the technologies they are using.
Mandating user-friendly 'fluff' between developer and technology just distorts the conversation
and makes solving problems even tougher.

As an example in the field of literature, scholars of Shakespeare prefer
to read the original text of his plays instead of reading a more contemporary
script without the 'thees' and 'thous', and certainly not (in general)
base research work on a film adaptation of one of his plays.

## Serious software projects typically use many files, surely developers use something more advanced than a text editor

Surprisingly enough, a minority of hard-core developers still use
generic text editors even for more advanced projects, but developers
generally prefer to use a type of software called an Integrated Development
Environment (IDE). IDEs are, at their core, just glorified text editors
but add a lot of additional support for things like source code management,
copy-pasting, refactoring (finding options to improve software),
and debugging.

## Exercise - Output the Contents of a Text File onto Command Prompt

Create a text file (using a text editor!) with "Hello World" as its only contents.
From the command line, use the `cat` command (in Mac/Unix) to output the file's contents
(use the `type` command instead on Windows). The output should exactly match the file's contents.

## Exercise - Output the Contents of a Text File onto Command Prompt

Create a word processor file (using a word processor!) with "Hello World" as its only contents.
From the command line, use the `cat` command (in Mac/Unix) to output the file's contents
(use the `type` command instead on Windows). The output should look strange.

## Exercise - Use a Text Editor to Create a Shell Script to Output 'Hello World'

On Mac/Unix, use a text editor to create file 'hello_world.sh' with the following content.
Note, to be able to execute (run) the file

```
echo 'Hello World'
read -rsp $'Press any key to continue...\n' -n 1 key
```

On Windows, use a text editor to create file 'hello_world.bat' with the following content.

```
echo 'Hello World'
pause
```

Execute (run) the file and 'Hello World' should appear in the output.
Note - running the file might require enabling 'execute' privileges,
on Mac/Unix this is achieved by executing the `chmod 777 hello_world.sh` command
(which gives read, write, and execute privileges to everyone).
