# OverTheWire Bandit — Levels 12–14

**Objective:** Progress through the Bandit levels via SSH, recovering each level's
password from files that require decoding, decompression, or key-based authentication.

**Environment:** SSH into each level of the Bandit game server; each level's
password unlocks the next account/level.

## Actions taken

**Level 12→13** — Moved the data file to /tmp as advised, then reversed the hexdump
with `xxd -r ~/data.txt data` to rebuild the binary. Confirmed the approach by
reading `man xxd` (noted `-r` = recover). Used `file` to identify the type at each
stage, renamed with the correct extension (e.g. `.bz2`), and decompressed
iteratively with `gzip`, `bzip2`, and `tar` — each layer revealed another
compressed file until the password surfaced.

**Level 13→14** — `ls` showed `sshkey.private` in the home directory. Attempted
`ssh -i sshkey.private bandit14@localhost` to authenticate with the key, but the
command failed. Reading the error, I determined SSH was using the wrong port;
the Bandit server uses 2220, so I retried with
`ssh -i sshkey.private -p 2220 bandit14@localhost`.

The connection was then refused with "Received disconnect ... no authentication
methods available." Analyzing this, I concluded SSH was rejecting the private key
because its file permissions were too open (no restriction applied to the key file).
Looked up `chmod` and applied `chmod 600 sshkey.private` so only the owner can read
or write it. Re-ran the SSH command and authenticated successfully.

## Result
Recovered the passwords for levels 12→13 and 13→14 and advanced to the next accounts.

## Takeaway
SSH silently refuses private keys whose permissions are too permissive — `chmod 600`
on the key file resolves it. Reinforced using `file` output to drive multi-layer
decompression, and reading error messages closely to diagnose port and auth failures.
