---
name: workflow-visualizer
description: Explains a workflow in detail as a visual page (symbol legend, info boxes, tangible explanations) and picks the shape of the diagram itself based on the structure of the process. Use whenever a workflow, process or procedure is the topic AND the user wants detail, e.g. "in more detail", "step by step", "how exactly does that work", "explain the workflow again". Do not use when "workflow" is only mentioned in passing or a short answer is enough.
---

# Workflow Visualizer

When someone wants to understand a workflow in detail, running text rarely suffices. A process has an order, handoffs, decisions and waiting times. A fitting graphic makes that readable at once. It replaces the long text answer rather than adding to it.

The shape is chosen freely. No shape has priority, neither the timeline nor any other. The structure of the workflow decides.

## When this skill applies

Two conditions together:

1. The context is a workflow, process or procedure (the user's own, one that was discussed, or one that needs to be explained from scratch).
2. The user wants more depth: "in detail", "more precisely", "step by step", "explain again", "how does it run".

If the word "workflow" only comes up in passing and the question is quickly answered, reply briefly in chat. A graphic for every passing mention cheapens it.

## Procedure

1. **Clarify the process.** Take the process from the conversation, from files, or from sources the user names. If something essential is missing, ask once, briefly. Do not invent steps, durations or tools. Anything unverified is marked "Open".
2. **Read the structure, then choose the shape.** See the next section. Say in one sentence in chat which shape you chose and why. The user can overrule you with one word.
3. **Outline.** 4 to 10 steps in total, grouped into 2 to 4 phases or lanes. More dilutes the graphic; summarize sub-processes instead.
4. **Fill each step.**
   - Time marker or position: a real duration, point in time, or order ("Step 3"). No guessed clock times.
   - A symbol from the legend.
   - A title (noun, short) and one to two sentences on what happens and why.
   - Optional **Important** box: only when a piece of information can make or break the process (prerequisite, source of error, approval).
   - Optional **Concrete** box: one tangible image, example or analogy that makes an abstract step graspable. The image explains something; it does not decorate.
5. **Build the legend.** Only the symbols that appear in the graphic, plus the elements of the chosen shape. The legend sits at the top.
6. **Deliver as a page.** Build it from `assets/base-template.html` (tokens, header, legend, boxes) and add the structure of the chosen shape following `references/shapes.md`. For the flowchart there is a finished example in `assets/flowchart-example.html`: reuse its CSS and replace the content. Title the page with the name of the workflow, for example "Document approval flow". If your environment can publish pages or artifacts, publish it there; otherwise deliver one self-contained HTML file.
7. **Reply in chat.** One or two sentences: the chosen shape with the reason, and any open points. Do not repeat the content of the graphic.

## Choosing the shape

Read the structure of the workflow first, then decide. These questions help:

- Are there decisions whose outcome leads back (a loop), or whose paths meet again, and should the reader be able to trace the path with a finger? → **Flowchart**
- Do paths split at decisions and end in different places without returning? → **Branching**
- Do several people, tools or roles carry parts of the process, is the difficulty in the handoffs, and is there no loop? → **Lanes**
- Does the process start over unchanged after the last step, or does the result feed the next run, with no decisions in between? → **Cycle**
- Do strands run at the same time and have to come together somewhere? → **Parallel tracks**
- Is the process at its core a sequence of steps over time, with waiting times, deadlines or durations that matter? → **Timeline**
- Does the workflow mix several properties? Pick the one where the reader is most likely to go wrong. The secondary property becomes an info box or a location tag: a flowchart can show where a step takes place without needing lanes.

A loop is the most common reason to switch shape. Hiding it in an info box buries it, and that is exactly where readers stumble. If there is one, the flowchart is usually the most honest shape, even if lanes or the timeline look suitable at first glance.

Do not choose by looks or by habit. A shape that does not match the structure falsifies the process: an axis hides alternatives, lanes without real handoffs are decoration.

The exact building rules for each shape are in `references/shapes.md`. Read only the section of the chosen shape.

## Symbols

All angular, no circles. The shapes are drawn with CSS rather than characters so they look the same everywhere.

| Symbol | Shape | Meaning |
|---|---|---|
| Action | filled square | something is done or produced |
| Decision | empty square | the flow branches here |
| Checkpoint | diamond | check, sign-off, approval |
| Handoff | triangle | result moves to a person, tool or phase |
| Wait | horizontal bar | nothing happens actively, time passes |
| Open | dashed square | information is missing or unverified |

Add further symbols only when the workflow really needs them, and explain them in the legend.

## Styling

The template ships with a neutral default: a warm paper background, near-black ink, one pale accent used only as a surface, and the system font. All colors are tokens in `:root`. If the user has a brand or design system, change only those tokens; do not restyle the structure.

- Paper as background, ink for titles, graphite for running text, a calm shade for quiet surfaces, hairlines for rules.
- The accent is used only as a surface, never as text or line color. Text on it is always ink. At most one large accent band per page; the small marker bars (10px) under phase and lane titles may repeat.
- One font family. Hierarchy through weight and letter-spacing; letter-spacing only on capitals.
- No shadows, gradients, rounded corners, emojis or exclamation marks. Lists use ink squares. Connections are straight lines with right angles, 2px ink.
- The page stays single-theme on paper. All colors are set explicitly so it reads the same in light and dark UIs.
- Mobile first, no horizontal scrolling of the page. Anything that has to be wider (lanes) scrolls in its own container.

Do not invent new colors, fonts or shapes. If the system lacks something, name the gap and solve it within the tokens.

## Language

Write the graphic in the language the user is using. Keep it factual, noun-based and short. No filler, no trend talk. Explanations may be vivid but precise: one strong image rather than three weak ones.

## Checklist before delivering

- The shape follows the structure of the workflow, and the chat sentence names the reason.
- Every loop is drawn as a path and not only mentioned in text.
- Every time statement is documented or marked as order only.
- Anything unverified carries the "Open" symbol.
- All symbols in the graphic appear in the legend, and no others.
- The accent is used only as a surface, never as text or line.
- No text runs past the edge, not even at 400px width.
- The chat text does not repeat the content of the graphic.
