# Bash — Beginner Notes

> [!info] What is Bash?  
> **Bash** stands for **Bourne Again Shell**.
> 
> A shell is a program that lets you interact with your operating system using commands.
> 
> Bash can be used:
> 
> - Interactively in the terminal
>     
> - To write scripts (`.sh` files)
>     
> - To automate repetitive tasks
>     

---

# 1. Bash Basics

## Check which shell you're using

```bash
echo $SHELL
```

or:

```bash
which bash
```

> [!note]  
> `$SHELL` usually shows your default shell.
> 
> `which bash` shows where the Bash program is located.

---

## Print text

```bash
echo "Hello World"
```

You can also print variables:

```bash
name="John"
echo "$name"
```

### `echo` vs `printf`

`echo` is simple and useful for beginners:

```bash
echo "Hello"
```

`printf` gives you more control:

```bash
printf "Hello %s\n" "John"
```

For now, **echo** is perfectly fine for simple scripts.

---

## Bash scripts

A Bash script is usually saved with:

```text
.sh
```

Example:

```text
script.sh
```

A script normally starts with a **shebang**:

```bash
#!/bin/bash
```

> [!important]  
> It's called a **shebang**.
> 
> `#!` tells the system which interpreter should run the script.

Example:

```bash
#!/bin/bash

echo "Hello from Bash!"
```

---

## Run a Bash script

You can run a script by explicitly giving it to Bash:

```bash
bash script.sh
```

Or make it executable:

```bash
chmod +x script.sh
```

Then run it:

```bash
./script.sh
```

### Why `./`?

`./` means:

> "Run the file from the current directory."

So:

```bash
./script.sh
```

means:

```text
Run script.sh from here.
```

---

# File Permissions

Use:

```bash
ls -l
```

Example:

```text
-rw-r--r--  1 user user 123 Sep 27 10:00 script.sh
```

The first part:

```text
-rw-r--r--
```

contains the file type and permissions.

Break it into groups:

```text
- rw- r-- r--
  └─┬┘ └┬┘ └┬┘
   user group others
```

## First character

```text
-
```

Means it's a regular file.

Common examples:

```text
-   regular file
d   directory
l   symbolic link
```

## Permission groups

The next 9 characters are divided into 3 groups:

```text
rw- r-- r--
│   │   │
│   │   └── others
│   └────── group
└────────── owner
```

Each group has:

```text
r = read
w = write
x = execute
```

So:

```text
rw-
```

means:

```text
read + write
```

while:

```text
r--
```

means:

```text
read only
```

Example:

```text
-rw-r--r--
```

means:

- `-` → regular file
    
- `rw-` → owner can read and write
    
- `r--` → group can read
    
- `r--` → others can read
    

---

## Making a script executable

```bash
chmod +x script.sh
```

`chmod` = **change mode**

`+x` = add execute permission.

Check the result:

```bash
ls -l script.sh
```

You might see:

```text
-rwxr-xr-x
```

Now you can run:

```bash
./script.sh
```

---

## `sleep`

Pause a script for a certain amount of time:

```bash
sleep 5
```

This waits for 5 seconds.

Example:

```bash
echo "Starting..."
sleep 2
echo "Done!"
```

---

# 2. Variables and User Input

## Creating a variable

```bash
name="John"
```

> [!important]  
> **Don't put spaces around `=`.**

Correct:

```bash
name="John"
```

Incorrect:

```bash
name = "John"
```

---

## Reading a variable

Use `$` to access its value:

```bash
name="John"

echo "$name"
```

Output:

```text
John
```

You can also use braces:

```bash
echo "${name}"
```

Braces are useful when putting text immediately after a variable:

```bash
name="John"

echo "${name}123"
```

Output:

```text
John123
```

---

## Strings

```bash
name="John"
message="Hello $name"

echo "$message"
```

Output:

```text
Hello John
```

---

## Reading user input

Use:

```bash
read name
```

Example:

```bash
echo "What is your name?"
read name

echo "Hello $name"
```

### `read -p`

