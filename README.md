# AppADay 091 &middot; Grade Runway

**Weighted course grades for every class you are taking, plus the minimum average you still need on the work that is left.**

**Live:** https://augustineiacopelli.github.io/appaday-091-grade-runway/
**Portfolio:** https://augustineiacopelli.github.io/appaday/

Category: **D** (Data Viz) &middot; Shipped 2026-08-06 &middot; App 091 of AppADay

## What it does

You copy the grading table out of a syllabus once. Each row becomes a component with a name, a weight, and a score. Grade Runway then keeps three questions answered at all times: where you stand right now, where you could still finish, and exactly what it takes to hit the grade you are after.

The center of the screen is the rail, a single band representing the whole course. Every component takes a slice of the rail as wide as its weight. Inside each slice, mint is points earned, rose hatching is points already lost, and indigo hatching is runway you have not flown yet. A gold line drops through the rail at your target. If the mint has passed the line, the target is locked in no matter what happens next. If the mint plus the runway falls short of the line, the target is gone and the app says so instead of pretending.

Underneath the rail is the number that actually matters: the average you need across everything still ungraded. It is restated per remaining item in raw points, so "92.5%" becomes "18.5 of 20 points on the final exam." A ladder of standard cutoffs sits beside it, showing the required average for an A, A-, B+, B, and B- at once, and each rung is a button that moves your target. A projection slider runs the other direction: pick an average you think you can hold, and watch the final grade land.

Every course you add gets its own rail, its own target, and its own math. The All Courses panel stacks them so a whole term reads in one glance.

## Details worth knowing

The score field takes whatever notation is in front of you. Type `88`, or `88%`, or `45/50` and it resolves to the same thing. Leave it blank until the work comes back graded; blank means "still open," not zero, which is what keeps the current-grade figure honest early in a term.

Weights are figured against their own total rather than an assumed 100. If a syllabus adds up to 95%, the app says so, does the math correctly against 95, and offers to scale everything to 100 in one tap.

Scores above 100 are allowed, so extra credit behaves the way it should.

Everything is kept in `localStorage` on the device. Nothing is uploaded, there is no account, and no network request leaves the page except the Google Fonts stylesheet.

## Build notes

One self-contained file. Vanilla HTML, CSS, and JavaScript, no framework and no build step. The rail and the course bars are laid out in CSS so they reflow at any width; the contribution chart is drawn on a canvas with device-pixel-ratio scaling and redrawn on resize and after web fonts settle. Component rows are rebuilt only on structural changes so typing never loses focus, while every derived readout recomputes on each keystroke.

Type is Bricolage Grotesque for display, Archivo for interface, and JetBrains Mono for every figure, on an indigo ground with a graph-paper grid.

Tested at 375px and on desktop. Keyboard focus is visible throughout, and motion is dropped when the system asks for reduced motion.

---

Part of [AppADay](https://augustineiacopelli.github.io/appaday/) by Augustine Iacopelli. One complete app, every day.
