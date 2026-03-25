---
name: bento-project-command-center
description: "Operational knowledge base for the Bento Project Claude project. Contains SOPs, workflow templates, JQL recipes, stakeholder doc standards, domain context, Jira quirks, and session recovery procedures for the Bento Framework team at NCI/CBIIT."
---

# Bento Project Command Center — Skill Knowledge Base

> **Project:** Bento Framework
> **Ecosystem:** Cancer Research Data Commons (CRDC)
> **Projects Built on Bento:** ICDC (Integrated Canine Data Commons), CTDC (Clinical and Translational Data Commons)
> **Team:** React web application engineers
> **Claude Project:** Bento Project Command Center
> **Last Updated:** 2026-03-25

---

## 1. Session Recovery & Infrastructure

### 🐳 Docker / MCP Recovery

If any MCP tool (Jira/Atlassian, SharePoint/Playwright) is unavailable or returns a connection error, **Docker is not running** on the user's machine. Do not attempt workarounds, do not ask for manual data. Surface the issue immediately:

> "🐳 **Docker doesn't appear to be running.** The Jira/Atlassian MCP container needs to be active. Please start Docker and restore the container, then let me know when it's back up and I'll pick up right where we left off."

Wait for the user to confirm Docker is running before retrying any Jira or SharePoint operations.

### 🔄 MCP Session Initialization

After any session gap or cold start, **re-initialize MCP connections before the first tool call**. If tools fail on the first attempt, the fix is to refresh the project session and resend the message — do not retry in a loop or attempt workarounds.

### NIH SharePoint MFA Flow

The Bento SharePoint requires NIH MFA on each fresh browser session:
1. Navigate to `https://nih.sharepoint.com/sites/NCI-CBIIT-FNL-Bento/SitePages/ProjectHome.aspx`
2. Fill in the NIH email when prompted
3. Read the **2-digit number** shown on the MFA challenge screen and tell the user — they match it in Microsoft Authenticator
4. After approval, click "Yes" on the "Stay signed in?" prompt
5. Session stays authenticated for the rest of the conversation

---

## 2. Domain Context

### About Bento

Bento is a **construction kit for scientific data websites** developed by NCI/CBIIT. Instead of each research group building their data-sharing site from scratch, Bento provides reusable building blocks — React frontend, Java backend, Neo4j graph database — that any team can use to stand up a data commons.

**Three core principles:**
- **Data Agnostic** — Works with any biology data type (genomic, proteomic, transcriptomic, etc.)
- **Modular** — Frontend, backend, and database are independently upgradeable
- **Cloud Enabled** — Deployable on-premise, AWS, or GCP

**Reference implementation:** https://bento-tools.org/#/home (TAILORx breast cancer trial)

### Projects Built on Bento

| Project | Full Name | Live Site | Jira Key |
|---------|-----------|-----------|----------|
| ICDC | Integrated Canine Data Commons | https://caninecommons.cancer.gov | `ICDC` |
| CTDC | Clinical and Translational Data Commons | TBD | `CTDC` |

### Technical Architecture

- **Frontend:** React.js + Redux + Apollo Client (GraphQL)
- **Backend:** Java servlet + GraphQL API + REST API
- **Database:** Neo4j (graph database) + Cypher query language
- **Infrastructure:** AWS (ALB, EC2, S3, SQS) + Docker + Jenkins CI/CD
- **Monitoring:** New Relic (performance), Sumo Logic (logs)
- **Security:** Codacy, Twistlock, IBM AppScan

### Key GitHub Repositories

| Repo | Purpose |
|------|---------|
| `CBIIT/bento-frontend` | React frontend + all page config files |
| `CBIIT/bento-backend` | Java backend API server |
| `CBIIT/bento-model` | Bento Core Data Model (graph schema) |
| `CBIIT/BENTO-TAILORx-model` | Extended data model for reference implementation |
| `CBIIT/bento-docs` | Documentation source |
| `CBIIT/icdc-model-tool` | Data model validation tool used during ETL |

### Multiomics Context

The team works with multiomics data — datasets combining multiple biological measurement types (genomics, proteomics, transcriptomics, etc.). When writing tickets or summaries for stakeholders, explain it simply: *"data that measures many different biological signals from the same samples, like reading both the DNA instructions and the proteins those instructions produce."*

---

## 3. Jira — Bento Board

### JQL Recipes

