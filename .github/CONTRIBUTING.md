# Contributing to the Front

> This is the organization-wide fallback guide. Individual repositories may ship
> a stricter `CONTRIBUTING.md` — when a repo has its own copy, **that one wins**.

We do not accept contributions that merely *work*. We accept contributions that
are well-formed. `0x02` Aesthetic Rigor is not decoration; it is review criteria.

## 1. Before you write code

Open an issue first. If the change belongs to `sable` (storage) versus
`sable-vector` (retrieval), say so explicitly — see the
[cross-layer case study](https://github.com/H-I-F/sable-vector/blob/main/docs/case-studies/cross-layer-bugfix.md)
for how often "it's the index" turns out to be "it's the daemon holding a deleted
inode".

Small = mergeable. A PR that touches storage, indexing and packaging at once gets
sent back, regardless of how good each part is.

## 2. Toolchain

| Tool | Purpose |
| :--- | :--- |
| Python 3.10 / 3.11 | Supported runtimes (matrix in CI) |
| `pytest` | Test suite; must be green locally |
| `ruff` | Lint + format gate in CI |

```bash
pip install -e ".[test,lint]"
ruff check .
pytest -q
```

## 3. Commit convention

We use [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(index): add nprobe sweep helper
fix(engine): pin snapshot sequence on memtable reads
docs(readme): correct materialise() signature
```

`feat` / `fix` / `docs` / `refactor` / `perf` / `test` / `chore` / `ci` are all in
use. Breaking changes get a `!` and a `BREAKING CHANGE:` footer.

## 4. Pull request rules

- Every PR needs a **statement of intent** — what changes, why, and how it was
  verified. Use the inherited PR template.
- Tests are not optional for behavioural changes. A fix without a regression
  test is a rumour.
- Include the **exact verification commands** you ran and their output. Reviewers
  should be able to reproduce without guessing.
- Root cause over symptom suppression. If you patched around a bug, explain why
  the underlying cause could not be fixed.
- CI must be green: lint, type checks and the full test matrix.

## 5. What we reject

- Generated code dumps with no explanation.
- Dependency additions that duplicate existing capability.
- Formatting-only churn mixed with behavioural changes.
- Anything claiming a test passes when the suite was never run.

---

<sub>Signals travel faster than committees. Send the patch.</sub>
