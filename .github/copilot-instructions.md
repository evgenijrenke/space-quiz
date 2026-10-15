# Copilot instructions

## Project shape

This is a dependency-free, single-page space quiz. `index.html` contains the semantic page markup, its responsive and light/dark CSS, and all quiz behavior in one inline script; there is no build step or server-side code.

The script's `questions` array is the quiz content source. `renderQuestion()` builds each question and its answer buttons, `selectAnswer()` handles scoring and feedback, and `showResults()` displays the final reaction. The progress display and result score derive from the question list.

## Commands

- Open the page locally on macOS: `open index.html`
- Check the inline JavaScript syntax: `sed -n '/<script>/,/<\\/script>/p' index.html | sed '1d;$d' | node --check`

There is no automated test or lint runner. Verify behavior in a browser by answering questions, checking score and correct/incorrect feedback, advancing to results, and restarting.

## Conventions

- Keep the app self-contained in `index.html`; do not add a framework, server, or runtime dependency.
- Keep exactly 10 quiz entries unless the product scope changes. Each entry has `question`, `answers`, `correct`, and `fact`; `correct` is the zero-based index into `answers`.
- Keep quiz content in the `questions` array and let the existing render/answer/result flow consume it rather than duplicating question-specific UI.
- Preserve theme values as CSS custom properties in `:root` and its `prefers-color-scheme: light` override. Respect the existing reduced-motion rule.
- Answer choices and actions are native buttons. Keep the live feedback and progress semantics, and move focus to the question heading when advancing so keyboard users stay oriented.
- Insert answer and fact strings as text, not HTML. The option-letter markup is static; question content is data.
