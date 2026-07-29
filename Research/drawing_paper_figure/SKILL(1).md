---
name: academic-figure-design
summary: Design, redraw, and revise publication-quality figures for AI/ML papers, grant proposals, technical reports, and academic presentations. Prioritizes scientific logic, exact dataflow, correct arrows, disciplined text, clear hierarchy, and high-resolution paper-style rendering.
---

# Academic Figure Design Skill

## 1. Scope

Use this skill for figures in AI, machine learning, LLMs, multimodal learning, agents, vision, NLP, data mining, optimization, systems, and adjacent technical fields.

Typical tasks include:

- motivation and problem-setting figures;
- overall system or research-route overviews;
- model architecture diagrams;
- training and inference pipelines;
- data construction and filtering workflows;
- retrieval, tool-use, and agent loops;
- benchmark teaser figures;
- method-detail diagrams;
- evaluation and ablation summaries;
- strict local edits of existing academic figures.

The goal is not decorative illustration. The goal is to make scientific logic understandable at paper-reading speed.

## 2. Core doctrine

Optimize in this order:

1. scientific correctness;
2. dataflow and arrow correctness;
3. module, variable, and stage correctness;
4. readability at final page scale;
5. visual hierarchy;
6. aesthetics.

If aesthetics conflicts with logic, logic wins.

A strong figure should let a reader answer quickly:

- What are the inputs?
- What transformations occur?
- What are the intermediate representations?
- What are the outputs?
- Which part is the contribution?
- How do training, inference, supervision, and feedback differ?

## 3. Scientific abstraction before drawing

Before writing a prompt, reduce the method to a graph.

Identify:

- nodes: inputs, modules, losses, memories, tools, outputs;
- directed edges: dataflow, control flow, supervision, recurrence;
- intermediate states: embeddings, tokens, hidden states, latent variables;
- final outputs: predictions, actions, scores, generated content;
- repeated structure: layers, iterations, rounds, stages;
- boundaries: training-only, inference-only, external system, frozen module;
- contribution: the one mechanism that deserves visual emphasis.

Do not start from colors or icons. Start from the dependency graph.

## 4. Default visual language

### 4.1 Background and typography

- Use a white background.
- Use black or dark-gray main text.
- Use one consistent sans-serif family.
- Use standard mathematical notation for variables.
- Use the language requested by the user; do not force Chinese or English.
- Keep labels as short noun phrases.
- Avoid paragraphs, footnote-size annotations, and prose copied from the paper.

### 4.2 Color

Color must encode meaning.

Recommended use:

- one stable color per data type, modality, branch, or stage;
- neutral gray for ordinary infrastructure;
- one accent color for the proposed contribution;
- one result color for outputs or decisions if needed.

Avoid:

- all-blue figures;
- gradients used only for decoration;
- large pastel background panels;
- neon glow, shadows, or glass effects;
- coloring all text, arrows, icons, and borders the same color;
- too many unrelated colors.

### 4.3 Borders and grouping

- Prefer whitespace, alignment, and thin separators over large panels.
- Use thin gray outlines only when grouping is necessary.
- Do not place every item inside a rounded rectangle.
- Avoid nested cards, pill-shaped headers, and dashboard layouts.
- Use group boundaries only when they communicate scope, stage, ownership, or training/inference separation.

### 4.4 Scientific visual primitives

Prefer technical primitives over generic infographic icons:

- token strips;
- embeddings and feature maps;
- attention matrices;
- sequence timelines;
- datasets and sample records;
- graphs and memory stores;
- retrieval indexes;
- prompts and generated outputs;
- trajectories through state space;
- loss branches;
- repeated blocks;
- confidence distributions;
- tool calls and environment interactions;
- tables, plots, and result summaries.

Generic icons are acceptable only when their meaning is immediate and precise.

## 5. Arrow and connection rules

Arrow correctness is a hard constraint.

Every arrow must have:

- one explicit source;
- one explicit destination;
- one real logical meaning;
- one direction.

Do not allow:

