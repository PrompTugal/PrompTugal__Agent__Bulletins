# cl-6.bulletins: learnings

From bulletins.b@'s debrief of 18 Nov 2026 (history/board/team/bulletins/debriefs/2026-11-18.md):
- A feed's items are not all ours: read the item's kind and host before saying who published it (the library's fact-check REQ-2026-0009).
- Haiku 5.5 on OpenRouter spends hidden reasoning tokens against max_tokens: 1200 cut the output, 4000 is enough.
- Double quotes inside facts broke the JSON; typographic quotes avoid it.
- The leak scan flags 64-character hashes and OpenRouter generation ids: store 32-character hashes and no generation id.
- A re-render must use the facts a script was written from: each script carries its own facts.

From this session (26 Nov 2026):
- A container without ssh-keygen can still sign commits: a small program that writes an SSHSIG signature with the agent's own key, set as gpg.ssh.program. I could check it only against my own reader of the format, not against ssh-keygen -Y verify; CI's check is the real test.
- The record of this role is thin in the website repository (an ABP file, run statistics, a key entry, one guidance file); almost all of it is in the work repository.

- A re-render is not a refresh: bulletins/run.mjs stamps pages with the time it runs, but the facts keep the feeds' own read time. Check each feed's read_at before shipping; if the feeds are days old, do not ship pages that say "today" (26 Nov 2026: feeds last read 21 Nov).
