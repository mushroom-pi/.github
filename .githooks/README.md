# Git hooks

`pre-commit` guards the one invariant this repository has: the organization
profile is **one deliverable in two files**.

| File | GitHub renders it on |
|---|---|
| `profile/README.md` — canonical | the organization page, `github.com/mushroom-pi` |
| `README.md` — mirror | the repository page, `github.com/mushroom-pi/.github` |

A symlink would render as plain text, so the second file is a real duplicate —
and the two must stay byte-identical, changed together. The hook fails the commit
when they diverge on disk, and also when only one of them was staged.

Hooks are not cloned, so enable it once per clone:

```sh
git config core.hooksPath .githooks
```

`git commit --no-verify` bypasses it in an emergency.

When the profile changes, edit `profile/README.md` first, then copy it over:

```sh
cp profile/README.md README.md
```
