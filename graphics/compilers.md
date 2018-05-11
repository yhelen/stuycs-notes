# Compilers

```
             compiler
source code ---------> executable code
```

## Compiler Parts

1. lexer
2. syntactic analyzer
3. semantic analyzer
4. optimizer (not always present)
5. code generator

| Name                      | Input                        | Output                                 |
| ------------------------- | ---------------------------- | -------------------------------------- |
| lexer                     | source code                  | token list                             |
| parser/syntactic analyzer | token list                   | syntax tree                            |
| semantic analyzer         | syntax tree                  | operation list, symbol table           |
| optimizer                 | operation list, symbol table | optimized operation list, symbol table |
| code generator            | operation list, symbol table | binary executable                      |

## Lexer

* Performs lexical analysis.
* "Knows" all valid tokens in a language
    * string literals
    * operators
    * formating characters
    * keywords
    * numeric literals
    * identifiers (functions, variables)
* Reads in source code and outputs a token list

Lexers:

* c: lex, flex
* java: javacc*

## Parser

* Perform syntax analysis.
* Checks the token list against the defined structure (grammar)
  of the language
* Output is a syntax tree
* tools:
    * C: yacc, bison

```
E.g.
token list:
int
main
(
)
{
long
x
=
5
+
6
;
printf
(
"%d"
,
x
)
;
}
            int  main
        /       |      \
        =      printf   return
      /   \     /   \      \
long x    +   "%d"   x      x
         / \
        5   6
```

## Semantic Analyzer

* Evaluates the syntax tree and creates an operation list and
  symbol table (stores identifiers and associated information).
* If the language is typed, type-checking will occur here.
* The semantic analyzer does NOT evaluate expressions.

**Tree Traversal Types**

* post: L -> R -> M
* pre: M -> L -> R
* in: L -> M -> R

**Operation List**

| Number | Operation | Arguments |
| ------ | --------- | --------- |
| 0      | +         | 5, 6      |
| 1      | =         | x, (0)    |
| 2      | return    | x         |

**Symbol Table**

| Symbol | Category | Type |
| ------ | -------- | ---- |
| main   | function | int  |
| x      | value    | long |
| printf | function | int  |
