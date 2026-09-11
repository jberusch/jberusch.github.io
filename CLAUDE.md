# Joe's blog — and the front door to his brain.

Two repos, one system.

- **This repo** (`jberusch/jberusch.github.io`, **public**) — the Jekyll blog at
  <https://jberusch.github.io>, plus two private-by-obscurity tools: a writing page at
  `/admin/` and a note-capture page at `/brain/`.
- **`jberusch/brain` (private)** — the vault the capture page writes into. His actual
  thinking lives there, not here.

**If Joe says `note: ...` to you, or asks you a question about his own thinking, the
answer is in the other repo and so are your instructions.** See *Working with the vault*
at the bottom of this file. Do not try to answer out of this repo's posts — they are the
published surface, a fraction of the material, and they lag the vault badly.

---

## This repo

Plain Jekyll on GitHub Pages. No build step you need to run; pushing to `main` publishes.

```
_posts/       published posts. permalink: /blog/:year/:month/:day/:title/
_drafts/      unpublished. Jekyll does NOT build these — a draft here is private.
_layouts/     one layout: post.html
writings/     hand-written standalone HTML essays (not posts)
index.html, about/, thoughts/, media/, privacy.html
admin/        the writing UI  (noindex)
brain/        the capture UI  (noindex)
```

`_config.yml` is twelve lines and does not need your help. Posts are kramdown/GFM.

### The two tools

Both are single self-contained HTML files that talk to the GitHub API straight from the
browser. There is no server and no secret in the repo — **Joe pastes a personal access
token into the page once and it lives in `localStorage`** (`brain_token`). In local dev
they fall back to `admin/dev-token.js`, which is **gitignored and must stay that way**.

- **`/admin/`** — writes posts and drafts into `_posts/` and `_drafts/` in *this* repo.
- **`/brain/`** — reads and writes `jberusch/brain`. Tabs: capture, inbox, threads, notes,
  sources, map. **Capture** writes one file to `inbox/` named
  `YYYY-MM-DD-HHMM-<slug>.md` with `type: capture` frontmatter and any thread chips he
  picked. It renders the private vault client-side via the git trees + blobs API, with a
  blob cache in `localStorage`.

Both are `noindex, nofollow`. Neither is linked from the site nav. If you touch either
file, keep it dependency-free and keep the token handling exactly as it is.

### The one bridge from private to public

`/brain/`'s reader has a **publish** button (`publishDraft()`), and it is the *only*
sanctioned path from the vault into this repo. It writes the note into **`_drafts/`**,
never `_posts/`, so Jekyll will not build or publish it — it is a staging area for turning
a note into a piece of writing, and it asks for confirmation first.

**Nothing else from the vault belongs in this repo.** Not in a post, not in a draft, not
in a commit message, not in an issue or PR. This repo is public and the vault is not. If
you are ever moving text from `brain` to here and Joe did not explicitly ask for it, stop.

---

## Working with the vault

If the work is about his thinking rather than about this website:

```bash
gh repo clone jberusch/brain ~/brain   # private; needs his gh auth
```

Then **read `~/brain/CLAUDE.md` in full** — it is the operating manual, and its *Start
here* section tells you exactly what to do with a `note: ...` or a question. `BRAIN.md`
next; that is the current map of threads, open questions and what's unfiled.

**The mode matters more than the mechanics: this is a suggestion and retrieval system,
and your job is not to push.** Organise his thoughts, file them, and put the relevant past
notes next to the new one. Do not nudge him about the job, the sabbatical, his career or
what he should write; do not generate takes, essay pitches or names for patterns he hasn't
named; do not tell him what he's missing or rank his ideas. If he asks for an opinion,
give it — the rule is about volunteering, not answering. The one standing exception is
**accuracy**: if the vault is factually wrong, say so and fix it.

The short version of the mechanics, so you are not useless before you've cloned it:

- The vault is `notes/` (atomic, flat, one idea each — `claim` | `question` | `spark` |
  `seed`), `threads/` (the organizing spine), `sources/`, and `inbox/` (raw captures,
  filed then deleted).
- **File what *he* said, not what Claude said.** Transcripts contain both sides; only his
  turns are his thinking.
- **Never invent a position for him.** Mark inference as `> [claude] ...`.
- **Supersede, never overwrite** when he changes his mind. The old claim stays.
- Unresolved tensions are finished notes. Don't tidy them into conclusions.
- Write in his voice: lowercase, direct, self-deprecating, willing to swear.