You can put the question directly inside `read`:

```bash
read -p "What is your name? " name

echo "Hello $name"
```

This is usually cleaner.

---

# Command-line Arguments

When running a script, you can give it information:

```bash
./script.sh hello world
```

Inside the script:

```text
$1 = hello
$2 = world
```

Example:

```bash
#!/bin/bash

echo "First argument: $1"
echo "Second argument: $2"
```

Run:

```bash
./script.sh apple banana
```

Output:

```text
First argument: apple
Second argument: banana
```

Useful special parameters:

```text
$0    name of the script
$1    first argument
$2    second argument
$3    third argument
...
$#    number of arguments
$@    all arguments
```

Example:

```bash
echo "Script: $0"
echo "Arguments: $#"
echo "All arguments: $@"
```

---

# Command Substitution

You can put the output of a command into a variable.

Use:

```bash
variable=$(command)
```

Example:

```bash
current_directory=$(pwd)

echo "$current_directory"
```

Another example:

```bash
files=$(ls)

echo "$files"
```

> [!tip]  
> `$(...)` means:
> 
> **"Run this command and use its output here."**

---

# 3. Environment Variables

Bash provides many useful variables automatically.

## `$RANDOM`

Generates a random number:

```bash
echo "$RANDOM"
```

Example output:

```text
18432
```

The exact number changes each time.

---

## `$SHELL`

Shows your default shell:

```bash
echo "$SHELL"
```

Example:

```text
/bin/bash
```

---

## `$USER`

Shows the current username:

```bash
echo "$USER"
```

---

## `$PWD`

Shows the current working directory:

```bash
echo "$PWD"
```

This is similar to:

```bash
pwd
```

---

## `$HOSTNAME`

Shows the computer's hostname:

```bash
echo "$HOSTNAME"
```

---

# Environment Variables vs Normal Variables

A normal variable:

```bash
name="John"
```

An environment variable can be created using:

```bash
export name="John"
```

or:

```bash
name="John"
export name
```

The important difference is that an **exported variable is passed to programs started from that shell**.

Example:

```bash
export NAME="John"

bash
echo "$NAME"
```

The child Bash process can see `NAME`.

---

# `.bashrc`

The file:

```text
~/.bashrc
```

contains Bash configuration that is normally loaded when an interactive Bash shell starts.

You can edit it with something like:

```bash
nano ~/.bashrc
```

For example:

```bash
export MY_NAME="John"
```

After saving, either open a new terminal or reload it:

```bash
source ~/.bashrc
```

Then:

```bash
echo "$MY_NAME"
```

---

# `ls -la`

You already know:

```bash
ls -l
```

Another useful version is:

```bash
ls -la
```

Meaning:

```text
-l    long format
-a    show hidden files
```

Files beginning with `.` are normally hidden.

For example:

```text
.bashrc
```

---

# Arithmetic

Bash can perform basic arithmetic with:

```bash
$(( ... ))
```

Example:

```bash
echo $((2 + 3))
```

Output:

```text
5
```

More examples:

```bash
echo $((10 - 3))
echo $((4 * 5))
echo $((10 / 2))
echo $((10 % 3))
```

`%` means **remainder/modulo**.

Example:

```bash
echo $((10 % 3))
```

Output:

```text
1
```

---

## Random number from 0–9

```bash
echo $((RANDOM % 10))
```

Possible results:

```text
0
1
2
...
9
```

> [!note]  
> You don't need `$` inside the arithmetic expression:
> 
> ```bash
> $((RANDOM % 10))
> ```
> 
> is preferred over:
> 
> ```bash
> $(( $RANDOM % 10 ))
> ```

---

# 4. Conditions

Conditions allow your script to make decisions.

Basic structure:

```bash
if [[ condition ]]; then
    echo "Something is true"
else
    echo "Something is false"
fi
```

> [!important]  
> Your original notes had:
> 
> ```bash
> if [ [ condition ] ]
> ```
> 
> The correct syntax is either:
> 
> ```bash
> if [[ condition ]]; then
> ```
> 
> or the older:
> 
> ```bash
> if [ condition ]; then
> ```
> 
> For Bash scripts, `[[ ... ]]` is generally easier and safer to learn.

