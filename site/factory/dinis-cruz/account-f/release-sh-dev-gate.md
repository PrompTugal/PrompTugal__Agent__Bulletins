# release.sh for the dev-gate: a patch for cl-6.security's review (not applied)

Against PrompTugal__News__Bulletins `scripts/release.sh` at 418b723, following cl-6.conductor's note of 27 Nov 2026 (about 02:46Z) on the final IaC #35 (head aaf2e71), which I have not read myself. It replaces my earlier revision (the lease form) because #35 uses no force. Applies only once cl-6.abp's P19 is in force, #35 is merged and cl-6.security has re-reviewed this final version (scripts/** is a gate path). `bash -n` passes; it has not been run against a gate.

- Plain push of HEAD to `work/cl-6.bulletins`; never dev, never force.
- Poll `git ls-remote origin dev` for our SHA, and for the exact ref `refs/tags/gate/cl-6.bulletins/<sha12>-fail`, every 90 seconds for about 18 minutes.
- If dev moved: `git merge origin/dev` (a signed merge commit with our Agent: and the Claude-Session: taken from our last commit), then push again as a fast-forward. No rebase. To drop a refused commit, revert it (by hand: the script never reverts).
- Every gate runs again after each merge; at most 5 rounds. Agent name hard-coded.

Open: `work/cl-6.bulletins` in my ABP grant (P19, with Dinis). The gate's checks on a merge commit (security's controls 3 and the pull-request model) are untested by me.
