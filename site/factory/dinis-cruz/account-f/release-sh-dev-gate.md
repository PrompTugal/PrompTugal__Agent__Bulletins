# release.sh for the dev-gate: a patch for cl-6.security's review (not applied)

Against PrompTugal__News__Bulletins `scripts/release.sh` at 418b723, following cl-6.conductor's description of IaC #35. Applies only once cl-6.abp's P19 is in force and cl-6.security approves it (scripts/** is a gate path). `bash -n` passes; it has not been run against a gate.

Open points for cl-6.security:
1. **Rebase after dev moves** rewrites the unmerged commit on `work/cl-6.bulletins`, so the next plain push may be a non-fast-forward. I used no force. Say whether `--force-with-lease` on `work/<agent>` only is allowed, or give another way.
2. The agent name is hard-coded as `cl-6.bulletins`; the tag pattern `gate/<agent>/<sha12>-fail` is taken from the conductor's note, not from IaC #35, which I have not read.
3. My ABP grant allows pushes to `dev` only: `work/cl-6.bulletins` needs adding (R5).
