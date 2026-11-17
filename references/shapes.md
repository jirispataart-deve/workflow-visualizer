# Shapes: building rules

All shapes share tokens, header, legend, symbols and info boxes from `assets/base-template.html`. The classes `.sym`, `.box.important`, `.box.concrete`, `.phase` and `.open-list` are defined there. This text describes only what each shape adds.

Contents
- Timeline
- Flowchart
- Branching
- Lanes
- Cycle
- Parallel tracks

## Timeline

The base template is already a timeline: phases with marker bars, below them an `ol.axis` with `li.step`. Each step has a time marker (`.when`), symbol, title, text and optional boxes. Waiting times get the "Wait" symbol and a documented duration in the time marker. Without a documented duration the time marker stays "Step N".

## Flowchart

For processes with decisions whose outcome leads back or brings paths together again. A finished example with complete CSS: `assets/flowchart-example.html`. Take the CSS and the scaffold from it, replace the content.

- One vertical column of boxes, joined by 2px ink lines. This works on phones because nothing sits side by side.
- Each box has an angular 2px ink border, a head with symbol, "Step N" and, on the right, a location chip, below that title and text. Decisions get `--paper-shade` as surface and the "Decision" symbol.
- The location chips replace lanes: they say where or by whom a step takes place. Three styles are enough and need no new color: outlined (ink on paper), solid ink (paper as text color) and accent surface (ink as text color). Every chip also appears in the legend.
- The exits of a decision are listed in the box, each with a bold condition ("Approved:", "Changes requested:") and the target ("continue with step 6", "back to step 2"). The path that continues downward additionally gets an uppercase tag next to the line.
- The loop-back is a bracket on the left edge: a vertical 2px stroke that ends with an arrow in the middle of the target box and starts in the middle of the decision box. It works without script using three segments (`loop-head`, `loop-body`, `loop-tail`) whose pseudo-elements attach at 50 % of the box height. The example shows the implementation.
- What the loop skips or changes on the second pass is stated in the exit of the decision (in the example: "step 4 is skipped"). The bracket spans the steps roughly, the text makes it exact.
- At most one loop-back per graphic and at most three decisions. More becomes a tangle; split into sub-processes and show each on its own.
- Connections always at right angles, no diagonals, no curves.

## Branching

For processes in which decisions change the path and the paths end in different places. If they merge again or return, the flowchart is the right shape.

- Main path vertical like the axis. At each decision (empty square) the path splits into 2 to 3 branches.
- Branches as `display: grid` with `grid-template-columns: repeat(auto-fit, minmax(220px, 1fr))` so they stack on phones.
- Each branch carries its condition on top as an uppercase label ("IF ..."), below it its steps as a short axis.
- Where branches merge again, a full-width 2px ink bar with the text "MERGE". If a branch never returns, it ends with "END" in a checkpoint symbol.
- At most two levels of branching. Deeper nesting becomes a decision tree nobody reads. Split into sub-processes and describe one of them in an info box.

## Lanes

For processes with several participants where the handoffs are the core.

- One lane per person, tool or role, at most four. The lane name sits as an uppercase label with an accent marker bar at the head.
- Lanes sit as columns side by side in a container with `overflow-x: auto`, the grid with a `min-width` of about 690px for three lanes so nothing is squeezed. The hint "swipe sideways" appears only below 700px width (media query); on desktop it is superfluous.
- Steps are numbered in order and each gets its own `grid-row`. This reads the time order as a staircase from top to bottom, even when the lanes change.
- Every handoff between lanes is a triangle symbol with the line "TO [LANE]" at the end of the handing-over step. Drawn connector lines across the grid are omitted: they break on phones and say no more than the label. The text states what is handed over.
- Omit lanes without a real handoff. If only one lane remains, the shape was chosen wrongly.
- If the process has a loop, lanes are the wrong shape: the loop ends up in an info box and gets overlooked. Use the flowchart with location chips instead.

## Cycle

For processes that repeat or whose result feeds the next run.

- Not a circle but a rectangular loop: steps as a vertical axis, at the end a 2px ink return arrow on the left side back to step 1, labeled "BACK TO STEP 1".
- On the way back it says what changes in the next run (knowledge, material, version). That is the reason for the loop and belongs in an Important box.
- The entry point of the first round gets a checkpoint symbol "START"; the exit of the loop, if there is one, gets a decision symbol "CONTINUE OR END".
- A cycle without a named gain per round is just repetition. Then a timeline with the note "repeats" is more honest.
- If the repetition depends on a decision (only repeat when something is wrong), it is a flowchart with a loop-back. The cycle applies only to processes that start over unconditionally.

## Parallel tracks

For processes in which strands run at the same time.

- Two to three tracks side by side as a grid with `repeat(auto-fit, minmax(200px, 1fr))`. Each track is a short axis.
- The start and end of the parallelism are full-width 2px ink bars: "SPLIT" at the top, "MERGE" at the bottom. The text under the lower bar says what all tracks must have delivered before things continue.
- Tracks are parallel only if they truly do not need each other. If there are dependencies, mark them with a handoff symbol between the tracks.
- The track that takes longer sets the pace. State that in an Important box if the duration is documented.