---

## Example

```bash
age=20

if [[ $age -ge 18 ]]; then
    echo "Adult"
else
    echo "Under 18"
fi
```

---

# Comparison Operators

For numbers:

```text
-eq    equal
-ne    not equal
-gt    greater than
-ge    greater than or equal
-lt    less than
-le    less than or equal
```

Examples:

```bash
[[ $age -eq 18 ]]
[[ $age -ne 18 ]]
[[ $age -gt 18 ]]
[[ $age -ge 18 ]]
[[ $age -lt 18 ]]
[[ $age -le 18 ]]
```

Remember:

```text
-gt = greater than
-ge = greater than or equal
-lt = less than
-le = less than or equal
```

---

# String Comparisons

For strings, you can use:

```bash
name="John"

if [[ "$name" == "John" ]]; then
    echo "Hello John"
fi
```

Not equal:

```bash
if [[ "$name" != "John" ]]; then
    echo "Not John"
fi
```

---

# `elif`

Use `elif` when you have multiple conditions:

```bash
age=20

if [[ $age -lt 13 ]]; then
    echo "Child"
elif [[ $age -lt 18 ]]; then
    echo "Teenager"
else
    echo "Adult"
fi
```

---

# `&&` and `||`

## AND — `&&`

Both conditions must be true:

```bash
if [[ $age -ge 18 && $age -lt 65 ]]; then
    echo "Working age"
fi
```

Think:

```text
condition 1 AND condition 2
```

---

## OR — `||`

At least one condition must be true:

```bash
if [[ $age -lt 18 || $age -gt 65 ]]; then
    echo "Not working age"
fi
```

Think:

```text
condition 1 OR condition 2
```

> [!note]  
> `&&` and `||` are also commonly used between commands:
> 
> ```bash
> command1 && command2
> ```
> 
> Run `command2` only if `command1` succeeds.
> 
> ```bash
> command1 || command2
> ```
> 
> Run `command2` if `command1` fails.

---

# `case`

`case` is useful when you want to compare one value against several possibilities.

```bash
choice="1"

case "$choice" in
    1)
        echo "You selected one"
        ;;
    2)
        echo "You selected two"
        ;;
    3)
        echo "You selected three"
        ;;
    *)
        echo "Unknown option"
        ;;
esac
```

The `*` means:

> Anything that didn't match the previous options.

---

# Exit Status

Every command returns an **exit status**.

Usually:

```text
0 = success
non-zero = error/failure
```

Check the exit status of the previous command with:

```bash
echo $?
```

Example:

```bash
ls
echo $?
```

If `ls` succeeds:

```text
0
```

---

## `exit`

You can stop a script and provide an exit status:

```bash
exit 0
```

Success:

```bash
exit 0
```

Failure:

```bash
exit 1
```

Example:

```bash
if [[ ! -f "file.txt" ]]; then
    echo "File does not exist"
    exit 1
fi

echo "File exists"
```

---

# 5. Loops

Loops allow you to repeat something.

## `while`

Basic structure:

```bash
while [[ condition ]]
do
    echo "Something"
done
```

Example:

```bash
number=1

while [[ $number -le 5 ]]
do
    echo "$number"
    ((number++))
done
```

Output:

```text
1
2
3
4
5
```

### How it works

Start:

```bash
number=1
```

Check:

```bash
number <= 5?
```

If yes:

```bash
echo "$number"
```

Then:

```bash
((number++))
```

Increase the number by 1.

Repeat until the condition becomes false.

---

# Incrementing Numbers

These are common ways to increase a number:

```bash
((number++))
```

or:

```bash
((number += 1))
```

or:

```bash
((number = number + 1))
```

For beginners, this is very common:

```bash
((number++))
```

---

# `read -p`

`read -p` lets you ask the user for input:

```bash
read -p "Enter your name: " name

echo "Hello $name"
```

Example:

