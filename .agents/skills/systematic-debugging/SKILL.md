---
name: systematic-debugging
description: Find the root cause of a bug or failing test before changing code. Use for unexpected behavior, failing checks or regressions.
---

# Debug to the root cause

1. Reproduce the symptom safely and record the exact error or output.
2. Form one hypothesis at a time and test it with a cheap check (log, small
   run, targeted test) instead of editing code on a guess.
3. Narrow the cause: what changed, which input triggers it, where the first
   wrong value appears.
4. Fix the cause, not the symptom. Do not weaken assertions or add delays to
   hide a failure.
5. Repeat the original reproduction and run the related checks.
6. If three attempts fail, stop and report what you ruled out and what you need.
7. Remove debugging output and temporary files before finishing.
