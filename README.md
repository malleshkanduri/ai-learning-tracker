# AI Learning Tracker

Static GitHub Pages learning tracker for the UT Austin AI/ML curriculum and its Pluralsight equivalents.

## Repository contents

- `index.html` - complete application
- `data/progress.json` - GitHub-backed progress state
- `.github/workflows/pages.yml` - GitHub Pages deployment workflow
- `.nojekyll` - serve the repository as a plain static site

## Default GitHub sync settings

- Owner: `malleshkanduri`
- Repository: `ai-learning-tracker`
- Branch: `main`
- Progress file: `data/progress.json`

## Deploy

1. Create the GitHub repository `malleshkanduri/ai-learning-tracker`.
2. Push every file in this folder to the `main` branch.
3. Open repository **Settings -> Pages**.
4. Under **Build and deployment**, choose **GitHub Actions** as the source.
5. Open **Actions** and wait for **Deploy GitHub Pages** to finish.
6. The expected site URL is `https://malleshkanduri.github.io/ai-learning-tracker/`.

The workflow ignores commits that only change `data/progress.json`, so normal progress auto-saves do not redeploy the website.

## Enable GitHub auto-save

The application always saves changes to browser local storage first. GitHub sync is optional and adds cross-device persistence.

1. In GitHub, open **Settings -> Developer settings -> Personal access tokens -> Fine-grained tokens**.
2. Create a token restricted to **Only select repositories -> ai-learning-tracker**.
3. Give it **Repository permissions -> Contents -> Read and write**. No other write permission is needed by the tracker.
4. Open the deployed tracker.
5. Choose **More -> GitHub auto-save settings**.
6. The owner, repository, branch and data path are already prefilled. Paste the token.
7. Choose **Save settings & sync**.
8. Change one topic to **In Progress** and wait for the header to show **Saved to GitHub**.
9. In GitHub, open `data/progress.json`. A new auto-save commit should be visible.

Changes are saved locally immediately and GitHub writes are debounced by about 1.2 seconds.

## Token behavior and security

The GitHub token is stored in browser `sessionStorage`, not in the repository. This prevents the token from being exposed in the public site source. You normally need to enter it again after starting a new browser session.

Do not paste a token into `index.html`, `progress.json`, README, GitHub Actions variables exposed to the browser, or any committed file.

For unattended cross-device saving without re-entering a token, a static GitHub Pages site is not sufficient by itself; use GitHub OAuth or a small authenticated serverless backend so the write credential remains server-side.

## Backup

Use **More -> Export progress backup** to download a JSON backup. Use **Restore progress backup** to import it later.