```text
Enter your name: John
Hello John
```

---

# `for` Loops

Another very important loop is `for`.

Example:

```bash
for number in 1 2 3 4 5
do
    echo "$number"
done
```

Output:

```text
1
2
3
4
5
```

You can also use:

```bash
for file in *.txt
do
    echo "$file"
done
```

This loops through `.txt` files in the current directory.

---

# Functions

Functions let you reuse code.

```bash
greet() {
    echo "Hello!"
}
```

Call the function:

```bash
greet
```

Example with an argument:

```bash
greet() {
    echo "Hello $1"
}

greet "John"
```

Output:

```text
Hello John
```

---

# Useful Bash Commands

Here are some commands worth knowing as a beginner:

|Command|What it does|
|---|---|
|`pwd`|Show current directory|
|`ls`|List files|
|`cd`|Change directory|
|`mkdir`|Create directory|
|`touch`|Create empty file|
|`cp`|Copy files|
|`mv`|Move/rename files|
|`rm`|Remove files|
|`cat`|Display file contents|
|`less`|Read a file page by page|
|`head`|Show beginning of file|
|`tail`|Show end of file|
|`grep`|Search text|
|`find`|Find files|
|`chmod`|Change permissions|
|`echo`|Print text|
|`sleep`|Wait|
|`clear`|Clear terminal|

---

# Quoting

Quoting is very important in Bash.

## Double quotes

```bash
name="John"

echo "Hello $name"
```

Variables are expanded inside double quotes.

Output:

```text
Hello John
```

---

## Single quotes

```bash
name="John"

echo 'Hello $name'
```

Output:

```text
Hello $name
```

Variables are **not expanded** inside single quotes.

### Easy rule

```text
"..." → variables work
'...' → literal text
```

When in doubt, quoting variables is usually a good habit:

```bash
echo "$name"
```

---

# Checking if a File Exists

```bash
if [[ -f "file.txt" ]]; then
    echo "File exists"
else
    echo "File doesn't exist"
fi
```

Useful file tests:

```text
-f    regular file exists
-d    directory exists
-e    something exists
-r    readable
-w    writable
-x    executable
```

Example:

```bash
if [[ -d "documents" ]]; then
    echo "Directory exists"
fi
```

---

# Comments

Comments are ignored by Bash.

Use:

```bash
# This is a comment
```

Example:

```bash
#!/bin/bash

# Ask for the user's name
read -p "Name: " name

# Say hello
echo "Hello $name"
```

Comments are useful for explaining **why** something is being done.

---

# A Small Complete Script

Putting several things together:

```bash
#!/bin/bash

# Ask for the user's name
read -p "What is your name? " name

# Ask for age
read -p "How old are you? " age

# Check the age
if [[ $age -ge 18 ]]; then
    echo "Hello $name, you are an adult."
else
    echo "Hello $name, you are under 18."
fi
```

Save it as:

```text
script.sh
```

Make it executable:

```bash
chmod +x script.sh
```

Run it:

```bash
./script.sh
```

---

# Bash Cheat Sheet

## Variables

```bash
name="John"
echo "$name"
```

## User input

```bash
read -p "Name: " name
```

## Arguments

```bash
$0    # script name
$1    # first argument
$2    # second argument
$#    # number of arguments
$@    # all arguments
```

## Command substitution

```bash
result=$(command)
```

## Arithmetic

```bash
result=$((2 + 3))
```

## Random number

```bash
echo "$RANDOM"
```

## If

```bash
if [[ condition ]]; then
    ...
elif [[ condition ]]; then
    ...
else
    ...
fi
```

## Case

```bash
case "$variable" in
    1)
        ...
        ;;
    2)
        ...
        ;;
    *)
        ...
        ;;
esac
```

## While

```bash
while [[ condition ]]
do
    ...
done
```

## For

```bash
for item in list
do
    ...
done
```

## Function

```bash
my_function() {
    echo "Hello"
}

my_function
```

## Exit status

```bash
echo $?
```

## Exit script

```bash
exit 0
```

---
