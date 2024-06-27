# 0x19. C - Stacks, Queues - LIFO, FIFO

## Overview

This project involves implementing stacks and queues using C. The stack follows a Last In, First Out (LIFO) principle, while the queue follows a First In, First Out (FIFO) principle. The primary goal is to create an interpreter for Monty ByteCodes files, which are used to manipulate a unique stack with specific instructions.

## Requirements

### General
- **Editors**: vi, vim, emacs
- **Compilation**: Ubuntu 20.04 LTS with gcc using `-Wall -Werror -Wextra -pedantic -std=c89`
- **Files**: All files should end with a new line
- **Code Style**: Use the Betty style, checked with `betty-style.pl` and `betty-doc.pl`
- **Global Variables**: Only one allowed
- **Functions per File**: Maximum of 5
- **Libraries**: C standard library allowed
- **Prototypes**: Include in `monty.h`
- **Header Files**: Include guards required
- **Task Order**: Complete tasks in order shown

### GitHub
- One project repository per group
- Cloning/forking a project repository with the same name before the second deadline may result in a 0% score

## Data Structures

### Stack and Queue Representation
```c
/**
 * struct stack_s - doubly linked list representation of a stack (or queue)
 * @n: integer
 * @prev: points to the previous element of the stack (or queue)
 * @next: points to the next element of the stack (or queue)
 *
 * Description: doubly linked list node structure
 * for stack, queues, LIFO, FIFO
 */
typedef struct stack_s
{
    int n;
    struct stack_s *prev;
    struct stack_s *next;
} stack_t;
```

### Opcode and Function
```c
/**
 * struct instruction_s - opcode and its function
 * @opcode: the opcode
 * @f: function to handle the opcode
 *
 * Description: opcode and its function
 * for stack, queues, LIFO, FIFO
 */
typedef struct instruction_s
{
    char *opcode;
    void (*f)(stack_t **stack, unsigned int line_number);
} instruction_t;
```

## Compilation & Output
Compile the code with:
```bash
$ gcc -Wall -Werror -Wextra -pedantic -std=c89 *.c -o monty
```

### Output
- Printed on `stdout`
- Errors printed on `stderr`

## Tests
- Collaboration on tests is strongly encouraged

## The Monty Language
Monty 0.98 is a scripting language that compiles into Monty byte codes. These codes manipulate a stack with specific instructions.

### Monty Byte Code Files
- **Extension**: `.m` (not mandatory)
- **Instruction Format**: One instruction per line, spaces before/after the opcode and its argument are allowed

### Example Byte Code File
```bash
push 0$
push 1$
push 2$
  push 3$
                   pall    $
push 4$
    push 5    $
      push    6        $
pall$
```

### Blank Lines and Comments
- Files can contain blank lines or comments after the opcode or argument

### Example with Comments
```bash
push 0 Push 0 onto the stack$
push 1 Push 1 onto the stack$
$
push 2$
  push 3$
                   pall    $
$
$
                           $
push 4$
$
    push 5    $
      push    6        $
$
pall This is the end of our program. Monty is awesome!$
```

## The Monty Program
### Usage
```bash
monty file
```
- `file`: Path to the file containing Monty byte code

### Error Handling
- **No File/Multiple Arguments**: Print `USAGE: monty file` and exit with `EXIT_FAILURE`
- **File Open Error**: Print `Error: Can't open file <file>` and exit with `EXIT_FAILURE`
- **Invalid Instruction**: Print `L<line_number>: unknown instruction <opcode>` and exit with `EXIT_FAILURE`
- **Malloc Failure**: Print `Error: malloc failed` and exit with `EXIT_FAILURE`

### Execution
- Runs bytecodes line by line
- Stops on error or after executing all lines

## Example `monty.h`
Include the required data structures and function prototypes.

```c
#ifndef MONTY_H
#define MONTY_H

#include <stdlib.h>
#include <stdio.h>
#include <string.h>

/* Data Structures */
typedef struct stack_s
{
    int n;
    struct stack_s *prev;
    struct stack_s *next;
} stack_t;

typedef struct instruction_s
{
    char *opcode;
    void (*f)(stack_t **stack, unsigned int line_number);
} instruction_t;

/* Function Prototypes */
void push(stack_t **stack, unsigned int line_number, int n);
void pall(stack_t **stack, unsigned int line_number);
void free_stack(stack_t *stack);

#endif /* MONTY_H */
```

This project emphasizes the understanding and implementation of stack and queue data structures in C, following the Monty language specifications and ensuring compliance with the provided requirements and coding standards.
