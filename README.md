

````markdown
# C Syntax Analyzer

A basic syntax analyzer (parser) for a fundamental subset of the C programming language, implemented purely in C. This project serves as a practical demonstration of core compiler design concepts, specifically **lexical analysis (tokenization)** and **syntax analysis (parsing)**.

## Features

This analyzer can process and validate the syntax of C code snippets that include:

* **Integer Variable Declarations:** `int variableName;`
* **Assignment Statements:** `variableName = expression;`
* **`if` Statements:** `if (condition_expression) { code_block }`
* **`while` Loops:** `while (condition_expression) { code_block }`
* **Arithmetic Expressions:** Supports addition (`+`), subtraction (`-`), multiplication (`*`), and division (`/`), correctly handling standard operator precedence.
* **Comparison Expressions:** Supports equality (`==`), less than (`<`), and greater than (`>`) operators for conditions.
* **Parenthesized Expressions:** Allows `(expression)` to override default operator precedence.
* **Code Blocks:** Groups statements and declarations within curly braces `{}`.
* **Error Detection:** Identifies and reports both lexical (unrecognized characters) and syntax (grammatical rule violations) errors.

## Supported C Grammar Subset (Simplified EBNF)

The analyzer is built to recognize and validate code following these rules:

```ebnf
program             -> (declaration | statement)* EOF
declaration         -> 'int' IDENTIFIER ';'
statement           -> assignment_statement | if_statement | while_statement
assignment_statement-> IDENTIFIER '=' expression ';'
if_statement        -> 'if' '(' expression ')' block
while_statement     -> 'while' '(' expression ')' block
expression          -> comparison_expression
comparison_expression -> additive_expression ( ( '==' | '<' | '>' ) additive_expression )*
additive_expression -> multiplicative_expression ( ( '+' | '-' ) multiplicative_expression )*
multiplicative_expression -> primary_expression ( ( '*' | '/' ) primary_expression )*
primary_expression  -> IDENTIFIER | NUMBER | '(' expression ')'
block               -> '{' (declaration | statement)* '}'
````

## How to Build and Run

### Prerequisites

  - A C compiler (e.g., GCC, MinGW, Clang).

### Steps

1.  **Save the code:** Save the `syntax_analyzer.c` file (which is the main C code for this project) into a directory on your computer.

2.  **Compile:** Open your terminal or command prompt, navigate to the directory where you saved `syntax_analyzer.c`, and compile the code using a C compiler (e.g., GCC):

    ```bash
    gcc syntax_analyzer.c -o syntax_analyzer
    ```

    This command will create an executable file named `syntax_analyzer` (or `syntax_analyzer.exe` on Windows).

3.  **Run:** Execute the compiled program from your terminal:

    ```bash
    ./syntax_analyzer
    ```

    (On Windows, you might typically just type `syntax_analyzer.exe` or `syntax_analyzer`).

4.  **Provide Input:** The program will prompt you to enter C code. Type your code, and then signal the end of input by:

      * Pressing `Enter` twice (leaving an empty line), OR
      * Pressing `Ctrl+Z` (on Windows) or `Ctrl+D` (on Unix/Linux/macOS) followed by `Enter`.

    The analyzer will then process your input and print messages indicating the parsed constructs or any detected errors.

## Example Input (Parses Successfully)

You can copy and paste this code when the analyzer prompts for input:

```c
int num1;
int num2;
int result;

num1 = 10;
num2 = num1 + 5 * (2 / 1); // num2 will be 10 + 5 * 2 = 20

if (num2 == 20) {
    result = num2 - 7; // result will be 13
    int temp_var;
    temp_var = result + num1; // temp_var will be 13 + 10 = 23
}

while (num1 < 15) {
    num1 = num1 + 1;
    if (num1 > 12) {
        num2 = num2 - 1;
    }
}

result = num1 * num2; // Final calculation
```

## Example Input (Expected Errors)

Try these inputs to see how the error handling works:

### 1\. Missing Semicolon

```c
int value
value = 10;
```

*Expected Error:* `Syntax Error: Expected a semicolon ';', but found 'value' (Type: 3) at position ...`

### 2\. Invalid Character (Lexical Error)

```c
int x;
x = 5 # 3; // '#' is not a recognized operator
```

*Expected Error:* `Lexical Error: Unexpected character '#' at position ...`

### 3\. Missing Closing Parenthesis in `while` Condition

```c
int counter;
counter = 0;
while (counter < 10 { // Missing ')'
    counter = counter + 1;
}
```

*Expected Error:* `Syntax Error: Expected a closing parenthesis ')', but found '{' (Type: 9) at position ...`

## Contribution

Contributions, issues, and feature requests are welcome\! Feel free to fork the repository and submit pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE](https://www.google.com/search?q=LICENSE) file for details.

```
```
