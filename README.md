# `Petal`

> **A systems research project exploring how Zig changes the design of dynamic runtimes.**
> Not a Python replacement. Not a competitor. A laboratory.

---

## Overview

**`Petal`** is an experimental runtime written in **Zig** to investigate:

* Native lowering without C as an intermediary
* Memory model design in dynamic systems
* Concurrency without legacy constraints (e.g., GIL-style locking)
* Deterministic behavior in a high-level runtime

`Petal` does **not** aim to:

* Replace **CPython**
* Compete with **Mojo**
* Implement full Python compatibility
* Build a production ecosystem

It exists to answer architectural questions.

---

## Motivation

Most modern dynamic runtimes historically rely on C as:

* The implementation language
* The memory abstraction layer
* The lowering path to native code

C introduces:

* Undefined behavior
* Optimizer-dependent semantics
* Implicit assumptions about memory
* Global-state patterns that complicate concurrency

Zig offers a different foundation:

* Explicit memory allocation
* No hidden runtime
* No undefined behavior by default
* Built-in cross-compilation
* Clear concurrency primitives

`Petal` explores whether these properties meaningfully change runtime design.

---

## Core Research Questions

### 1. Native Lowering Semantics

* Does Zig produce more predictable machine code than C in runtime contexts?
* Is layout reasoning clearer?
* Can dynamic dispatch and tagged unions be lowered more transparently?

---

### 2. Memory Architecture

`Petal` experiments with:

* Explicit allocator injection
* Arena-based models
* Region-based lifetimes
* Deterministic destruction strategies
* Minimizing or avoiding garbage collection

Question:

> Can a dynamic runtime gain predictability without a borrow checker or full GC?

---

### 3. Concurrency Models

Instead of inheriting global interpreter lock patterns, `Petal` investigates:

* Actor-style isolation
* Per-heap isolation
* Message passing between runtime domains
* Structured concurrency using Zig primitives
* Lock-free runtime components

Goal:

> What concurrency models become viable when not constrained by C-era runtime assumptions?

---

### 4. Toolchain Simplicity

`Petal` evaluates:

* Zig as a code generation layer
* Zig’s LLVM integration
* Cross-compilation without CMake/toolchain glue
* Reduced build complexity

---

## Minimal Architecture

`Petal` intentionally implements only what is required to test hypotheses.

```text
Source (minimal subset)
    ↓
Lexer
    ↓
Parser
    ↓
Simple AST
    ↓
Optional Bytecode
    ↓
Zig VM
    ↓
Experimental Native Backend
```

Language subset (research scope):

* Integers
* Functions
* Control flow
* Basic object model
* Concurrency primitives

No:

* Full standard library
* C extension support
* Ecosystem compatibility
* Production guarantees

---

## What `Petal` Is Not

* Not a “ZPython”
* Not a drop-in replacement
* Not an ecosystem play
* Not a language war

It is a controlled environment for experimentation.

---

## Expected Outcomes

`Petal` may yield insights into:

* Deterministic dynamic runtimes
* Safer memory discipline in non-Rust systems
* Alternative concurrency models
* Cleaner native lowering paths
* Runtime architecture for future systems projects

Even if `Petal` never becomes a product, the architectural knowledge gained is the objective.

---

## Timeline

Planned exploration window: **2028**

`Petal` requires:

* Systems maturity
* Compiler literacy
* Concurrency intuition
* Architectural discipline

It is a research effort, not a sprint.

---

## Philosophy

`Petal` asks a narrow but meaningful question:

> If we were designing a dynamic runtime today,
> without C-era constraints,
> what architectural freedoms would Zig give us?
