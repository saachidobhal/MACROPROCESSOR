
# Two-Pass-Macro-Processor
A macro processor is a program that copies a stream of text from one place to another, making a systematic set of replacements as it does so. Macro processors are often embedded in other programs, such as assemblers and compilers. Sometimes they are standalone programs that can be used to process any kind of text.   
  
Macro processors have been used for language expansion (defining new language constructs that can be expressed in terms of existing language components), for systematic text replacements that require decision making, and for text reformatting.
## Language Used
- C
- Assembly (for input)
## Data Structures
- MACRO Definition table
- MACRO Name Table
- Argument Array List 
## Format of Data Structures
### MACRO Definition Table
| Index|      Definition      |  Arguments |
|----------|:-------------:|------:|
| 1 |  INCR  | &arg1, &arg2 |
|2 |    A   |   #1 |
|3 | A | #2 |
|4 | MEND| |
> Note: Argument list contains the index of the argument in the argument list array.
 ### MACRO Name Table
| Index|      Name      |  MDT Index |
|----------|:-------------:|------:|
| 1 |  "INCR"  | 1 |

> Note: MDT index contains the starting index of the MACRO in MDT.
 ### Argument List Array
| Index|      Argument      | 
|----------|:-------------:|
| 1 |  "DATA 1bbb"  |
| 2 | "DATA 2bbb" |

> Note: MDT index contains the starting index of the MACRO in MDT.
## Pass 1 (Definition of MACROS)
- Pass1 of macro processor makes a line-by-line scanover it's input.
- Set MDTC = 1 and MNTC = 1.
- Read next line of input program.
- If it is a MACRO pseudo-op, the entire macro definition except MACRO line is stored in MDT.
- The name is entered in the MNT along with a pointer to the 1st location of MDT entry.
- When the END pseudo-op is encountered all the macro-definitions have been processed, so control is transferred to pass2.
## Pass 2 (Replacing MACRO calls by its definition)
- This algorithm reads one line of i/p program at a time.
- For each line it checks if op-code of that line matches any of the MNT entry.
- The initial value of MDTP is obtained from MDT index field of MNT entry.
- The macro expander prepares the ALA consisting of a table of dummy argument indices and corresponding arguments to the call.
- The value from the argument list is substituted for dummy arguments indices in the macro definition table.
- Reading MEND line in MDT terminates expantion of macro and scanning continues in the input file.
- When END pseudo-op is encountered, the expanded source program is given to the assembler.
