# 🟡 Add a Pac-Man Animation to Your GitHub Profile

Bring your GitHub profile to life with a dynamic Pac-Man animation that plays across your contribution graph!  
Follow all the steps below — each action is preserved exactly, only enhanced for clarity and style.

---

## 🎯 Step 1: Create a New Repository

Create a new repository named **exactly** after your GitHub username.  
This special repository automatically becomes your profile’s homepage.

---

## ⚙️ Step 2: Set Up GitHub Actions

You’ll set up an automated workflow that generates and updates the Pac-Man contribution graph.

### 1. Create the Workflow Directory
Create the following folder inside your repository:

```
.github/workflows/
```

### 2. Add the Workflow File  
Inside that directory, create a file named **main.yml** and paste this content:

```yaml
name: generate pacman game

on:
  schedule: # Run automatically every 24 hours
    - cron: "0 */24 * * *"
  workflow_dispatch: # Allows manual triggering
  push: # Runs on every push to the main branch
    branches:
      - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: generate pacman-contribution-graph.svg
        uses: abozanona/pacman-contribution-graph@main
        with:
          github_user_name: ${{ github.repository_owner }}

      - name: push pacman-contribution-graph.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

This workflow builds a Pac-Man contribution graph daily and publishes it to the `output` branch.

---

## 🖼️ Step 3: Add the Pac-Man Graph to Your Profile README

To display your animated graph:

### 1. Create or edit your `README.md`
This is the file you're reading right now.

### 2. Embed the graph  
Replace **[USERNAME]** with your GitHub username:

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/[USERNAME]/[USERNAME]/output/pacman-contribution-graph-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/[USERNAME]/[USERNAME]/output/pacman-contribution-graph.svg">
  <img alt="Pac-Man contribution graph" src="https://raw.githubusercontent.com/[USERNAME]/[USERNAME]/output/pacman-contribution-graph.svg">
</picture>
```

---

## 🚀 Step 4: Push Your Changes and Enjoy!

Commit and push everything to GitHub.  
Within minutes, your profile will come alive with a playful Pac-Man animation running through your contribution grid.

This setup not only enhances your profile visually, but it also shows your mastery of GitHub Actions and profile customization.

---

Happy hacking - and enjoy your new animated GitHub profile! 🟡👾
