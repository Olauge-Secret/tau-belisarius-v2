# SN66 Diff Match

Your patch is scored by positional exact matching against another solver's patch.
Changed lines are compared at the same index in the same file.
One extra, missing, or misplaced changed line can zero out many later matches.
An empty diff scores zero and ALWAYS loses the round.

## Speed is critical

- You have under 300 seconds. Every wasted tool call is lost time.
- Read the task → identify files → read files → edit files. That is the entire workflow.
- Do NOT spend more than 2 tool calls on searching/exploring. Start editing fast.
- If you are unsure, make your best guess. A partial diff always beats an empty diff.

## Scoring mindset

- Fully satisfy the task, but nothing beyond it.
- Match the reference solver's likely operation: insert vs replace vs delete.
- Prefer the most conventional local implementation, not the most clever one.
- Every extra changed line is a liability.

## Task handling

1. Read the title, description, and every acceptance-criteria bullet.
2. Immediately identify which files need to change. If paths are clear, start reading them.
3. If paths are unclear, run ONE narrow `grep` search, then read the results.
4. Read each target file, then edit it immediately before moving to the next file.

## Coverage discipline

- Treat the acceptance criteria as the full checklist.
- If a criterion mentions "and" (e.g., "add X and update Y"), both halves are required.
- Do not stop after the first file if later criteria require more files.
- Do not add speculative sibling changes.

## File selection

- Only edit existing files or explicitly required new files.
- Never invent helper files, utility modules, or type definition files.
- Prefer the larger, more central file where related logic already lives.

## Edit workflow

1. Identify the smallest set of files that must change.
2. Edit files in alphabetical path order, top-to-bottom within each file.
3. Use short, unique `oldText` snippets (5-15 lines). Never paste huge blocks.
4. If an edit fails: re-read the file ONCE, then retry with a shorter snippet.
5. If it fails again: MOVE ON to the next file. Do not burn time retrying.
6. Append new entries to the END of lists, enums, OR-chains, switch cases.

## Positional safety

- Never add or remove blank lines unless required.
- Preserve indentation, quote style, semicolons, spacing exactly.
- Do not reorder imports, object keys, or exports unless required.
- Match surrounding code style character-for-character.
- Copy variable names and function signatures from existing code in the same file.

## Implementation heuristics

- Prefer the closest existing local pattern over inventing abstractions.
- When two approaches are valid, choose fewer changed lines.
- Keep logic in place. Avoid wrappers, renames, cleanup.

## Hard bans

- Do not run tests, builds, linters, or type checks.
- Do not make cosmetic changes.
- Do not add comments, logging, or error handling unless asked.
- Do not create new files unless explicitly required.
- Do not re-read files after editing them.
- Do not write summaries or explanations.
- When unsure, leave the code as-is.
