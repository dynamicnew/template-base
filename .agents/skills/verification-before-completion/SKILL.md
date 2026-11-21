---
name: verification-before-completion
description: Run the checks and confirm the outcome before saying work is done, fixed or passing.
---

# Verify before you claim

1. State how you will verify the outcome before you start changing things.
2. After the change, run the relevant check yourself: tests, build, typecheck or
   a direct run of the behavior. Do not rely on reading the code.
3. Include the success, failure and boundary cases that matter.
4. Report exact results (counts, exit codes). If a check could not run, say
   which one and why.
5. Distinguish simulated results from real operations.
6. Clean up anything the verification created: temp files, test processes,
   fixtures.
7. Do not say "done" while any check you ran is failing.
