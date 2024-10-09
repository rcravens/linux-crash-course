# Chapter 11: Basic Shell Scripting

<a href="README.md">&laquo; main menu</a>

## 11.1 Introduction to Shell Scripting
- **What is Shell Scripting?**
  - Shell scripting is the process of writing scripts to automate tasks and manage system operations using a command-line interpreter, or shell.
  - The most commonly used shell is Bash (Bourne Again Shell), but other shells like Sh (Bourne Shell) and Zsh (Z Shell) are also popular.
- **Why Use Shell Scripts?**
  - **Automation**: Automate repetitive tasks such as backups, system monitoring, and data processing.
  - **Efficiency**: Simplify complex sequences of commands into a single executable file.
  - **Consistency**: Ensure that tasks are performed the same way each time by using a script.

## 11.2 Writing Your First Shell Script
- **Creating a Script File**
  - Open a terminal and use a text editor to create a new file. For example:
    ```bash
    nano script.sh
    ```
  - Start the file with the shebang line to specify the interpreter:
    ```bash
    #!/bin/bash
    ```
    - The shebang (`#!`) tells the system which interpreter to use to execute the script.
- **Example Script**
  ```bash
  #!/bin/bash
  echo "Hello, World!"
  
Explanation: This simple script prints “Hello, World!” to the terminal.
- **Making the Script Executable**

•	Change the file permissions to make it executable: `chmod +x script.sh`

•	Run the script by typing: `./script.sh`

•	Note: The ./ is used to run scripts and executables in the current directory.

## 11.3 Basic Scripting Constructs

- **Variables**
  - **Syntax**: `variable_name=value`
  - Example:
    ```bash
    greeting="Hello, World!"
    ```
  - Accessing variables:
    ```bash
    echo $greeting
    ```
  - **Explanation**: This prints the value of the `greeting` variable.
  - **Best Practices**:
    - Use meaningful names.
    - Enclose values in quotes to handle spaces or special characters.

- **Comments**
  - **Syntax**: `# This is a comment`
  - Comments are used to explain code and are ignored during execution.
  - Example:
    ```bash
    # This script prints a greeting
    echo "Hello, World!"
    ```

- **Conditional Statements**
  - **Syntax**:
    ```bash
    if [ condition ]; then
        # commands
    elif [ another_condition ]; then
        # commands
    else
        # commands
    fi
    ```
  - Example:
    ```bash
    if [ -f /etc/passwd ]; then
        echo "File exists."
    else
        echo "File does not exist."
    fi
    ```
  - **Explanation**: This script checks if the file `/etc/passwd` exists and prints a message based on the result.
  - **Common Conditions**:
    - `-f file`: True if the file exists and is a regular file.
    - `-d directory`: True if the directory exists.
    - `-e file`: True if the file exists (any type).

- **Loops**
  - **For Loop**:
    ```bash
    for i in {1..5}; do
        echo "Number $i"
    done
    ```
  - **While Loop**:
    ```bash
    counter=1
    while [ $counter -le 5 ]; do
        echo "Count $counter"
        ((counter++))
    done
    ```
  - **Explanation**:
    - The `for` loop iterates through a sequence of numbers.
    - The `while` loop continues as long as the condition is true, incrementing the `counter` variable each iteration.
  - **Use Cases**:
    - Use `for` loops for a fixed number of iterations.
    - Use `while` loops for conditions that may change dynamically.

- **Functions**
  - **Syntax**:
    ```bash
    function_name() {
        # commands
    }
    ```
  - Example:
    ```bash
    greet() {
        echo "Hello, $1!"
    }
    greet "Alice"
    ```
  - **Explanation**: Defines a function `greet` that takes one argument (`$1`) and prints a greeting.
  - **Function Parameters**: Parameters are accessed using `$1`, `$2`, etc.
  - **Returning Values**: Shell functions do not return values directly. Use `echo` to output results and capture them.

## 11.4 Handling Input and Output

- **Reading User Input**
  - Use the `read` command to get input from the user:
    ```bash
    echo "Enter your name:"
    read name
    echo "Hello, $name!"
    ```
  - **Explanation**:
    - The `echo` command prompts the user to enter their name.
    - The `read` command waits for the user to input their name and stores it in the variable `name`.
    - The second `echo` command outputs a personalized greeting using the value stored in `name`.

- **Redirecting Output**
  - **Standard Output**: Redirect output to a file, overwriting the file:
    ```bash
    echo "Log entry" > log.txt
    ```
    - **Explanation**: The `>` operator redirects the output of the `echo` command to `log.txt`, overwriting any existing content in the file.
  - **Appending Output**: Append output to a file:
    ```bash
    echo "Log entry" >> log.txt
    ```
    - **Explanation**: The `>>` operator appends the output of the `echo` command to `log.txt`, preserving the existing content and adding new content at the end.
  - **Standard Error**: Redirect error messages to a file:
    ```bash
    ls /nonexistent_directory 2> error.log
    ```
    - **Explanation**: The `2>` operator redirects the standard error (file descriptor 2) of the `ls` command to `error.log`, capturing any error messages generated by the command.

## 11.5 Basic Error Handling

- **Exit Status**
  - Each command returns an exit status code (`$?`), where `0` indicates success and non-zero indicates an error.
  - **Example**:
    ```bash
    ls /nonexistent_directory
    if [ $? -ne 0 ]; then
        echo "Directory not found."
    fi
    ```
  - **Explanation**:
    - The `ls` command attempts to list a non-existent directory.
    - The `$?` variable captures the exit status of the last command (`ls` in this case).
    - The `if` statement checks if the exit status is not equal to `0` (indicating an error) and prints "Directory not found." if true.

- **Handling Errors in Scripts**
  - Use `set -e` at the beginning of a script to exit on any command failure:
    ```bash
    #!/bin/bash
    set -e
    ls /nonexistent_directory
    echo "This will not be executed if the previous command fails."
    ```
  - **Explanation**:
    - The `set -e` command ensures that the script stops execution if any command fails (returns a non-zero exit status).
    - This is useful for scripts where you want to halt on errors to prevent further unintended actions.

## 11.6 Conclusion

Basic shell scripting provides a foundation for automating tasks and managing system operations. By learning to create scripts, use variables, control structures, loops, and handle input and output, you can significantly enhance your productivity and efficiency in a Linux environment.

- **Key Takeaways**:
  - **Variables**: Store and manipulate data.
  - **Comments**: Document and explain code.
  - **Conditional Statements**: Execute commands based on conditions.
  - **Loops**: Repeat commands multiple times.
  - **Functions**: Define reusable code blocks.
  - **Input and Output**: Handle user input and redirect output.

Practice these basics to build a strong foundation and prepare for more advanced scripting techniques in the next chapter.


<a href="README.md">&laquo; main menu</a>