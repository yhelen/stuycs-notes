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

| Name                        | Input       | Output     |
| --------------------------- | ----------- | ---------- |
| lexer                       | source code | token list |
| parser (syntactic analyzer) |             |            |

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
