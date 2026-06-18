# LaTeX Thesis — Dev Setup

This is a LaTeX thesis project built for RWTH. It uses a devcontainer so you don't have to install a full TeX distribution locally. Here's what you need.

---

## What you need installed

### Docker
The whole TeX environment runs inside a container (`texlive/texlive:latest`). Docker Desktop handles that.

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) — make sure it's running before you open the project

### VS Code Extensions

Install these in VS Code:

| Extension | ID | Why |
|---|---|---|
| **Dev Containers** | `ms-vscode-remote.remote-containers` | Opens the project inside the Docker container |
| **LaTeX Workshop** | `James-Yu.latex-workshop` | Builds, previews, and syntax-highlights LaTeX |
| **LTeX** | `valentjn.vscode-ltex` | Grammar + spell check for LaTeX |

> LaTeX Workshop and LTeX get auto-installed inside the container — you only need Dev Containers on your host machine.

---

## How to open it

1. Open the folder in VS Code
2. Hit **Ctrl+Shift+P** → `Dev Containers: Reopen in Container`
3. Wait for Docker to pull `texlive/texlive:latest` (first time takes a bit)
4. Done — the environment is ready

---

## Building the PDF

The devcontainer is configured to auto-build on save. Full build chain:

```
pdflatex → bibtex → makeglossaries → pdflatex → pdflatex
```

To trigger manually: **Ctrl+Alt+B** in VS Code, or use the LaTeX Workshop sidebar.

Entry point is `thesis.tex`.

---

## Tracking changes with Git

Keeping a local repo is a great way to track your writing progress and roll back if something breaks.

```bash
git init
git add .
git commit -m "initial draft"
```

From there, just commit whenever you hit a milestone (finished a section, rewrote a paragraph, etc.). Build artifacts are already covered by `.gitignore` so only your actual `.tex` and `.bib` files get tracked.

If you ever mess something up, `git diff` shows exactly what changed, and `git checkout -- <file>` brings any file back to its last committed state.

---

## Notes

- Perl is required by `makeglossaries` for acronyms — it's included in the `texlive` image, so no separate install needed
- PDF preview opens in a VS Code tab (not an external viewer)
- Word wrap is on by default — the `.tex` files are long