- floating arrows;
- arrows ending near multiple modules;
- duplicated arrows for the same relation;
- arrows crossing labels;
- arrows entering a group boundary when they should enter a specific submodule;
- long curved arrows when a short orthogonal route is possible;
- decorative arrows that do not represent computation or control.

Use visual priority:

- thickest: main pipeline;
- medium: branches, outputs, and merges;
- thinnest: supervision, residual, recurrence, or auxiliary signals.

When several signals travel together, aggregate them first into a named sequence, bundle, bus, or state. Then connect that structure to the target.

Good pattern:

`feature groups -> scoring heads -> per-item scores -> aligned score sequence -> backbone`

Bad pattern:

`many heads -> many long curved arrows -> several ambiguous points inside the backbone`

If one signal affects repeated layers, use one shared bus with short local branches.

## 6. Text discipline

### 6.1 Minimal but sufficient

An overview figure should usually contain only:

- stage titles;
- module names;
- variable names;
- short output labels.

A detail figure may contain more module names, but still avoid prose.

Replace text with structure whenever possible:

- shifted timelines instead of explaining misalignment;
- aligned bars instead of explaining per-token confidence;
- a retrieval loop instead of describing repeated search in a sentence;
- a trajectory or token stream instead of writing “iterative generation.”

### 6.2 Text whitelist

For fragile image generation, provide an explicit whitelist of allowed labels and forbid invented text.

### 6.3 Exact publication text

When typography must be exact:

1. generate the visual skeleton with minimal text;
2. replace labels manually in PowerPoint, Figma, Illustrator, Inkscape, or LaTeX;
3. export as SVG/PDF or high-resolution PNG.

Do not rely on a generative model for dense, exact text.

## 7. Layout principles

### 7.1 Geometry before decoration

Specify layout in geometric terms:

- left / center / right zones;
- upper and lower parallel streams;
- aligned rows;
- fixed branch points;
- exact module order;
- exact placement of intermediate variables;
- whether a line enters a group or a specific internal block.

Weak instruction:

“Make the architecture clearer.”

Strong instruction:

“Place the token sequence above the score sequence, left-aligned and equal in length. Feed both horizontally into the backbone. The score sequence enters only the attention block.”

### 7.2 Overview figures

Use:

- one dominant left-to-right or top-to-bottom flow;
- 3–6 major stages;
- limited internal detail;
- one visual center for the contribution;
- one clean feedback or iteration loop when needed.

Do not fully expand low-level internals if a separate detail figure exists.

### 7.3 Detail figures

Use:

- exact internal module order;
- exact branch points and merge points;
- clear residual, recurrence, or supervision paths;
- one detailed repeated block plus `x L`, stacked outlines, or an iteration marker;
- minimal upstream and downstream context.

A detail figure should explain one mechanism, not the entire paper.

### 7.4 Training versus inference

If both appear, separate them explicitly using one of:

- top/bottom lanes;
- solid/dashed boundaries;
- different arrow styles;
- clearly labeled phases.

Do not mix training losses, labels, and inference outputs in one undifferentiated flow.

## 8. Variable and representation placement

A variable's position must reflect its semantic role.

- Inputs appear before the module that consumes them.
- Intermediate representations appear inside the module or at the internal stage where they are formed.
- Final outputs appear outside the producing module.
- Losses and supervision use separate thin branches.
- Cached states or memories appear where they persist across steps.

Example:

If `Z` is an internal shared representation of a backbone, place it inside the backbone near the stage that produces it. Connect the backbone boundary directly to downstream heads. Do not place `Z` as a standalone external output box unless the method treats it as an explicit output artifact.

If `R` is a per-token score sequence, first show:

`tokens -> scoring heads -> per-token scores -> aligned sequence R`.

Then feed `R` through one clean path to the module that consumes it.

## 9. Repeated and iterative structures

For repeated layers:

- fully draw one representative block;
- show repetition with `x L`, stacked outlines, or a bracket;
- keep shared auxiliary inputs on a bus;
- avoid drawing every layer unless layer-wise differences matter.

For iterative reasoning, agent loops, or refinement:

- show the loop entry and exit clearly;
- distinguish persistent state from newly generated state;
- distinguish model calls from tool/environment calls;
- show stopping conditions only if central to the method.

