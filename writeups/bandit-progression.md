# OverTheWire Bandit — Progression Log

A running index of completed Bandit levels, the technique each required, and the
key command used. No passwords or flags — techniques and methodology only. Each
level range links to its full FORM-001 write-up.

| Level | Technique | Key command(s) | Write-up | Solved |
|-------|-----------|----------------|----------|--------|
| 0→1 | Basic SSH + cat | `ssh`, `cat readme` | [bandit-00-04](./bandit-00-04.md) | ✓ |
| 1→2 | Oddly named file (dash) | `cat ./-` | [bandit-00-04](./bandit-00-04.md) | ✓ |
| 2→3 | Spaces in filename | `cat "spaces in this filename"` | [bandit-00-04](./bandit-00-04.md) | ✓ |
| 3→4 | Hidden file | `ls -la inhere/` | [bandit-00-04](./bandit-00-04.md) | ✓ |
| 4→5 | File type detection | `file ./-file*` | [bandit-05-08.md](./bandit-05-08.md) | ✓ |
| 5→6 | Find by size/permissions | `find inhere -type f -size 1033c ! -executable` | [bandit-05-08.md](./bandit-05-08.md) | ✓ |
| 6→7 | Find by owner/group | `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null` | [bandit-05-08.md](./bandit-05-08.md) | ✓ |
| 7→8 | grep for keyword | `grep millionth data.txt` | [bandit-05-08.md](./bandit-05-08.md) | ✓ |
| 8→9 | Unique line | `sort data.txt \| uniq -u` | [bandit-09-11.md](./bandit-09-11.md) | ✓ |
| 9→10 | Human-readable strings | `strings data.txt \| grep '==='` | [bandit-09-11.md](./bandit-09-11.md) | ✓ |
| 10→11 | Base64 decode | `base64 -d data.txt` | [bandit-09-11.md](./bandit-09-11.md) | ✓ |
| 11→12 | ROT13 | `cat data.txt \| tr 'A-Za-z' 'N-ZA-Mn-za-m'` | [bandit-09-11.md](./bandit-09-11.md) | ✓ |
| 12→13 | Hexdump reversal + decompression | `xxd -r data.txt > d`, then `file`/`gzip`/`bzip2`/`tar` iteratively | [bandit-12-14](./bandit-12-14.md) | ✓ |
| 13→14 | SSH private key auth + port | `ssh -i sshkey.private -p 2220 bandit14@localhost` | [bandit-12-14](./bandit-12-14.md) | ✓ |
| 14→15 | chmod 600 + key fix | `chmod 600 sshkey.private` | [bandit-12-14](./bandit-12-14.md) | ✓ |
| 15→16 | openssl s_client | `openssl s_client -connect localhost:30001` | | |
| 16→17 | nmap port scan + SSL | `nmap -p 31000-32000 localhost --open` | | |
| 17→18 | diff two files | `diff passwords.old passwords.new` | | |
| 18→19 | Remote SSH command | `ssh bandit18@localhost -p 2220 'cat readme'` | | |
| 19→20 | setuid binary | `./bandit20-do cat /etc/bandit_pass/bandit20` | | |
| 20→21 | — | — | | |
| 21→22 | — | — | | |
| 22→23 | — | — | | |
| 23→24 | — | — | | |
| 24→25 | — | — | | |
| 25→26 | — | — | | |
| 26→27 | — | — | | |
| 27→28 | — | — | | |
| 28→29 | — | — | | |
| 29→30 | — | — | | |
| 30→31 | — | — | | |
| 31→32 | — | — | | |
| 32→33 | — | — | | |
| 33→34 | — | — | | |

## Notes
- Write-up links point to FORM-001 incident reports in this folder.
- Levels 15–20 techniques are noted from the handbook daily plan — write-ups pending.
- Table updated as each level is completed and documented.
- No passwords, flags, or solutions — techniques and methodology only.
