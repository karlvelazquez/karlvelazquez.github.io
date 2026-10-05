# Decaf Compiler — MIT 6.035, Computer Language Engineering (Feb – May 2024)

**Context:** Class project for MIT's Computer Language Engineering course (6.035)
**Dates:** February – May 2024

## What Karl did (resume-sourced)

- Wrote a compiler for Decaf (a C-like subset language used as the course's project language) in pure C, totaling roughly 8,000 lines of code.
- Built this with one partner over the course of a semester.
- Implemented a full pipeline architecture: tokenization → abstract syntax tree (AST) construction → semantic tree → low-level intermediate representation (IR) → optimizations → assembly code generation.

## Background context (web research)

**MIT 6.035, Computer Language Engineering.** Per MIT OpenCourseWare, 6.035 covers the implementation of higher-level programming languages — the theory and practice of building a compiler, and the tools used to do it. The centerpiece of the course is a semester-long project: writing a compiler for a language called Decaf, a simplified imperative language similar to C or Pascal, deliberately scoped down so a student team can implement a complete, working compiler for it in one term. OCW materials describe the project as broken into segments mirroring the classic compiler pipeline — scanner/parser, semantic checker, code generator, data-flow optimizer, and instruction optimizer — with the first stage often done individually and later stages done in small teams (the course has historically had students write in Java for some offerings, though Karl's resume specifies the project was done in pure C, which is consistent with some versions/variants of the course or an independent reimplementation choice).

**What a compiler pipeline actually does, stage by stage (for a non-specialist reader):**
- **Tokenization (lexing):** the first pass over raw source text, chopping it into the smallest meaningful chunks — keywords, identifiers, numbers, punctuation — called tokens. This is the same idea as recognizing words before trying to parse a sentence.
- **Parsing / AST construction:** the token stream is checked against the language's grammar and assembled into an Abstract Syntax Tree (AST), a tree structure that captures the program's nested structure (e.g., "this is a function call whose arguments are these two expressions").
- **Semantic analysis (the "semantic tree" step):** the compiler walks the AST and checks that the program actually makes sense beyond grammar alone — type checking (you can't add a string to a function pointer), scope resolution (is this variable declared?), and other rule enforcement that a grammar can't capture on its own.
- **Low-level IR (intermediate representation):** the program is lowered into a simpler, more uniform representation that's easier to analyze and transform mechanically than the original tree structure — not tied to the source language's syntax, and not yet tied to any specific CPU's instruction set either.
- **Optimizations:** the IR is transformed to make the resulting program faster or smaller — classic examples include eliminating dead code, hoisting invariant computations out of loops, and propagating constants — all while preserving the program's meaning.
- **Assembly / code generation:** the optimized IR is finally translated into actual machine instructions (assembly) for a target processor, including decisions like register allocation.

Writing all of these stages from scratch, in C, for a ~8,000-line project with a partner, means Karl and his partner built a real (if scoped-down) end-to-end compiler toolchain rather than just one stage of one — which is the whole point of 6.035 as a project-based systems course.
