# Contributing to Code to Cloud

Thanks for taking the time to contribute! This project exists to help novice developers get comfortable with version control, containers, and cloud deployment — and ironically, contributing to it is a great way to practise exactly those skills.

---

## Ways to contribute

- **Fix a typo or clarify an explanation** — always welcome
- **Add or update a resource link** — if you find a better video or article for a chapter
- **Improve a code example** — more realistic, more beginner-friendly, or updated for newer tooling
- **Add a checklist item** — something your team catches in code review that others should know
- **Translate the tutorial** — open an issue first to coordinate

---

## Ground rules

- Keep the audience in mind — this is for **novice developers**, not experienced engineers
- One concern per pull request — don't bundle unrelated changes
- Test locally before opening a PR — open `index.html` in a browser and check your section looks right
- Write a clear PR description: **what changed, why, and how to verify it**

---

## Step-by-step contribution workflow

This workflow mirrors what the tutorial itself teaches — good practice!

```bash
# 1. Fork the repo on GitHub, then clone your fork
git clone https://github.com/<your-username>/code-to-cloud.git
cd code-to-cloud

# 2. Create a branch named after your change
git checkout -b fix/update-docker-commands
# or
git checkout -b feat/add-go-dockerfile-example

# 3. Make your changes to index.html (or other files)

# 4. Preview locally
open index.html
# or: python3 -m http.server 8080

# 5. Commit with a clear message
git add .
git commit -m "Update Docker push command to use Artifact Registry v2 format"

# 6. Push your branch to your fork
git push origin fix/update-docker-commands

# 7. Open a Pull Request on GitHub against the main branch
```

---

## Branch naming conventions

| Type | Pattern | Example |
|------|---------|---------|
| Bug fix | `fix/short-description` | `fix/broken-networking-diagram` |
| New content | `feat/short-description` | `feat/add-terraform-chapter` |
| Typo / copy | `copy/short-description` | `copy/clarify-commit-formula` |
| Resources | `resources/chapter-name` | `resources/docker-links` |

---

## Commit message format

Follow the same Conventional Commits style the tutorial teaches:

```
fix: correct port number in networking diagram
feat: add Go Dockerfile example to Docker chapter
docs: update README with new GCP region note
```

---

## Reporting issues

Open a GitHub Issue if you:
- Find incorrect or outdated information
- Notice a broken link or embed
- Want to propose a new chapter before writing it

Use the issue title format: `[Chapter 04] Docker build command outdated`

---

## Code of conduct

Be kind. This project is aimed at beginners — keep feedback encouraging, not discouraging. Constructive criticism of content is welcome; criticism of contributors is not.
