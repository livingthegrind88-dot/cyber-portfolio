# OverTheWire Bandit — Levels 0–4

**Objective:** Get comfortable moving around a Linux filesystem over SSH and
reading files whose names or locations make them awkward to open.

**Environment:** SSH into the Bandit game server; each level's password unlocks
the next account.

## What I did
- **Level 0→1:** Logged in over SSH and read a plain `readme` with `cat`.
- **Level 1→2:** The password lived in a file literally named `-`. Because a bare
  dash is read as an option flag, I opened it with `cat ./-` to force a file path.
- **Level 2→3:** Filename had spaces, so I quoted it: `cat "spaces in this filename"`.
- **Level 3→4:** The file was hidden (dot-prefixed) inside a subdirectory. `ls -la`
  revealed it, then `cat` on the full path.

## What I learned
The big takeaway was how the shell *interprets* arguments — a dash means "option,"
spaces mean "separate arguments" — and how to escape both with `./` and quoting.
These aren't Bandit tricks; they're the everyday reasons a `cat` or `rm` command
"mysteriously" fails, and now I know why.

## Commands picked up
`ssh`, `cat`, `ls -la`, quoting and `./` to handle awkward filenames.
