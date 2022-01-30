# Introduction to Computer Science (YSC1212)

1. Week 01
2. Week 02
3. Week 03



# Week 01

Key Topics:

- Aristotle's four cases
- Background and general introduction
- Exploring one's computer with Emacs
- Language and language processors
- Precision
- Bootstrapping



## Aristotle's four causes

- Material Cause
  - What is the object of discourse
  - What are we talking about
- Efficient Cause
  - What is done to it?
  - Who is doing it?
- Formal Cause
  - What methods are used to do that
- Final Cause
  - Towards what goal?
  - Why is this done?
  - What for?



## Background and general introduction

- Data represents information and is built using data constructors
  - Representation is sound when using constructors correctly always yields a piece of data that correctly represents the information it is meant to represent
- Programs:
  - Recipe computer executes to process data
  - Computes a function from input information to output information
- Programming Languages:
  - Language in which a program is written
  - Notation to express computations
- Computer:
  - Yields output data
  - Issue an error message
  - Loop; Not produce any output data



## Language and language processors

- Meta-language:
  - Language to talk about another language
- Programming language:
  - Language in which a program is written
  - A notation to express computations
- Interpreters:
  - An interpreter is basically a program to execute another program
  - It is written in a meta-language, also known as an implementation language
  - It is depicted with an I diagram
  - Whereby S is Source, M is implementation (meta)

![_images/ditaa-a95feb256bad9462ac5cf844432040d1a14fbf07.png](https://delimited-continuation.github.io/YSC1212/2021-2022_Sem2/_images/ditaa-a95feb256bad9462ac5cf844432040d1a14fbf07.png)

- Microprocessors:
  - Interpreters for programs that are written in assembly language, and implemented in hardware
- Virtual machines:
  - Interpreters for programs that are implemented in software
- Compilers:
  - A program for translating another program from one language to another language
  - Given a source program, a compiler produces a target program
  - Compilers preserve the meaning of the programs they translate
  - Target programs mean the same in the sense that executing either does the same as the other

![_images/ditaa-7822f155e36df5699f9241f11ae432681e7d373d.png](https://delimited-continuation.github.io/YSC1212/2021-2022_Sem2/_images/ditaa-7822f155e36df5699f9241f11ae432681e7d373d.png)

- Compiler Design:
  - S - Source
  - T - Target language of compiled program
  - I - Implementation language

![_images/ditaa-fb57942f36b870823aa58478afe4a1feb91dc621.png](https://delimited-continuation.github.io/YSC1212/2021-2022_Sem2/_images/ditaa-fb57942f36b870823aa58478afe4a1feb91dc621.png)

- Compiling Interpreter:
  - The input of the compiler is a program written in C, and therefore the output is a program written in A since the compiler translates programs from C to A. 
  - The input of the compiler is an interpreter for Scheme, and therefore the output is also an interpreter for Scheme since a compiler preserves the meaning of the programs it translates. 
  - Therefore since the input is an interpreter for Scheme written in C, the output is an interpreter for Scheme written in A.
- Notes:
  - Executing a program and running a program are used interchangeably
  - Executing program with interpreter:
    - Proceeds in one step
  - Executing program with compiler:
    - Proceeds in two steps
    - First Step: program is compiled, translated into a compiled program
      - Called Compile Time
    - Second Step: compiled program is executed
      - Called Run Time
- Compiler Efficiency:
  - If a compiler is efficient, compile time is short
  - If a compiler generates efficient code, the subsequent run time is short
- Self-Interpreters and Self-Compilers:
  - Self-Interpreters:
    - When interpreter written in a subset of its source language, it can interpret a copy of itself
    - An interpreter that can interpret a copy of itself is called a self-interpreter
  - Self-Compilers:
    - A compiler that can compile a copy of itself is called a self-compiler
    - Input of the compiler is a program written in L
    - Output of compiler is a program written in A, since the compiler translates from L to A
      - Since compiler preserves the meaning of the programs it translates
    - In the diagram, input is program from L to A, output is program from L to A
      - And in the input, it is written in L, so the compiler written in L is passed through compiler that accepts input language of L, and spits out output language of A
      - Thus, the compiled compiler is written in A, but still has the program from L to A

![_images/ditaa-795f0845c76302cdd0e40e06092510421d78e608.png](https://delimited-continuation.github.io/YSC1212/2021-2022_Sem2/_images/ditaa-795f0845c76302cdd0e40e06092510421d78e608.png)



### Precision

- Program is something written in a programming language
- Compiler translates a program from one programming language to another
- Do not say that compilers compile programming language, be more precise, don't use pleonasms



### Bootstrapping

- Writing an efficient ML Compiler:
  - Assume we have an executable compiler from C to Assembly, written in x86, as well as a byte-code interpreter for A, written in x86
  - Create throw-away compiler from ML to A, written in C
    - It is inefficient compile time, and inefficient run time (code)
    - Using our compiler, convert ML to A compiler written in C, to ML to A compiler written in A
    - It is still inefficient compile time, and inefficient run time (code)
  - Create ML to A compiler, written in ML
    - This compiler has efficient compile time and efficient run time (code)
    - Using our new compiler, convert ML to A compiler written in ML, to ML to A compiler in A
    - Using interpreter for A, written in x86
    - Now new compiler is inefficient compile time, but runs efficient code
  - Using new compiler, ML to A compiler written in A
    - This compiler is the same, it is inefficient compile time but runs efficient code
    - Convert ML to A compiler written in ML, to ML to A compiler written in A
    - Using interpreter for A, written in x86
- Compilers should have:
  - Compile Time (how fast program takes to compile)
  - Run Time (when the compiled program is executed)





## Week 02

Key Topics:

- Kleene's S-m-n Theorem
- Computational Paradigms
- Finite description of arbitrarily large data
- Syntax of regular expressions



## Syntax of regular expressions

