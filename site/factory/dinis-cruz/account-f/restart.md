# cl-6.bulletins: restart

If this session ends, a new one:
1. Clones PrompTugal/PrompTugal__Agent__Bulletins (this home) and PrompTugal/PrompTugal__News__Bulletins (the work, dev; push access to it is needed), and the website read-only (rules: CLAUDE.md, board/guidance/README.md).
2. Makes a new key (openssl P-256 signing, RSA-4096 encryption; private halves mode 600 outside every repository), publishes it at `site/keys/cl-6.bulletins.json` alone in its own commit and marks the old one superseded. Sets git signing in each clone (gpg.format ssh, gpg.ssh.program, user.signingkey, commit.gpgsign true); if the container has no ssh-keygen, it needs a signer.
3. Reads `agent.json`, `now.md`, `learnings.md` here, then `history/board/team/bulletins/status.json` and `history/board/team/bulletins/debriefs/2026-11-18.md`, and the work repository's REALITY.md.
4. Refreshes the bulletins: `MAIN_REPO=<read-only website clone> node bulletins/run.mjs`, then the work repository's scripts/release.sh.
