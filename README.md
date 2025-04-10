## 1. Book Component with Service

```c
%{
#include <stdio.h>
%}

%%
[" "]                  ; // Ignore whitespace
"//".*                    ; // Ignore single-line comment
.                         { printf("%s", yytext); } // Print everything else
%%

int main() {
    yylex();
    return 0;
}
```
## Input
```
Pavan G
```
## Output
```
PavanG
```

## 2. Construct a recursive descent parser for simple arithmetic expressions.

```c
#include <stdio.h>
#include <ctype.h>

const char *input;
char lookahead;

void error() {
    printf("Syntax Error\n");
    
}
void match(char token) {
    if (lookahead == token) {
        lookahead = *++input; // Move to the next character
    } else {
        error();
    }
}

// Recursive functions for grammar rules
void E();  // Expression
void EPrime();  // Expression Tail
void T();  // Term
void TPrime();  // Term Tail
void F();  // Factor

void E() {
    T();
    EPrime();
}

void EPrime() {
    if (lookahead == '+') {
        match('+');
        T();
    }
}

void T() {
    F();
    TPrime();
}

void TPrime() {
    if (lookahead == '*') {
        match('*');
        F();
    }
}

void F() {
    if (isdigit(lookahead)) {
        match(lookahead);
    } else {
        error();
    }
}

int main() {
    char expression[100];
    printf("Enter an arithmetic expression: ");
    scanf("%s", expression);
    input = expression;
    lookahead = *input;
    
    E();
    if (lookahead == '\0') {
        printf("Parsing Successful!\n");
    } else {
        error();
    }

    return 0;
}

```
## Input
```
2+3*4
```
## Output
```
Parsing Successful!
```
---
