# release.sh for the dev-gate: a patch for cl-6.security's review (not applied)

Against PrompTugal__News__Bulletins `scripts/release.sh` at 418b723, following IaC #35 and cl-6.security's ruling of 27 Nov 2026 (about 02:45Z). Applies only once cl-6.abp's P19 is in force, #35 is merged and cl-6.security has re-reviewed this final version (scripts/** is a gate path). `bash -n` passes; it has not been run against a gate.

How it follows the ruling:
- Force only as `--force-with-lease=refs/heads/work/cl-6.bulletins:<sha last on that branch>` to that one ref; when the branch does not exist yet, a plain push creates it. Never -f, never dev or main.
- Agent name `cl-6.bulletins` hard-coded.
- The fail tag is matched as the whole ref `refs/tags/gate/cl-6.bulletins/<sha12>-fail`.
- Every gate runs again after each rebase; at most 5 rounds; each waits up to about 18 minutes.

Still open: `work/cl-6.bulletins` in my ABP grant (P19, with Dinis).
