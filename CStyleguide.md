

Initial version of a C style guide for likwid.

# Files #

## C1  File organization ##

  1. Include files always have the file name extension ".h".
  1. Implementation files always have the file name extension ".c".
  1. Machine dependent code has to be placed in a separate file.
  1. Modules shall be named all lowercase according to the module name.
  1. Source and belonging header files shall have the same name.
  1. Type definitions shall be declared in a file named `modulename_types.h`.
  1. All type headers are included wrapped by a single header file `types.h` .

## C2  File structure ##

  1. Every source file shall have the following structure:
    * File Header
    * System Includes
    * Local Includes
    * Macro Definitions
    * Local Type Definitions
    * Local Function Prototypes
    * Global Constant Definitions
    * Global Variable Definitions
    * Module Constant Definitions
    * Module Variable Definitions
    * Global and local Function Definitions

  1. Every header file shall have the following structure:
    * File Header
    * System Includes
    * Local Includes
    * Macro Definitions
    * Type Definitions
    * Global Constant Declarations
    * Global Variable Declarations
    * Global Function Declarations

  1. The source/header file header shall be as follows

```
    ===========================================================================
    
         Filename:  test.c
    
         Description:  Implementation of test module.
    
         Version:  <VERSION>
         Created:  <DATE>
    
         Author:  Jan Treibig (jt), jan.treibig@gmail.com
         Company:  RRZE Erlangen
         Project:  likwid
         Copyright:  Copyright (c) 2010, Jan Treibig
    
         This program is free software; you can redistribute it and/or modify
         it under the terms of the GNU General Public License, v2, as
         published by the Free Software Foundation
        
         This program is distributed in the hope that it will be useful,
         but WITHOUT ANY WARRANTY; without even the implied warranty of
         MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
         GNU General Public License for more details.
        
         You should have received a copy of the GNU General Public License
         along with this program; if not, write to the Free Software
         Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.
    
    ===========================================================================
```

  1. The public API and all enums, structs or typedefs shall be documented using doxygen.


# Code #

## C3  Code formatting ##

  1. Maximum line length is 78 characters.
  1. Language for specifiers and comments is in US English only.
  1. Braces enclosing a block are to be placed in the same column, on separate lines directly before and after the block.
  1. Comments shall use `/*  */` .
  1. After an opening brace the code is indented.
  1. Indent depth is always 4.
  1. Indent is always using spaces, NO tabs.
  1. The flow control primitives if, else, while, for and do should always be followed by a block.
  1. The dereference operator `*` and the address-of operator `&` should be directly connected with the type names in declarations and definitions.
  1. Every declaration has to be a separate statement.
  1. Do not use spaces around `.` or `->`, nor between unary operators and operands.
  1. Put spaces around binary operators and operands.
  1. Every statement shall be on a separate line.

Example:
```
    int* source;

    if (i < 0)
    {
        A[i] = 1;
    }
```

### C3.A Functions ###

  1. Always provide the return type of a function explicitly.
  1. When declaring functions, the leading parenthesis and the first argument  are to be written on the same line as the function name.
  1. Other arguments and the closing parenthesis have be written on the same line as the function name.
  1. If not all arguments fit in one line each additional argument is to be written on a separate line (with the closing parenthesis directly after the last argument).
  1. In a function definition, the return type of the function should be written on a separate line directly above the function name.
  1. Always write the left parenthesis directly after a function name.

Example:
```
    void testFunction( int, double*, double);

    void
    testFunction( int i,
                  double* A,
                  double* B,
                  double* C,
                  int size)
    {
```

## C4  Naming conventions ##

  1. The identifier of every globally symbol has to begin with a prefix that is unique to the module.
  1. The module prefix consists of the uppercase module name and is separated by one underscore.
  1. The names of variables, constants, and functions are to begin with a lowercase letter.
  1. In names which consist of more than one word, the words are written together and each word that follows is begun with an uppercase letter.
  1. Apart from suffixes and prefixes Symbol names should not contain underscores.
  1. Names should not include abbreviations that are not generally accepted.
  1. The names of structures and enumerated types and their typedefs are to begin with an uppercase letter.
  1. All other typedefs shall be lowercase with a `_t` suffix.
  1. Macro names are all uppercase.


## C6 Coding style ##

  1. Definitions of variables and functions are always in c files.
  1. The visibility of variables and types has to be as restricted as possible.
  1. Every global function prototypes must be declared with `extern` in include files.
  1. Local function prototypes are declared with `static` in c files.
  1. No argument names shall be specified in prototypes.
  1. A function without argument shall explicitly use void in the argument list.

### C6.A Include files ###

  1. Every include file must contain a mechanism that prevents multiple inclusions of the file.
  1. All includes shall use the directive `#include <filename.h>`.
  1. An include directive shall not contain a path.

Technique for preventing multiple inclusion of an include file:
```
    #ifndef FOO_H
    #define FOO_H
      /*The rest of the file*/
    #endif /* FOO_H */
```