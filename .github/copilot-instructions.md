# Copilot instructions

## Build, test, and lint

The project is a standalone `index.html`; there is no package manifest, build step, configured test runner, or linter. Open `index.html` directly in a browser to run it. For a manual smoke test, answer questions correctly and incorrectly, advance through all ten questions, and check the score, feedback, progress bar, results, restart, and theme toggle.

## Architecture

The entire application lives in `index.html`: semantic page markup, theme-aware CSS, and a vanilla JavaScript quiz controller are inline. The `questions` array is the source of truth for question text, answer choices, correct-answer indices, categories, and explanations. The controller renders one question at a time, tracks score and progress, presents feedback and results, and restarts the quiz.

## Project conventions

- Keep the page self-contained: no server, build tooling, or external runtime dependencies.
- Keep quiz length data-driven from `questions.length`; progress, completion, and results use that count. Each question's `correct` value is a zero-based index into its `answers` array.
- Preserve the light/dark theme contract: define colors as CSS custom properties in `:root` and `:root[data-theme="dark"]`; JavaScript sets `data-theme` on the document element and initially follows the system color preference.
- Render question and feedback content with DOM APIs and `textContent`. Keep answer choices as native buttons and preserve the live feedback/announcement regions and keyboard focus transfer when questions change.
- Keep motion respectful of `prefers-reduced-motion` and verify visual changes in both themes.
