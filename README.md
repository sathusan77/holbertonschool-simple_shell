# HOLBERTON SCHOOL — simple_shell
# Description

hsh is a minimal UNIX command line interpreter written in C.
This project is part of the Holberton School curriculum.

The shell reads user input, parses commands, searches executable paths,
and executes programs using system calls.

# Compilation
gcc -Wall -Wextra -Werror -pedantic -std=gnu89 *.c -o hsh
# Usage
./hsh
$ ls
$ /bin/ls
$ ls -l /tmp
$ exit

The prompt is shown only when stdin is a terminal (isatty)

Ctrl + D (EOF) exits the shell

Ctrl + C prints a new prompt without exiting

# Core Behavior
# Input Reading

The shell uses getline() to read input from stdin

One command is processed per line inside a loop

# Command Splitting

The input line is split into a char ** using strtow()

Separators handled:

space

tab

newline

The : character is also handled internally to split PATH

# PATH Handling

get_path() retrieves the PATH environment variable

If the command is not a direct path (/ or ./):

Each directory in PATH is checked

When found:

cmd[0] is replaced with the full executable path

fork() is not called if the command does not exist

# Execution

execve_cmd():

creates a child process using fork()

the child executes the command using execve()

the parent waits using waitpid()

# Error Handling

Error messages match /bin/sh format

Example:

./hsh: 1: qwerty: not found

Errors are printed to stderr

Exit codes follow UNIX standards:

127: command not found

126: permission denied or directory

2: invalid exit argument

# Built-in Commands
# exit
exit
exit N

Exits the shell

If N is provided, the exit status is N % 256

Invalid numbers exit with status 2

# env
env

Prints the current environment

# Project Files
shell.c

Main loop

Prompt handling (isatty)

Signal handling (SIGINT)

Built-in command dispatch

execve.c

execve_cmd()

Handles fork, execve, and waitpid

get_path.c

PATH resolution

Executable path replacement

strtow.c

Input string tokenization

shell.h

Function prototypes

Include guards

extern char **environ

# Authors

Sathusan

Janice

![Flowchart] (flowchart, 12_24_16.png)
