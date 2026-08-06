# AppADay 091 &middot; Grade Runway

**Drop in a syllabus PDF, get the grading table read out of it, and track the weighted grade for every class you are taking alongside the minimum average you still need on the work that is left.**

**Live:** https://augustineiacopelli.github.io/appaday-091-grade-runway/
**Portfolio:** https://augustineiacopelli.github.io/appaday/

Category: **D** (Data Viz) &middot; AI-powered &middot; Shipped 2026-08-06 &middot; App 091 of AppADay

## What it does

You get the grading table into the app once, either by typing it or by handing over the syllabus itself. Each row becomes a component with a name, a weight, and a score. Grade Runway then keeps three questions answered at all times: where you stand right now, where you could still finish, and exactly what it takes to hit the grade you are after.

The center of the screen is the rail, a single band representing the whole course. Every component takes a slice of the rail as wide as its weight. Inside each slice, mint is points earned, rose hatching is points already lost, and indigo hatching is runway you have not flown yet. A gold line drops through the rail at your target. If the mint has passed the line, the target is locked in no matter what happens next. If the mint plus the runway falls short of the line, the target is gone and the app says so instead of pretending.

Underneath the rail is the number that actually matters: the average you need across everything still ungraded. It is restated per remaining item in raw points, so "92.5%" becomes "18.5 of 20 points on the final exam." A ladder of standard cutoffs sits beside it, showing the required average for an A, A-, B+, B, and B- at once, and each rung is a button that moves your target. A projection slider runs the other direction: pick an average you think you can hold, and watch the final grade land.

A projection slider runs the whole thing in reverse. Rather than asking what you need, it asks what happens if. Drag it to an average you think you can actually hold on the ungraded work and the final grade moves with it, with the two endpoints labeled so you can see the floor and the ceiling of the course without moving anything. Until you touch it the slider parks itself on the average you need, so it opens showing exactly the scenario that matters.

Every course you add gets its own rail, its own target, and its own math. The All Courses panel stacks them so a whole term reads in one glance.

## Reading a syllabus

The dropzone sits directly under the course chips at the top of the page. Drop the PDF on it, or click it to choose a file. It goes to Claude as a document, along with an instruction to find the grading breakdown and return it as structured data, and comes back as a list of components with weights. If the syllabus states a grading scale, the A cutoff becomes the course target, so a program that puts an A at 93 rather than 90 is respected without you setting it.

Nothing is applied behind your back. The result appears as a preview with the course name, the component count, the weight total, and the detected A cutoff, and you decide whether it becomes a new course, replaces the one you are looking at, or gets discarded. Points-based syllabi are converted to percents on the way through.

Plain text files and photos of a printed grading table work too, though a clean PDF gives the best results.

This is the only part of the app that touches the network. Your Anthropic API key goes in the Settings gear at the top right, is kept in `localStorage` on your device, is never committed anywhere, and is sent only to `api.anthropic.com`. There is a Test key button that fires a one-word request so you can confirm it works before uploading anything. The rest of Grade Runway runs with no key at all.

## Details worth knowing

The score field takes whatever notation is in front of you. Type `88`, or `88%`, or `45/50` and it resolves to the same thing. Leave it blank until the work comes back graded; blank means "still open," not zero, which is what keeps the current-grade figure honest early in a term.

Weights are figured against their own total rather than an assumed 100. If a syllabus adds up to 95%, the app says so, does the math correctly against 95, and offers to scale everything to 100 in one tap.

Scores above 100 are allowed, so extra credit behaves the way it should.

Course data is kept in `localStorage` on the device. There is no account and no sync. Apart from the Google Fonts stylesheet, the only request that leaves the page is the syllabus you choose to send to Claude.

## Build notes

One self-contained file. Vanilla HTML, CSS, and JavaScript, no framework and no build step. The rail and the course bars are laid out in CSS so they reflow at any width; the contribution chart is drawn on a canvas with device-pixel-ratio scaling and redrawn on resize and after web fonts settle. Component rows are rebuilt only on structural changes so typing never loses focus, while every derived readout recomputes on each keystroke.

Syllabus PDFs are base64 encoded in the browser and passed to the Messages API as a `document` block, so there is no PDF parsing library and no server in the path. The model is pinned to `claude-sonnet-5`. Responses are requested as bare JSON, fences are stripped defensively, parsing is wrapped, and every returned weight is checked for a finite positive number before it is allowed anywhere near your grades.

Type is Bricolage Grotesque for display, Archivo for interface, and JetBrains Mono for every figure, on an indigo ground with a graph-paper grid.

Tested at 375px and on desktop. Keyboard focus is visible throughout, and motion is dropped when the system asks for reduced motion.

---

Part of [AppADay](https://augustineiacopelli.github.io/appaday/) by Augustine Iacopelli. One complete app, every day.
