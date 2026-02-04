# Documentation Futures for Technical Teams

> **TL;DR**: Just markdown. Just git. Render anywhere.

---

## The Pitch

```
Confluence → Markdown + Git → Render wherever you want
```

The destination isn't MKDocs specifically. It's **markdown as the source of truth**, version controlled in git, rendered by whatever tool fits:

| Renderer | Use Case |
|----------|----------|
| **GitHub/BitBucket** | Already there, free, good enough |
| **VS Code Preview** | While you're editing |
| **MKDocs Material** | When you want it pretty |
| **Local `mkdocs serve`** | Fast, offline, no hosting |

**You're not locked into anything.** Markdown is portable. Git is portable. The renderer is just presentation.

---

## The Workflow

```mermaid
flowchart LR
    A[Edit markdown] --> B[Commit to git]
    B --> C{Where to view?}
    C --> D[GitHub renders it]
    C --> E[VS Code renders it]
    C --> F[mkdocs serve locally]
    C --> G[Deploy to static host]
```

That's it. No WYSIWYG. No database. No vendor lock-in.

---

## What Renders for Free

### GitHub Markdown

GitHub renders markdown beautifully out of the box:
- Headers, lists, tables, code blocks
- Syntax highlighting for any language
- **Mermaid diagrams** (native support since 2022)
- Relative links between docs
- Inline images

### Mermaid Diagrams

No Gliffy. No paid plugins. Just text:

```mermaid
graph TD
    A[Confluence Page] -->|Export| B[Markdown]
    B --> C[Git Repo]
    C --> D[GitHub Renders]
    C --> E[MKDocs Renders]
    C --> F[VS Code Renders]
```

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant Git as Git Repo
    participant GH as GitHub

    Dev->>Git: git commit -m "update docs"
    Dev->>Git: git push
    Git->>GH: Webhook
    GH->>GH: Renders markdown
    Note over GH: Instantly viewable
```

Version controlled. Diffable. No binary blobs.

### Code Blocks

```sql
-- Syntax highlighting just works
SELECT
    d.department_name,
    COUNT(*) as headcount
FROM employees e
JOIN departments d ON e.dept_id = d.id
GROUP BY 1
ORDER BY 2 DESC;
```

```python
# Works for any language
def process_document(path: str) -> dict:
    """AI can read this. Confluence storage format? Not so much."""
    with open(path) as f:
        return parse_markdown(f.read())
```

---

## Audience Fit

Not everything belongs in markdown. Here's the honest breakdown:

```mermaid
quadrantChart
    title Documentation Tool Fit
    x-axis Low Technical Skill --> High Technical Skill
    y-axis Low Change Frequency --> High Change Frequency

    quadrant-1 MKDocs / GitHub
    quadrant-2 Confluence
    quadrant-3 SharePoint / TDX
    quadrant-4 Git + Markdown

    Runbooks: [0.85, 0.75]
    Architecture Docs: [0.80, 0.25]
    Onboarding: [0.40, 0.30]
    Meeting Notes: [0.30, 0.90]
    Support KB: [0.25, 0.50]
    Code Comments: [0.95, 0.60]
```

| Audience | Skill Level | Best Fit |
|----------|-------------|----------|
| SDDS Technical (AIA, ERP, DDS) | Git-native | **Markdown + Git** |
| Campus IT (broad) | Mixed | Confluence Cloud |
| Non-IT Collaborators | Low | Confluence / TDX |

**SDDS doesn't need Confluence for technical docs.** We live in git. Our docs should too.

---

## The AI Angle

This matters more than people realize:

| Format | AI Can... |
|--------|-----------|
| **Markdown** | Read directly, search, reference, update |
| **Confluence** | Requires export, conversion, loses structure |

A markdown-first knowledge base is immediately usable by AI tools. Every MCP, every code assistant, every search tool understands plaintext markdown.

Confluence storage format is proprietary XML soup.

---

## Conversion Reality

**Confluence → Markdown isn't that hard:**

1. Use the [Markdown Exporter](https://marketplace.atlassian.com/apps/1221351/markdown-exporter-for-confluence) marketplace app
2. Export space as markdown
3. Clean up (AI handles 80% of this)
4. Commit to git

**Gliffy diagrams:**
- Export existing as SVG (one-time)
- New diagrams in Mermaid (text-based, version controlled)
- Complex stuff in draw.io → export SVG

Jesse and I have done this. It's not painful.

---

## MKDocs Material (When You Want Pretty)

For documentation that needs polish:

```bash
# Install once
pip install mkdocs-material

# Serve locally
mkdocs serve
# → http://localhost:8000

# That's it.
```

**Features:**
- Beautiful Material Design theme
- Built-in search (client-side, fast)
- Dark mode toggle
- Mobile responsive
- Edit button → links to repo for direct editing

**But you don't need it.** GitHub rendering is often enough.

---

## Recommended Path for SDDS

```mermaid
flowchart TD
    A[Current: Confluence] --> B{Team Technical?}
    B -->|Yes| C[Migrate to Markdown + Git]
    B -->|No| D[Stay on Confluence Cloud]

    C --> E{Need Polish?}
    E -->|Yes| F[Add MKDocs Material]
    E -->|No| G[GitHub rendering is fine]

    F --> H[Team owns their instance]
    G --> H
    D --> I[IS manages centrally]
```

1. **Don't fight the campus service** — Confluence Cloud for broad IT use is fine
2. **Technical teams go their own way** — We manage our own markdown repos
3. **No central MKDocs service** — Teams own it, no burden on Tyf
4. **Start simple** — GitHub rendering first, MKDocs if needed

---

## Key Points

| Question | Answer |
|----------|--------|
| What's the actual proposal? | Markdown + git. Renderer is optional. |
| Does this replace Confluence? | For technical teams, yes. Campus-wide, no. |
| Who supports it? | Teams own their own repos |
| Is conversion hard? | No. AI helps. We've done it. |
| What about Gliffy? | Mermaid is better and free |
| What about search across teams? | GitHub search, or accept siloed docs |
| Is MKDocs sustainable? | MIT licensed, not VC-backed, stable |

---

## Resources

- [MKDocs Material](https://squidfunk.github.io/mkdocs-material/) — The pretty option
- [Mermaid Live Editor](https://mermaid.live/) — Try diagrams interactively
- [GitHub Markdown Demo](https://github.com/magpieE5/demo) — What renders natively
- [Markdown Exporter](https://marketplace.atlassian.com/apps/1221351/markdown-exporter-for-confluence) — Confluence → Markdown

**People:**
- **Ryan Leonard / NTS** — Already using MKDocs on campus
- **Jesse & Brock** — Experience with Confluence export, happy to help

---

> *The goal isn't to convince everyone to switch. It's to have markdown + git as a legitimate option for teams where it fits.*