## 10. Figure archetypes

### 10.1 Motivation / problem figure

Use a problem progression rather than a dashboard.

Typical form:

`existing setting -> failure mechanism -> consequence -> research objective`

Show failure visually using conflicting evidence, missing context, noisy supervision, distribution shift, hallucination, long-context overload, or branching uncertainty.

### 10.2 Overall system or research route

Show all major research contents, but allocate detail unevenly:

- enough upstream detail to show how inputs become representations;
- enough center detail to show the key mechanism;
- enough downstream detail to show outputs, evaluation, or feedback;
- no low-level expansion already covered by another figure.

### 10.3 Model architecture

Use explicit dataflow through modules.

Possible pattern:

`inputs -> encoders -> aligned representations -> backbone -> task heads -> outputs`

Show frozen, shared, trainable, or external modules only when relevant.

### 10.4 Data and training pipeline

Possible pattern:

`raw sources -> cleaning/filtering -> annotation or synthesis -> training mixture -> objective -> model`

Use distinct paths for labels, negatives, rewards, or preference pairs.

### 10.5 Retrieval, tool-use, or agent system

Possible pattern:

`query -> planner/model -> retrieval/tool call -> observation -> state update -> final response`

Use one loop for repeated interaction. Avoid many tangled return arrows.

### 10.6 Benchmark teaser

Use controlled visual comparison:

`original setting -> challenge or shift -> method response -> outcome`

Keep camera, layout, scale, or sample structure consistent across stages. Change only the intended factor.

Use one concise statistics strip instead of many dashboard cards.

### 10.7 Method-detail block

Show one mechanism precisely.

For a Transformer-like block, detail may include:

`input -> projections -> modified attention -> Add & Norm -> FFN -> Add & Norm -> output`

Keep formulas secondary unless the formula itself is the contribution.

### 10.8 Evaluation or ablation figure

Use plots or structured comparisons, not decorative icons.

- align baselines and variants;
- highlight one conclusion per panel;
- label axes and units clearly;
- do not encode the same information redundantly with color, shape, and text unless accessibility requires it.

### 10.9 Strict local edit

When modifying an existing figure:

- specify the exact editable region;
- list all elements that must remain unchanged;
- state whether the task is copy/replace, redraw, recolor, or relabel;
- prohibit changes outside the target region.

For pixel-identical duplication, use a graphics editor or compositing workflow rather than generative redraw.

## 11. Prompt construction workflow

Before writing the prompt, determine:

1. figure type;
2. one-sentence scientific message;
3. graph of modules and arrows;
4. input, intermediate, and final variables;
5. contribution to emphasize;
6. level of detail appropriate to the figure;
7. allowed text;
8. semantic color mapping;
9. exact geometry;
10. excluded content and known failure modes.

Then write the prompt in this order:

### A. Task and purpose

State the figure type and scientific message.

### B. Scope

State what is included and excluded.

### C. Hard constraints

Specify:

- arrow correctness;
- variable placement;
- text amount;
- language policy;
- resolution;
- style restrictions.

### D. Exact layout

Define zones, rows, sequence alignment, branch points, merges, and loops.

### E. Module contents

Describe only the visual components required inside each stage.

### F. Text whitelist

List allowed labels when text accuracy matters.

### G. Negative constraints

Explicitly forbid known wrong structures, irrelevant modules, malformed text, UI-like styling, and ambiguous arrows.

## 12. Reusable master prompt template

