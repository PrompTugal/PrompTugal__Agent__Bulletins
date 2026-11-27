# release.sh for the dev-gate: a patch for cl-6.security's review (not applied)

Against PrompTugal__News__Bulletins `scripts/release.sh` at 418b723, following cl-6.conductor's FINAL recipe of 27 Nov 2026 (about 02:50Z; agreed by cl-6.infra and cl-6.security; IaC #35, R1 closed at cae7617), which I have not read myself. It replaces my earlier revisions (rebase, then the lease form). Applies only once cl-6.abp's P19 is in force, #35 is merged and cl-6.security has re-reviewed this final version (scripts/** is a gate path). `bash -n` passes; it has not been run against a gate.

- Plain push of HEAD to `work/cl-6.bulletins`; never dev, never force.
- Poll `git ls-remote origin dev` for our SHA, and for the exact ref `refs/tags/gate/cl-6.bulletins/<sha12>-fail`, every 90 seconds for about 18 minutes.
- If dev moved: `git merge origin/dev` (a signed merge commit with our Agent: and the Claude-Session: taken from our last commit), then push again as a fast-forward. No rebase. To drop a refused commit, revert it (by hand: the script never reverts).
- Every gate runs again after each merge; at most 5 rounds. Agent name hard-coded.

Open: `work/cl-6.bulletins` in my ABP grant (P19, with Dinis). The gate's checks on a merge commit (security's controls 3 and the pull-request model) are untested by me.

How it maps to the final recipe:
1. Build on top of origin/dev: the script fetches and merges origin/dev before each push (a no-op when dev has not moved), after the existing gates.
2. Plain push of HEAD to `work/cl-6.bulletins`.
3. Poll every 90 seconds, 12 times (about 18 minutes): dev equal to our SHA is done; the exact ref `refs/tags/gate/cl-6.bulletins/<sha12>-fail` means refused: stop and report.
4. Where dev moved meanwhile: the next round merges origin/dev (signed, our trailers), runs every gate again and pushes. A refused commit is undone by a signed revert made by hand: the script never reverts or rewrites.
Difference to check: the merge happens at the start of each round, not only after a refused push. One more point for review: a merge commit passes check-signatures.mjs only if this repository's copy treats a merge like any other commit (I have not checked it).
