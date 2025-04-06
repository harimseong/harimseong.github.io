---
layout: post
title: "Compiler Frontend Basic"
date: 2025-04-06 21:09:07 +0900
categories: parser
---

## Introduction

Compiler translates source code to target code. During the compiling process, compiler must preserve intentions represented in source code. If it does not produce correct output, target code will have unexpected behaviors. Compiler frontend is a part that read and analyze the source code, then generate intermediate representation (IR) that compiler uses for following processes such as code optimization and generation.

___
## Lexer

Lexer, scanner or tokenizer is first stage of the compiler frontend. Source code is just a collection of characters that need to be processed. Result of the lexer is **token**. It consists of characters and token type. Next stage, parser, represents grammar and uses tokens to find if input has valid structure.

### Regular expression

Purpose of the lexer is generating tokens, so tokens need to be defined first. Regular expression (RE) can define the token effectively.

#### Basic Operations

There are three basic operations for RE.

##### 1. Alternation `a|b`
It is similar to `OR` operation. A pattern `a|b` allows the lexer to recognize pattern `a` or `b`.

##### 2. Concatenation `ab`
A pattern consists of more than one characters are represented as consecutive characters. This is as simple as it sounds. A pattern `a|ab` allows `a` and `ab`.

##### 3. Closure `a*`
It represents zero or more occurance of a pattern. `a*` can match empty pattern, `a`, `aa`, `aaa` and infinite amount of consecutive `a`.

Parenthesis and other operations are used to define more complex RE. 

### Deterministic Finite Automata
Finite automata or finite state machine can be derived from the RE. Nondeterministic finite automata (NFA) is constructed from RE and deterministic finite automate (DFA) is constructed from NFA. 

DFA is special case of NFA. Given a state and a character, NFA allows multiple state transitions but DFA allows only one transition.

#### Definition of DFA
- starting state
- accepting state
- set of finite states
- set of finite characters
- transition functions

___
## Parser
In data-oriented perspective, lexer takes characters and gives tokens. Parser takes tokens and gives IR. Abstract syntax trees (AST) are common form of IR.

### Context-Free Grammar (CFG)
CFG is efficient notation to describe programming language syntax.
It consists of a set of rules that defines sentences that belong to a language.

#### Backus-Naur Form (BNF)
BNF is traditional notation to represent CFG.
```
<start>      ::= <expression> ; <start>
              |  <expression>
<expression> ::= <number> <op> <expression>
              |  <number> <op> <number>
<number>     ::= (1-9)(0-9)*
<op>         ::= (+|-)
```

### Top-down parser (LL parser)
Find matching sentence from left to right, top-down. From BNF example, first sentence LL parser recognizes is `<start>` then `<expression>`.

#### Recursive Descent Parser (RDP)
- easier to add syntax error messages.
- efficient if CFG is backtrack-free and does not have left recursion.
- flexible as it is hand wrote.

#### Backtrack-free


#### Left Recursion
If `<start>` sentence is defined as `<start> ; <expression>`, parser will fall into infinite recursion of `<start>`.
