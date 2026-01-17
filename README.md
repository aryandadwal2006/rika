# RIKA

**A programming language that starts like Python and hardens like Rust—without a rewrite.**

---

## The Vision

Most software doesn’t start as a system. It starts as a script.

Over time, the script grows:
- a few functions become a service,
- then a product,
- then a critical dependency.

At each stage, the code carries the DNA of its origin:  
fast to write, hard to optimize; easy to change, hard to reason about.

The traditional response is:
> “Prototype in Python, then rewrite in C++/Rust/Go when it matters.”

That rewrite is often the most expensive, risky, and demoralizing part of the lifecycle.

**RIKA is an exploration of a language where you don’t rewrite—you evolve.**

---

## The Problem

The core tensions:

- **Prototype vs Production**  
  Dynamic, GC’d languages excel at exploration; statically-typed, ownership-based languages excel at robustness and performance. Teams are forced to pick *one* upfront or juggle *two* forever.

- **Cognitive Overhead**  
  Rust’s borrow checker is incredibly powerful, but it’s an all-or-nothing commitment. You pay the cognitive cost on line 1, even when you’re just sketching an idea.

- **Operational Complexity**  
  Two-language stacks introduce:
  - FFI boundaries,
  - duplicated logic,
  - version skew between “research” and “prod” code.

- **Organizational Friction**  
  Different teams own different layers: “Python folks” vs “systems folks”. Handoffs become bottlenecks.

Underneath all this is a single rigid choice:  
**global memory management strategy decided on day zero**.

---

## What RIKA Strives To Be (Concept-Only)

RIKA is not a language yet. It is a **direction**:

> Start with Python-like ergonomics;  
> selectively introduce Rust-like ownership where profiling tells you it matters;  
> keep everything in one language and one mental model.

Tentative design aspirations:

1. **Mode 1: GC-First Scripting**  
   - Write code with high-level collections, dynamic structures, and garbage collection.
   - Ideal for exploration, glue code, scripts, and “let’s see if this works”.

2. **Mode 2: Gradual Typing and Constraints**  
   - Add type annotations for clarity and tooling.
   - The compiler can optimize more aggressively as information increases.
   - Still primarily GC’d, but more predictable and analyzable.

3. **Mode 3: Hot-Path Ownership**  
   - Mark specific functions/files as “hot paths”.
   - Inside those regions, ownership and borrowing rules (Rust-like) apply.
   - GC is disabled or tightly controlled there; code compiles to tight machine code.

4. **Single-Language Interop Between Modes**  
   - GC regions and ownership regions can call each other with well-defined, visible boundaries.
   - No FFI, no separate build systems—just different compilation regimes.

5. **Tooling-Guided Evolution**  
   - Profilers and analyzers suggest where to introduce ownership for the biggest wins.
   - The “rewrite in Rust” becomes “add annotations here”.

---

## Why the Name “RIKA”?

“RIKA” is short, memorable, and relatively unused in the programming world.

It also evokes the idea of **growth** and **refinement**: something small and simple that can mature into something robust and strong.

You can also read it as:
- **R**ust-**I**nspired **K**indergarten **A**pproach:
  start gentle, learn ownership gradually.

If a future community prefers a different name, the ideas can outlive the label.

---

## North Star Questions

This repository is meant to explore questions like:

- How can a single type system cleanly express both GC-managed and owned/borrowed memory?
- Where do boundaries between “modes” live: functions, modules, types?
- What guarantees can we give about GC not “leaking into” hot paths?
- Can we build a developer experience where ownership feels like an upgrade, not a punishment?
- How do we avoid ending up with *two* languages accidentally glued together?

These are open questions meant to drive design sketches and research.

---

## Non-Goals (For Now)

- Competing head-on with Python or Rust as they exist today
- Designing a perfect syntax
- Solving every performance corner case before proving the core idea
- Producing a full-blown compiler before the semantics are clear on paper

RIKA is currently about **principles**, not products.

---

## How This Repo Should Evolve

Initially, this repository will hold:

- Design notes contrasting “monolithic ownership” (Rust) vs “global GC” (Python/Go)
- Strawman proposals for:
  - ownership regions,
  - GC boundaries,
  - interop between them
- Case studies of codebases that went through a Python → Rust or Python → C++ rewrite and what pain points could have been avoided

If the direction holds up under critique, later steps might include:

- A tiny experimental interpreter to explore semantics
- A minimal compiler that supports:
  - one GC mode
  - one ownership-annotated mode
  - a visible transition between them

---

## Contributing (At the Idea Stage)

Helpful contributions at this point:

- War stories:
  - “We rewrote X from Python to Rust; here’s what really hurt”
  - “We tried to wrap C++ from Python; here’s where the model broke”
- Theoretical input:
  - Prior work on mixed memory models
  - Gradual typing with ownership
- Skepticism:
  - Reasons why this may be impossible or undesirable
  - Trade-offs that are being ignored

There is **no implementation to patch** yet. The battle is for the *design space*.

---

*This repo is a stake in the ground: that maybe the industry doesn’t actually need “a better Python” or “a simpler Rust”, but a bridge between the two ways of thinking built into one coherent language.*
