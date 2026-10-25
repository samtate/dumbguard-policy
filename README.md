# DumbGuard policy

The signed policy that [DumbGuard](https://github.com/samtate/dumbguard-android)
phones enforce: which domains the DNS filter blocks, which apps are removed,
and which browsers are allowed. Phones poll
`dist/policy.signed.json` and accept it only if it is signed by a key built
into the app.

Forked from [drawbridge](https://github.com/Nilss3/drawbridge)'s policy and
lists (MIT), re-signed with DumbGuard's own key.

## Changing it

1. Edit `dist/policy.json` (or a list in `dist/lists/`). **Raise `version`**:
   phones refuse a document older than the one they hold.
2. Sign:

       python3 tools/policytool.py sign --key-id dumbguard-2026-10 \
           --in dist/policy.json --out dist/policy.signed.json

3. Commit and push. Phones pick it up on their next poll.

The private key is in `keys/`, which is never committed. Keep a copy offline:
without it no phone can be given a new policy.