```
# Everything on Bento, most recently updated
project = "Bento" ORDER BY updated DESC

# Open items by priority
project = "Bento" AND status != Done ORDER BY priority DESC

# Current sprint
project = "Bento" AND sprint in openSprints()

# Bugs only
project = "Bento" AND issuetype = Bug AND status != Done

# Epics only
project = "Bento" AND issuetype = Epic

# Items updated this week
project = "Bento" AND updated >= -7d ORDER BY updated DESC

# Blocked items
project = "Bento" AND sprint in openSprints() AND status = "Blocked"

# Unassigned open items
project = "Bento" AND sprint in openSprints() AND assignee is EMPTY AND status != Done
```

### Assignee Format
- Use full email address: e.g., `gina.kuffel@nih.gov`
- Do not use display names or usernames alone

---

## 4. SharePoint

**Bento SharePoint site root:**
```
https://nih.sharepoint.com/sites/NCI-CBIIT-FNL-Bento
```

**Project home:**
```
https://nih.sharepoint.com/sites/NCI-CBIIT-FNL-Bento/SitePages/ProjectHome.aspx
```

### Reading .docx Files — CRITICAL

Do NOT click a `.docx` file to open it in the browser. SharePoint renders `.docx` files inside an Office Online iframe (`officeapps.live.com`) — a different domain — and Playwright cannot read cross-origin iframes.

**Always use the SharePoint REST API method:**
```javascript
const apiUrl = `${siteUrl}/_api/web/GetFileByServerRelativeUrl('${encodeURIComponent(filePath)}')/$value`;
const res = await fetch(apiUrl, { method: 'GET', credentials: 'include' });
// Parse with native browser APIs only (no CDN libraries — CSP blocks them)
```

### Write Operations — Form Digest Required
```javascript
const digestRes = await fetch(`${siteUrl}/_api/contextinfo`, {
  method: 'POST', credentials: 'include',
  headers: { 'Accept': 'application/json;odata=verbose' }
});
const digest = digestData.d.GetContextWebInformation.FormDigestValue;
// Include 'X-RequestDigest': digest in write request headers
```

---

## 5. Stakeholder Document Standards

### Formatting Rules
- **Page size:** US Letter (never A4)
- **Font:** Arial throughout
- **Brand color for headers:** NCI Blue `#1F4E79`
- Keep technical jargon minimal — add a plain-English parenthetical if jargon is necessary
- Tables preferred over bullet walls for multi-ticket data
- Include Jira links as footnotes, not inline URLs (keeps docs readable in print)

### Epic Summary Document Structure
1. **Cover / Title Block** — Epic title, Jira key, date, TPM name, status badge
2. **Executive Summary** (3–5 sentences) — Problem, why it matters, expected outcome
3. **Scope & Objectives** — In-scope deliverables, out-of-scope callouts
4. **Work Breakdown** (table) — Ticket Key | Summary | Type | Status | Assignee | Story Points
5. **Progress Summary** — % complete, story points burned vs. total
6. **Risks & Blockers**
7. **Diagrams & Visuals** — Attach or note absence
8. **Next Steps / Open Questions**

---

## 6. Ticket Writing Standards

### Task Format
```
**Summary:** [Brief, actionable description]

**Context:**
[1–2 sentences on why this work is needed and what system/component it affects]

**Acceptance Criteria:**
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

**Technical Notes:**
[Any relevant implementation context, environment details, or dependencies]

**Related:**
- Epic: BENTO-XXXX
- Design: [link if applicable]
```

### Bug Format
```
**Environment:** [dev / qa / stage / prod]
**Severity:** [Critical / High / Medium / Low]

**Steps to Reproduce:**
1.
2.
3.

**Expected Behavior:**
[What should happen]

**Actual Behavior:**
[What actually happens]

**Screenshots/Logs:**
[Attach or paste]

**Related Epic:** BENTO-XXXX
```

---

## 7. Key Contacts & Roles

> Update this section as team membership changes.

| Role | Name / Email | Notes |
|------|-------------|-------|
| Senior Technical PM | gina.kuffel@nih.gov | Primary contact for Bento, ICDC, and CTDC |

---

## 8. Reference Links

| Resource | URL |
|----------|-----|
| Bento Reference Implementation | https://bento-tools.org/#/home |
| Bento Documentation Site | https://cbiit.github.io/bento-docs/master/index.html |
| bento-frontend | https://github.com/CBIIT/bento-frontend |
| bento-backend | https://github.com/CBIIT/bento-backend |
| bento-model | https://github.com/CBIIT/bento-model |
| BENTO-TAILORx-model | https://github.com/CBIIT/BENTO-TAILORx-model |
| bento-docs | https://github.com/CBIIT/bento-docs |
| icdc-model-tool | https://github.com/CBIIT/icdc-model-tool |
| Bento SharePoint | https://nih.sharepoint.com/sites/NCI-CBIIT-FNL-Bento/SitePages/ProjectHome.aspx |
| CRDC Overview | https://datascience.cancer.gov/data-commons |
| Bento Help Desk | mailto:bento-help@nih.gov |
| Bento Documentation Repo | https://github.com/kuffelgr/bento-documentation |

