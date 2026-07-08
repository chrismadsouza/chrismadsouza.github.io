# Editing chrismadsouza.github.io

Your site now runs on **Hugo** with the **academimal** theme. Every time you push a change to the `master` branch, GitHub Actions automatically rebuilds and republishes the live site at https://chrismadsouza.github.io/ — usually within 1–2 minutes.

## Where things live

| Section | File |
|---|---|
| About | `content/sections/aboutme.md` |
| CV | `content/sections/cv.md` (links to `static/pdf/cv_github.pdf`) |
| Research | `content/sections/research.md` |
| Publications | `data/publications/list.yaml` (auto-generated list, not plain Markdown — see below) |
| Teaching | `content/sections/teaching.md` |
| Contact | `content/sections/contact.md` |
| Site title / short bio / photo | `config.toml` |
| Section order / headings | `layouts/index.html` and `layouts/partials/sidebar.html` |

The About/CV/Research/Teaching/Contact files are plain **Markdown** — no HTML needed for normal edits. Publications is different: it's a data file (YAML) that auto-generates its section, described below.

## Making an edit directly on GitHub (no local setup needed)

1. Go to the repo: https://github.com/chrismadsouza/chrismadsouza.github.io
2. Navigate to the file you want to change (e.g. `content/sections/research.md`).
3. Click the **pencil icon** (Edit this file) in the top right.
4. Make your changes. Markdown basics:
   - `**bold text**` → **bold text**
   - `### Heading` → a subheading (used for "Work in Progress" in Research)
   - `[link text](https://example.com)` → a clickable link
   - Blank line = new paragraph
5. Scroll down, add a short commit message describing the change, and click **Commit changes directly to the `master` branch**.
6. Wait ~1–2 minutes, then check https://chrismadsouza.github.io/ — GitHub Actions will have rebuilt and redeployed automatically.

## Checking whether a deploy succeeded

Go to the **Actions** tab: https://github.com/chrismadsouza/chrismadsouza.github.io/actions
A green checkmark next to "Deploy Hugo site to Pages" means it's live. A red X means something broke — click into it to see the error (most commonly a Markdown/TOML syntax typo).

## Updating your CV

1. Go to `static/pdf/` in the repo.
2. Delete the old `cv_github.pdf` (or upload a new file with the same name to overwrite it) via **Add file → Upload files**.
3. Commit to `master`.

## Adding another research or teaching entry

Add another paragraph in the same style, e.g. in `research.md`:

```
### Work in Progress

**Long-term Impact of Short-term Subsidies.** (with Farzana Afridi and Prabhat Barnwal)

**Your New Paper Title.** (with Coauthor Name)
```

Or in `teaching.md`:

```
AEM 4420/5420: Emerging Markets, (Fall 2025)

AEM 4510: Environmental Economics, (Spring 2026)

Your New Course: Course Title, (Term Year)
```

## Adding a publication

Publications aren't edited as prose — they're entries in `data/publications/list.yaml`, which automatically renders as a "Publications" section between Research and Teaching (only shows up once you add at least one entry). Edit that file on GitHub and add an entry under `works:`, following YAML formatting (indentation matters):

```yaml
works:
  - title: "Your Paper Title"
    pdflink: "/pdf/your_paper.pdf"
    book: "Journal Name, Year"
    coauthors: "Coauthor One and Coauthor Two"
    links:
      - url: "/pdf/appendix.pdf"
        text: "Online Appendix"
    abstract: >
      Optional short abstract text goes here.
```

Notes:
- `pdflink`, `coauthors`, `links`, and `abstract` are all optional — include only what you have.
- If you reference a PDF (via `pdflink` or `links`), upload it to `static/pdf/` first (same process as updating your CV, below), then point to it as `/pdf/filename.pdf`.
- Each new entry is another `- title: ...` block at the same indentation level as the example above.

## Editing site-wide settings

`config.toml` controls the page title and short bio shown under your name:

```toml
title = "Chrisma Dsouza"
[params]
    shortbio = "Your one-line bio shown at the top of the page"
    logo = "Capture.JPG"
```

## Things to be careful about

- **Don't touch the `themes/academimal` folder** — it's a pinned theme dependency (a git submodule), not regular content. Editing it directly on GitHub can break the submodule link.
- **Don't rename section files** (e.g. `aboutme.md`) unless you also update `layouts/index.html` and `layouts/partials/sidebar.html` to match — those files reference the section filenames directly.
- For a bigger redesign, layout change, or new section type, it's easiest to ask me again — that involves editing Hugo templates, not just content.

## If something breaks

Every past version of every file is preserved in GitHub's history. To undo a bad edit:
1. Go to the file → **History** (clock icon) → find the last good version → **View** → **Edit this file** → copy its content back → commit.
2. Or ask me to roll it back for you.
