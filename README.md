# Code to Cloud — Developer Field Guide

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/hosted-GitHub%20Pages-brightgreen)](https://jkmpod.github.io/code-to-cloud)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)](CONTRIBUTING.md)

An interactive, scrollytelling tutorial covering everything a novice developer needs before their first production deployment on Google Cloud Platform.

**🌐 Live site:** `https://jkmpod.github.io/code-to-cloud`

---

## What's covered in code-to-cloud

| Chapter | Topic |
|---------|-------|
| 01 | Why version control, containers, and CI/CD matter |
| 02 | Git & GitHub — concepts, branching, pull requests |
| 03 | Writing good commit messages |
| 04 | Docker & containerisation |
| 04b | Docker Compose — running multi-container apps locally and in deployments |
| 05 | Networking basics — DNS, ports, firewalls, VPC |
| 05 | Networking basics — DNS, ports, firewalls, VPC |
| 06 | Google Cloud Platform — the 8 services you'll actually use |
| 06b | Code quality — Ruff (Python) and Biome (JS/TS), linting in CI |
| 07 | CI/CD with Cloud Build |
| 08 | Interactive pre-deploy checklist |

Each chapter includes an embedded YouTube video and curated external resources.

## Developer Induction Program

The repository also hosts a companion **AI-Assisted Full-Stack Developer Induction** program — an interactive onboarding hub for new developers joining the team.

**🌐 Live:** `https://jkmpod.github.io/code-to-cloud/induction/`

### What the induction unit covers

| # | Module | Core Skill |
|---|--------|-----------|
| 01 | Full-Stack Thinking | Systems over features; the UI→API→Service→DB flow |
| 02 | System Lifecycle | Problem → Spec → API → Implement → Test → Deploy → Monitor |
| 03 | Learning Workflow | 7-step engineering process with expand/collapse stepper |
| 04 | GitHub Template | Repo structure, docs, AI usage log |
| 05 | API Design | Contracts, validation rules, structured errors |
| 06 | TDD in Practice | Red → Green → Refactor with full worked examples |
| 07 | PR Review Simulation | Annotated broken code; four classes of issues |
| 08 | AI Usage Guidelines | Do / Don't rules; mandatory disclosure |
| 09 | Prompt Library | Reusable prompts for API design, testing, debugging, review |
| 10 | Deployment Awareness | CI/CD, env config, monitoring |
| 11 | Final Checklist | 16-point self-assessment before submission |

---

## Running locally

No build step needed — it's a set of static HTML files.

```bash
# Clone the repo
git clone https://github.com/jkmpod/code-to-cloud.git
cd code-to-cloud

# Open directly in your browser
open index.html

# Or serve with Python's built-in server (avoids iframe quirks)
python3 -m http.server 8080
# Visit http://localhost:8080
```

---

## Deploying to GitHub Pages

This repo uses **GitHub Actions** to automatically deploy to GitHub Pages on every push to `main`.

### First-time setup

1. Push this repo to GitHub
2. Go to **Settings → Pages**
3. Under **Source**, select **GitHub Actions**
4. That's it — the workflow in `.github/workflows/deploy.yml` handles the rest

Every push to `main` will trigger a deploy. The live URL will be:
```
https://jkmpod.github.io/code-to-cloud
```

### Manual deploy (alternative)

If you prefer not to use Actions, you can also set Source to **Deploy from a branch**, select `main`, and set the folder to `/ (root)`. GitHub Pages will serve `index.html` directly.

---

## Repository structure

```
code-to-cloud/ 
├── README.md               # This file
├── LICENSE                 # MIT License
├── CONTRIBUTING.md         # How to contribute
├── CONTRIBUTORS.md         # Credits and acknowledgements
├── index.html              # The code-to-cloud tutorial
├── code-to-cloud
│   └── CLAUDE.md
├── induction/
│   └── index.html          # AI-Assisted Developer Induction
│   └── CLAUDE.md
├── wiki/                   # Source for GitHub Wiki pages
│   ├── Home.md
│   ├── UI-UX-Design.md
│   ├── Pedagogic-Design.md
│   ├── Examples-Used.md
│   └── Mini-Project-Idea.md
├── .gitignore              # Standard web project ignores
└── .github/
    └── workflows/
    │   └── deploy.yml      # GitHub Actions → GitHub Pages
    └── ISSUE_TEMPLATE/
        ├── feedback.yml    # Feedback on either program
        └── content_suggestion.yml
```
---

## Customising for your team

A few things worth updating before sharing with your developers:

- **GCP region** — search for `asia-south1` in `index.html` and replace with your team's actual region (e.g. `us-central1`, `europe-west1`)
- **Organisation name** — update `your-org` in the Git examples
- **Checklist items** — add team-specific checks to the pre-deploy checklist in Chapter 08

---

## Contributing

Contributions are welcome! Whether it's fixing a typo, updating a resource link, or adding a new chapter — all improvements are appreciated.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full workflow, branch naming conventions, and commit message format.

A short version:

```bash
git checkout -b fix/your-change
# make your changes
git commit -m "fix: describe what you changed"
git push origin fix/your-change
# open a Pull Request on GitHub
```

See [CONTRIBUTORS.md](CONTRIBUTORS.md) for a list of everyone who has contributed to this project.

---

## License

This project is licensed under the [MIT License](LICENSE) — you are free to use, modify, and distribute it, provided the copyright notice is retained.

---

*Built for novice developers · GCP Edition*