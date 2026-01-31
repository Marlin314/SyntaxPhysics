# SpanMarks: Reframing Structure, Annotation, and Parsing

## 1. Background and Motivation

Most systems for processing text—whether natural language, programming languages, or mixed documents—assume that a document has a single primary structure that can be recovered by parsing a linear character stream. This structure is typically represented as a tree, such as an abstract syntax tree (AST), derived by applying a grammar to the text in a largely deterministic, left-to-right process.

This approach has been enormously successful. However, it also carries a set of implicit assumptions that become limiting in modern settings: heterogeneous documents, partially correct code, mixed languages, incremental editing, refactoring, projectional views, and tooling that must reason about multiple interpretations simultaneously.

This paper explores an alternative conceptual framing. Instead of treating structure as something extracted once from text, we treat interpretation as a collection of independently generated annotations over spans of text. Trees and token streams become derived views rather than primary representations.

---

## 2. SpanMarks

We introduce **SpanMarks** as a minimal abstraction for annotating text.

A *SpanMark* is a triple of ints: (id, start, end)

`start` and `end` are integer offsets into a base text, and `id` refers to metadata describing the meaning, provenance, or interpretation of that span. When `start == end`, the mark refers to a position between characters rather than a range.

A document may have any number of SpanMarks. Marks may overlap arbitrarily, may be adjacent, nested, disjoint, or partially intersecting. No structural constraints are imposed by the representation itself.

Importantly, SpanMarks are not a storage format. They are a conceptual model for reasoning about structure, annotation, and interpretation independently of how text is stored, edited, or rendered.

---

## 3. Markup as Explicit Annotation

The term *markup* is often associated with presentation-oriented systems such as HTML or rich text formatting. In contrast, SpanMarks treat markup as **explicit annotation**: information about a text that is traditionally implicit, conventional, or enforced by grammar.

Natural text already contains many such annotations: spaces indicate word boundaries, line breaks suggest paragraph structure, and punctuation encodes cadence and grouping. Programming languages similarly embed structural cues into text using keywords, delimiters, indentation, and naming conventions. These cues are meaningful, but they are also overloaded.

SpanMarks separate these concerns. The base text need not carry all structural meaning directly. Instead, structure can be made explicit and manipulable as annotations over spans.

---

## 4. SpanMarks as Generated Evidence

A key property of SpanMarks is that they can be **generated**, not just stored.

Regular expressions and similar detectors can be treated as *SpanMark generators*: computations that, when applied to a document, produce sets of spans with known provenance. The name of a mark corresponds to the computation itself.

These generators may identify digit runs, identifier-like spans, or candidate literals. They need not be perfect or complete; they produce candidates. Multiple generators may overlap, contradict, or reinforce one another.

SpanMarks do not require that all structure be discovered in a single pass, or even eagerly. Annotations can be recomputed on demand, filtered, combined, or ignored depending on the task.

---

## 5. Composition Without Commitment

Traditional parsing commits early: once a token stream or parse tree is produced, alternative interpretations are discarded.

SpanMarks enable a different workflow. Multiple span generators can be combined and filtered. For example, candidate literal spans may be accepted or rejected based on whether they occur within code spans, comments, or identifier spans.

This approach is typically less efficient than a hand-written parser, but it is often easier to reason about, easier to modify, and more robust in the presence of incomplete or mixed-language input.

---

## 6. Projections and Editing

SpanMarks naturally support projectional views of documents. A given structure may be rendered in multiple textual forms without changing its underlying identity.

Object-oriented syntax and functional notation can be understood as different projections of the same underlying structure. Keywords such as `this` or implicit parameters can be treated as presentation choices rather than fundamental semantic entities.

From this perspective, an editor need not edit text directly. Instead, it edits structures and relationships that can be rendered as text when needed—whether as conventional ASCII for legacy tools or as richer views for navigation and comprehension.

---

## 7. Discussion

SpanMarks do not replace grammars, parsers, or ASTs. Rather, they reposition them as derived artifacts within a broader ecosystem of annotations. This reframing makes it easier to reason about ambiguity, partial structure, mixed languages, and evolving documents.

By making interpretation explicit and separable from text, SpanMarks invite experimentation with new tooling models—particularly editors and analyzers that operate on structure without requiring early or exclusive commitment to a single parse.
