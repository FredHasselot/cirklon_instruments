# Git Hooks

Versioned git hooks for this repository.

## Activation

`core.hooksPath` is a local setting and is **not** carried by a clone. Run this once
per clone, from the repository root:

```bash
git config core.hooksPath hooks
```

Without it, git keeps looking in `.git/hooks/` and the hooks below never run.

## `pre-commit`

Keeps the version badge in the root `README.md` in sync with the commit count.

- Version format: `0.1.<number of commits>`
- Only the `v0.1.x` badge is rewritten. Manual references such as `v1.11`, `v2.0`,
  `v31.0`, `v1.20` and `v8` do not match the pattern and are left untouched.
- The badge sits inside an ASCII box, so the surrounding spaces are adjusted to keep
  the right border aligned when the digit count changes.
- The hook re-reads the badge after substitution. If the badge is missing, or if the
  rewrite did not happen, it **aborts the commit** instead of reporting a success that
  did not occur.

### Portability note

The substitution uses `sed -E`. The BRE form `\+` is a GNU extension: the BSD `sed`
shipped with macOS does not treat it as a quantifier, so a `\+` pattern silently
matches nothing.
