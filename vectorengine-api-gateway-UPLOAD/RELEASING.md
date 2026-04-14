# How to publish a release (tags & GitHub Releases)

This repo is **docs-first**; tags mark **documentation snapshots**, not API deployments.

## Option A — GitHub website (no CLI)

1. Push all files to `main` (`README.md`, `LICENSE`, `docs/`, `SECURITY.md`, etc.).  
2. Open **Releases** → **Draft a new release**.  
3. **Choose a tag** → type `v0.1.0` → **Create new tag on `main`**.  
4. **Release title:** `v0.1.0 — documentation`  
5. **Describe release:** paste the `[0.1.0]` section from [`CHANGELOG.md`](CHANGELOG.md).  
6. Publish release.

## Option B — Git command line

```bash
cd vectorengine-api-gateway
git add -A
git commit -m "chore: add LICENSE, docs, SECURITY, CHANGELOG"
git push origin main

git tag -a v0.1.0 -m "docs: initial public documentation bundle"
git push origin v0.1.0
```

Then on GitHub: **Releases** → **Draft a new release** → select tag `v0.1.0` → publish (optional but looks better than a bare tag).

## Option C — GitHub CLI (`gh`)

```bash
gh release create v0.1.0 --title "v0.1.0 — documentation" --notes-file CHANGELOG.md
```

(requires `gh auth login`)

---

**Bump version later:** edit `CHANGELOG.md`, new tag e.g. `v0.1.1`, repeat.
