Absolutely, Thierno! Here's a markdown version of the comprehensive bash scripting documentation. This includes both basic and more advanced topics, structured to be readable and well-organized for GitHub.

markdown
Copy code
# Bash Scripting Comprehensive Guide

## Table of Contents
1. [Introduction to Bash Scripting](#introduction-to-bash-scripting)
2. [Variables](#variables)
3. [Conditionals](#conditionals)
4. [Loops](#loops)
5. [Functions](#functions)
6. [Input and Output](#input-and-output)
7. [File Operations](#file-operations)
8. [Intermediate and Advanced Concepts](#intermediate-and-advanced-concepts)
9. [Practice Examples](#practice-examples)

---

## Introduction to Bash Scripting

Bash (Bourne Again SHell) is a Unix shell and command language. A bash script is a file containing a series of commands that are executed sequentially by the bash shell. Bash scripts can automate tasks, manipulate files, and more.

### Creating a Bash Script
1. Open a text editor (e.g., `nano`, `vim`).
2. Write your script.
3. Save the file with a `.sh` extension (e.g., `myscript.sh`).
4. Make the script executable:
   ```sh
   chmod +x myscript.sh
Run the script:
sh
Copy code
./myscript.sh
Variables
Variables in bash are used to store data that can be used later in the script.

Syntax
sh
Copy code
variable_name=value
Examples
sh
Copy code
#!/bin/bash

# Define a variable
greeting="Hello, World!"

# Print the variable
echo $greeting
Special Variables
$0: The name of the script.
$1, $2, ...: Positional parameters (arguments to the script).
$#: The number of positional parameters.
$@: All positional parameters as separate words.
$*: All positional parameters as a single word.
$?: The exit status of the last command.
$$: The process ID of the current shell.
Conditionals
Conditionals allow you to execute code based on certain conditions.

if Statement
sh
Copy code
if [ condition ]; then
    # code to execute if condition is true
fi
if-else Statement
sh
Copy code
if [ condition ]; then
    # code to execute if condition is true
else
    # code to execute if condition is false
fi
if-elif-else Statement
sh
Copy code
if [ condition1 ]; then
    # code to execute if condition1 is true
elif [ condition2 ]; then
    # code to execute if condition2 is true
else
    # code to execute if no condition is true
fi
Examples
sh
Copy code
#!/bin/bash

number=10

if [ $number -gt 5 ]; then
    echo "The number is greater than 5."
else
    echo "The number is 5 or less."
fi
Loops
Loops allow you to execute code multiple times.

for Loop
sh
Copy code
for variable in list; do
    # code to execute
done
Examples
sh
Copy code
#!/bin/bash

for i in 1 2 3 4 5; do
    echo "Number: $i"
done
while Loop
sh
Copy code
while [ condition ]; do
    # code to execute
done
Examples
sh
Copy code
#!/bin/bash

count=1

while [ $count -le 5 ]; do
    echo "Count: $count"
    ((count++))
done
until Loop
sh
Copy code
until [ condition ]; do
    # code to execute
done
Examples
sh
Copy code
#!/bin/bash

count=1

until [ $count -gt 5 ]; do
    echo "Count: $count"
    ((count++))
done
Functions
Functions allow you to group code into reusable blocks.

Syntax
sh
Copy code
function_name() {
    # code to execute
}
Examples
sh
Copy code
#!/bin/bash

greet() {
    echo "Hello, $1!"
}

greet "Thierno"
Input and Output
Reading User Input
sh
Copy code
#!/bin/bash

echo "Enter your name:"
read name
echo "Hello, $name!"
Outputting Data
echo: Print to the terminal.
printf: More control over formatting.
Examples
sh
Copy code
#!/bin/bash

echo "Hello, World!"
printf "Hello, %s!\n" "Thierno"
File Operations
Checking if a File Exists
sh
Copy code
if [ -e filename ]; then
    echo "File exists."
fi
Reading a File Line by Line
sh
Copy code
while IFS= read -r line; do
    echo "$line"
done < filename
Writing to a File
sh
Copy code
echo "This is a line of text." > filename
Appending to a File
sh
Copy code
echo "This is another line of text." >> filename
Examples
sh
Copy code
#!/bin/bash

# Check if a file exists
if [ -e myfile.txt ]; then
    echo "File exists."
else
    echo "File does not exist."
fi

# Write to a file
echo "This is a line of text." > myfile.txt

# Append to a file
echo "This is another line of text." >> myfile.txt

# Read from a file
while IFS= read -r line; do
    echo "$line"
done < myfile.txt
Intermediate and Advanced Concepts
Error Handling
Use set -e to make your script exit when a command fails.

sh
Copy code
#!/bin/bash
set -e

# Your script here
Debugging
Use set -x to enable debug mode.

sh
Copy code
#!/bin/bash
set -x

# Your script here
Arrays
Arrays store multiple values in a single variable.

sh
Copy code
#!/bin/bash

# Define an array
my_array=("one" "two" "three")

# Access array elements
echo ${my_array[0]} # one
echo ${my_array[1]} # two

# Loop through array elements
for element in "${my_array[@]}"; do
    echo $element
done
Advanced Loops
Loop through files in a directory.

sh
Copy code
#!/bin/bash

for file in /path/to/directory/*; do
    echo "Processing $file"
done
Case Statement
A case statement is used for multi-way branching.

sh
Copy code
#!/bin/bash

echo "Enter a number between 1 and 3:"
read number

case $number in
    1)
        echo "You entered one."
        ;;
    2)
        echo "You entered two."
        ;;
    3)
        echo "You entered three."
        ;;
    *)
        echo "Invalid number."
        ;;
esac
Network Configuration Example
Configure a network interface using nmcli.

sh
Copy code
#!/bin/bash

echo "Enter the interface name:"
read ifname

nmcli con add type ethernet ifname $ifname con-name my-connection ipv4.method auto

if [ $? -eq 0 ]; then
    nmcli con up my-connection
    systemctl restart NetworkManager
    echo "Network configuration applied successfully."
else
    echo "Failed to configure the network. Please check your input."
fi
Practice Examples
Example 1: Simple Calculator
sh
Copy code
#!/bin/bash

echo "Enter first number:"
read num1
echo "Enter second number:"
read num2

echo "Choose operation (+ - * /):"
read op

case $op in
    +) result=$((num1 + num2)) ;;
    -) result=$((num1 - num2)) ;;
    \*) result=$((num1 * num2)) ;;
    /) result=$((num1 / num2)) ;;
    *) echo "Invalid operation"; exit 1 ;;
esac

echo "Result: $result"
Example 2: File Backup
sh
Copy code
#!/bin/bash

echo "Enter the filename to back up:"
read filename

if [ -e $filename ]; then
    cp $filename ${filename}.bak
    echo "Backup created: ${filename}.bak"
else
    echo "File does not exist."
fi
Example 3: Loop through Files
sh
Copy code
#!/bin/bash

for file in /path/to/directory/*; do
    echo "Processing $file"
done
Example 4: User Management Script
sh
Copy code
#!/bin/bash

echo "Enter username to add:"
read username

sudo useradd $username

if [ $? -eq 0 ]; then
    echo "User $username added successfully."
else
    echo "Failed to add user $username."
fi
Example 5: Disk Usage Monitoring
sh
Copy code
#!/bin/bash

threshold=80
df -h | awk '$5 > threshold {print $0}' threshold=$threshold
