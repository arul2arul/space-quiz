# Copilot instructions

## Project shape

This is a dependency-free, single-page space quiz in `index.html`. The document contains all markup, styles, question data, and client-side behavior; there is no separate build or server-side layer. The page moves between the intro, quiz, and results sections by toggling their `hidden` class.

Question content is the `questions` array in the inline script. Each entry has a category, question, answer strings, and a zero-based `correct` answer index. Quiz state (`current`, `score`, and `answered`) is managed in the same script; `showQuestion`, `chooseAnswer`, and `showResults` update the DOM and connect the quiz flow.

## Commands

There is no configured build, automated test, or lint command: the repository has no package manifest, test runner, or tooling configuration.

To preview locally, open `index.html` in a browser, or run `python -m http.server 8000` from the repository root and visit `http://localhost:8000`. There is no automated single-test command; verify changes in the browser by starting a quiz, selecting correct and incorrect answers, completing all questions, and restarting.

## Conventions

- Keep the app dependency-free and self-contained in `index.html` unless the project is deliberately being expanded.
- Keep quiz text and answer keys in the `questions` data rather than duplicating question-specific behavior in rendering code. `correct` is a zero-based index into `answers`; the displayed question count and progress maximum derive from `questions.length`.
- Preserve the three-stage flow and its state boundaries: initialize or reset in `beginQuiz`, render the active item in `showQuestion`, accept at most one selection in `chooseAnswer`, and populate the summary in `showResults`.
- Build answer controls as buttons and use `textContent` for question and answer copy. Keep selection and disabled states, visible feedback, focus movement, live regions, and progress-bar ARIA values in sync with the quiz state.
- Keep visual styling in the document's `<style>` block. Shared colors are CSS custom properties on `:root`; the light palette follows `prefers-color-scheme`, and responsive and reduced-motion behavior is handled with media queries.
