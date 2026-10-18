# Copilot instructions

## Project shape and architecture

- This is a standalone, dependency-free Spanish space-exploration quiz. The entire application lives in the root `index.html`; markup, responsive styling, question data, and interaction logic are intentionally kept together so the page can be opened directly with a `file://` URL.
- The `questions` array is the source of truth for the quiz. Each entry provides a question, four answer strings, a zero-based correct-answer index, and an explanatory fact shown as feedback.
- The quiz controller renders one question at a time, locks answers after selection, awards 10 points for a correct answer, updates progress, then replaces the quiz content with the results screen. Restarting reloads the standalone page.

## Commands and local verification

- There is no package manifest, build system, test runner, or linter configured, so there are no build, lint, or automated test commands (including a single-test command). No install or build step is required.
- Run the app by opening `index.html` directly in a browser. A single manual smoke test is: answer one question correctly and one incorrectly, confirm only the correct answer adds 10 points and each selection shows the appropriate feedback, continue through all 10 questions, verify the final score/reaction, and use “Jugar de nuevo” to restart.

## Codebase-specific conventions

- Keep application changes in `index.html` unless the project is deliberately expanded beyond its current single-file, no-dependency design.
- Keep question content in Spanish and add or edit questions in the `questions` array. Correct-answer indices are zero-based; the score display and results logic currently assume 10 questions worth 10 points each.
- Keep presentation colors in CSS custom properties in `:root`, with corresponding overrides in `@media (prefers-color-scheme: dark)`. Preserve the mission-control header and its readouts in both themes.
- Use native `<button>` elements for answer and action controls. Preserve visible keyboard focus, focus transfer after answering and changing questions, and the live/status announcements for score, question feedback, and quiz content.
- Feedback state is expressed with the `.correct`, `.incorrect`, `.good`, and `.bad` classes. Maintain the green correct treatment, red incorrect treatment with the shake animation, and `prefers-reduced-motion` override when adjusting these states.
- Keep the quiz card narrow and responsive, and use the existing sans-serif system font stack and 14–16 px body/control typography.
