# SyntaxPhysics

**SyntaxPhysics** is a trainable parsing substrate inspired by biochemical binding, energy minimization, and emergent structure.

Instead of executing a fixed grammar left-to-right, SyntaxPhysics lets structure *form* by local interactions between spans and joints. Directional affinities, reversible bindings, and conserved invariants ("physics") guide the system toward stable parse trees—even for incomplete, malformed, or partially edited input.

This repository explores a different question than traditional parsing:

> *What structure is trying to exist here, even if the text is wounded?*

---

## Core Idea (One Paragraph)

Text is modeled as spans separated by joints. Joints exert directional binding forces; spans accumulate tension when forces remain unresolved. Structure emerges as bindings form to reduce total energy. Some bindings harden and become effectively irreversible. Others remain soft and reversible. Rather than encoding syntax rules, we define a small set of mechanics and allow affinities to be **trained from examples** (or evolved), producing parsers that are robust, parallel in concept, and excellent at error localization.

---

## Why This Exists

Traditional parsers are:
- Serial (single global state)
- Brittle in the presence of errors
- Forced to choose modes early (lexer/parser phases)

SyntaxPhysics aims to:
- Parse incomplete or malformed text gracefully
- Localize errors without halting structure formation
- Support interactive and structural editors
- Learn syntax from examples rather than grammars
- Separate *mechanics* from *language definition*

This is not a replacement for classical parsing—it is a **front-end substrate** that can feed, augment, or even discover grammars.

---

## Design Principles

### 1. Hard-code Invariants, Not Syntax

The system hard-codes only the *physics*:
- Spans and joints
- Directional binding forces
- Energy, tension, and fracture costs
- Suppression and shielding of forces

Which characters matter, how they bind, and when bindings harden are **learned**.

---

### 2. Directional Affinity at Joints

Bindings are not symmetric.

For example:
- An opening delimiter tends to bind strongly to the **right**
- A closing delimiter tends to bind strongly to the **left**

This asymmetry naturally produces pairing and nesting without stacks or modes.

---

### 3. Spans Can Be Unhappy

Spans accumulate internal tension when binding forces are unresolved.

- Balanced structure → low tension → rigid
- Unbalanced structure → high tension → seeks resolution or fracture

Errors are not failures; they are *stress concentrations*.

---

### 4. Suppression Instead of Modes

Quotes, comments, and literals are not special cases.

They emerge as spans that **absorb or suppress forces**, preventing internal structure from affecting the outside. This allows literal delimiters like `"("` or commented delimiters like `/* ( */` to coexist naturally with structural ones.

---

### 5. Hybrid Initialization Is Allowed

A lightweight serial pass may:
- Identify all joints
- Seed obvious, high-certainty bindings
- Apply regex-based recognizers as *nucleation sites*

These steps bias the system but do not dictate final structure.

---

## Learning From Examples

SyntaxPhysics can be trained using:
- Finite example strings
- Regex-defined languages (infinite positive examples)
- Target parse trees or span groupings

Learning adjusts:
- Binding affinities
- Directional pull strengths
- Suppression behavior
- Hardening thresholds

No grammar rules are required.

---

## What This System Is Good At

- Expression parsing
- Parentheses and delimiter recovery
- Partial and in-progress code
- Structural editors
- Error localization and visualization
- Mixed natural/formal text
- Grammar discovery

---

## What This System Is *Not*

- A drop-in compiler front-end
- A replacement for proven LR/LL parsers
- A purely neural black box
- A lexer-with-modes

SyntaxPhysics trades procedural certainty for structural resilience.

---

## Minimal Architecture (Conceptual)

1. **Initialization**
   - Identify spans and joints
   - Apply optional regex recognizers

2. **Dynamics**
   - Random but biased joint selection
   - Directional binding and fracture
   - Energy minimization

3. **Stabilization**
   - Low-tension spans harden
   - High-tension regions remain flexible

4. **Interpretation (Optional)**
   - Extract trees
   - Feed classical parsers
   - Visualize stress and structure

---

## Roadmap

- [ ] Minimal span/joint substrate
- [ ] Directional force model
- [ ] Energy and tension mechanics
- [ ] Regex-based nucleation
- [ ] Example-driven training loop
- [ ] Visualization of stress and bindings
- [ ] Integration with structural editors

---

## Guiding Motto

> *Let syntax settle, don’t force it.*

---

## Status

Early research / prototype design.
Contributions, critiques, and thought experiments are welcome.

---

## License

TBD (likely permissive).