```text
Create a publication-quality academic figure for [paper / grant / report].
Figure type: [overview / architecture / method detail / data pipeline / benchmark teaser / motivation / evaluation / local edit].
Scientific message: [one sentence].

Hard constraints:
- Scientific logic and arrow correctness take priority over aesthetics.
- Every arrow has one explicit source and destination.
- No floating, duplicated, crossing, or decorative arrows.
- Use a white background, dark text, thin neutral outlines, and limited semantic color.
- Avoid dashboard cards, large pastel panels, gradients, shadows, glow, and all-blue styling.
- Use minimal text; represent information with sequences, matrices, graphs, timelines, trajectories, plots, or module structure whenever possible.
- Use the highest available resolution and crisp vector-like rendering.

Scope:
- Include: [content].
- Exclude: [content].

Layout:
- [Define exact left / center / right or top / bottom geometry.]
- [Define aligned rows, parallel streams, branch points, merges, and feedback loops.]

Pipeline:
[input] -> [transformation 1] -> [transformation 2] -> [output].

Variable placement:
- [input variable] appears before [module].
- [intermediate variable] appears inside [module] at [specific internal stage].
- [final output] appears outside [module].

Module details:
[Describe only necessary internal blocks and their order.]

Text:
Use only the following labels:
[whitelist]
Do not invent additional labels.

Negative constraints:
[Forbid known wrong structures, irrelevant modules, text-heavy explanations, ambiguous arrows, malformed text, and UI-like elements.]
```

## 13. Iteration strategy

Do not solve structure and polish in one pass when the figure is complex.

Recommended sequence:

1. structural draft;
2. scientific and arrow review;
3. variable placement review;
4. text reduction;
5. visual styling;
6. high-resolution export;
7. manual typography cleanup.

When revisions keep preserving a wrong layout, stop asking for “optimization.” State explicitly:

- delete the target region;
- redraw it using the specified geometry;
- do not reuse the old internal layout.

## 14. Quality-control checklist

### Scientific correctness

- Does every module correspond to the written method?
- Are training, inference, and evaluation separated correctly?
- Are intermediate and final outputs visually distinguished?
- Is any outdated component still present?

### Arrow correctness

- Can every arrow be explained in one sentence?
- Does each arrow enter the exact intended module?
- Are there crossings, floating ends, or reversed directions?
- Are auxiliary signals visually weaker than the main flow?

### Layout

- Is the main flow visible at thumbnail size?
- Is the contribution the visual center?
- Are repeated items aligned?
- Are parallel sequences parallel and one-to-one where required?
- Are merge and branch points geometrically clear?

### Text

- Can any label be removed without losing logic?
- Is any prose copied unnecessarily from the paper?
- Are there malformed or invented words?
- Is the smallest text readable at final page scale?

### Style

- Does the figure resemble a research figure rather than a business infographic?
- Is color semantic and limited?
- Are borders and fills restrained?
- Is the background mostly white?

### Export

- Is the output high resolution?
- Are text and arrows sharp when zoomed?
- Can the figure be converted or redrawn as SVG/PDF if needed?

## 15. Common failure modes and fixes

### Figure looks AI-generated

Cause:

- all-blue styling;
- large pastel panels;
- rounded-card layout;
- generic icons;
- equal visual weight everywhere;
- too much explanatory text.

Fix:

- return to white background and dark text;
- use semantic color only;
- remove background panels;
- replace icons with technical primitives;
- reduce labels;
- strengthen one main pipeline.

### Arrows remain wrong after revision

Cause:

- prompt says “make arrows clearer” without defining geometry.

Fix:

- specify source, destination, path, and forbidden targets;
- use aligned rows and shared buses;
- remove long curved lines;
- redraw the region rather than patch it.

### Intermediate representation looks like a final output

Cause:

- variable placed outside the module boundary.

Fix:

- place it inside the module at the stage where it is formed;
- connect the module boundary directly to downstream heads.

### Auxiliary-score paths are messy

Cause:

- many scattered branches connect directly to the backbone.

Fix:

- generate per-item values first;
- align or concatenate them into one sequence;
- send the sequence through one clean input path.

### Architecture block is only a list of buzzwords

Cause:

- labels are placed inside a box without explicit internal dataflow.

Fix:

- replace the list with ordered internal modules and arrows;
- show where the intermediate representation is produced;
- keep one visual primitive per stage.

### Revision barely changes the figure

Cause:

- prompt says “adjust,” “optimize,” or “preserve the current structure.”

Fix:

- explicitly delete and redraw the target region;
- define the replacement geometry;
- state which old layout must not be reused.

## 16. Final operating rule

A publication-quality academic figure is not a decorated summary of the text. It is a compact visual proof of the method's logic.