---

## 9. Claude Knowledge Base — Reference Library

> ⚠️ **Fetch-on-demand only. Do NOT auto-fetch these files at the start of every session.**
>
> Loading all files upfront consumes context window space before any real work begins.
> Fetch the relevant file(s) only when a task genuinely requires that context.

The `claude/` folder is a structured knowledge base. It stores things Jira and SharePoint cannot: decisions, rationale, conventions, and epic briefings optimized for Claude to read quickly. The `docs/` folder stores all generated project documents as Markdown files.

### Folder Structure

```
claude/
  SKILL.md              <- This file. SOPs, JQL, doc standards, reference links.
  epics/                <- One .md file per active epic. Claude-optimized briefings.
  decisions/            <- Scope, architecture, and process decision records.
  conventions/          <- Team conventions Claude applies automatically.
docs/
  releases/             <- Release reports and changelogs. One file per version.
                           Naming: bento-X.X.X-release-report.md
  meetings/             <- Meeting notes and action item summaries.
                           Naming: YYYY-MM-DD-[meeting-type].md
  stakeholder/          <- Executive summaries, one-pagers, external-facing artifacts.
                           Naming: YYYY-MM-DD-[description].md
  epics/                <- Epic-level summaries generated for stakeholders.
                           Naming: BENTO-XXXX-[epic-slug].md
README.md               <- Index of all generated docs. Always updated when a new doc is pushed.
```

### Generated Documents Convention

**Every document Claude generates must be:**

1. **Stored as a `.md` file** in the appropriate `docs/` subfolder (see structure above).
2. **Named consistently** using the patterns above — lowercase, hyphens, no spaces.
3. **Registered in `README.md`** — add a row to the "Generated Documents" table with the file path, a one-line description, and the date.
4. **Committed to `main`** via the GitHub MCP in the same session it is created, not deferred to later.

**Subfolder selection guide:**

| What you're generating | Where it goes |
|---|---|
| Release report, changelog, version summary | `docs/releases/` |
| Meeting notes, action items | `docs/meetings/` |
| Executive summary, one-pager, stakeholder brief | `docs/stakeholder/` |
| Epic status summary for external audience | `docs/epics/` |
| Anything that doesn't fit above | `docs/` root with a descriptive name |

**Example commit messages:**
```
docs: add Bento 4.0.0 release report and Bento X roadmap
docs: add 2026-03-25 sprint planning meeting notes
docs: add BENTO-2617 Webpack upgrade stakeholder summary
```

### Existing Generated Documents

| File | Description | Date |
|------|-------------|------|
| [`docs/releases/bento-4.0.0-release-report.md`](../docs/releases/bento-4.0.0-release-report.md) | Bento 4.0.0 release completion report and Bento X roadmap — full Jira-sourced breakdown of all completed work, bugs fixed, open QA tests, and roadmap items | 2026-03-25 |

### Fetch Strategy by Session Type

| Session Type | Fetch These Files |
|---|---|
| Epic-specific work (tickets, updates, doc generation) | `claude/epics/BENTO-XXXX.md` for that epic |
| Sprint planning or retrospective | `claude/conventions/workflow.md` |
| New session after a long gap | `claude/conventions/workflow.md` |
| Scope or deferral question | Relevant file under `claude/decisions/` |
| Reviewing a prior release or roadmap | `docs/releases/bento-X.X.X-release-report.md` |
| Quick one-off ticket work | No fetch needed — pull live from Jira |

### How to Add New Files

- **New epic created?** Generate `claude/epics/BENTO-XXXX.md` alongside the Jira tickets.
- **Scope or process decision made?** Add a `claude/decisions/YYYY-MM-topic.md` entry.
- **Team convention changes?** Update `claude/conventions/workflow.md`.
- **New generated document?** Place in the correct `docs/` subfolder, follow the naming convention, and register it in `README.md`. See the Generated Documents Convention above.

---

## 10. Maintenance Notes

- This file lives at `kuffelgr/bento-documentation/claude/SKILL.md`
- Update JQL recipes when Jira workflow statuses change
- Update Reference Links when new repos or resources are added
- Review stakeholder doc standards before each major release cycle
- New SOPs or workflow patterns discovered in Claude conversations should be added here
- When new files are added to `claude/`, update Section 9 so they remain discoverable
- When a new `docs/` subfolder is created, add it to the folder structure diagram in Section 9
- The "Existing Generated Documents" table in Section 9 is a quick-reference index; the canonical index is `README.md` at the repo root — keep both in sync
