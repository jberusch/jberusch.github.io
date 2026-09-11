# jberusch.github.io

Jekyll blog at **<https://jberusch.github.io>** — plus two unlisted tools:

| | |
|---|---|
| **`/admin/`** | write posts and drafts into this repo |
| **`/brain/`** | capture notes into the private [`jberusch/brain`](https://github.com/jberusch/brain) vault, browse it, and promote a note into `_drafts/` |

Both are single self-contained HTML files that call the GitHub API from the browser with a
personal access token kept in `localStorage`. No server, no secrets committed. For local
dev, drop a token in `admin/dev-token.js` (gitignored — see `dev-token.js.example`).

```
_posts/    published        _layouts/   the one post layout
_drafts/   not built        writings/   standalone HTML essays
admin/     writing UI       brain/      capture UI → private vault
```

**Working on the note system? Start with [`CLAUDE.md`](CLAUDE.md)**, then
`jberusch/brain`'s own `CLAUDE.md`. Vault content is private and only ever reaches this
repo through `/brain/`'s publish button, which writes to `_drafts/`.
