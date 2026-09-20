# Setup Guide — Stephen's GitHub Profile README

Follow these steps once. After that everything updates itself automatically.

## 1. Create the special profile repository

1. Go to https://github.com/new
2. Repository name: **`StphenThy`** (must exactly match your username — this is what makes it show on your profile)
3. Set it to **Public**
4. Tick **Add a README file** (we'll overwrite it)
5. Click **Create repository**

## 2. Upload these files

Copy everything from this folder into the repo, keeping the structure:

```
StphenThy/
├── README.md
└── .github/
    └── workflows/
        ├── metrics.yml
        └── snake.yml
```

Either via the GitHub web UI (**Add file → Upload files**) or with git:

```bash
git clone https://github.com/StphenThy/StphenThy.git
cd StphenThy
# copy README.md and the .github folder in here, then:
git add .
git commit -m "Add animated profile README"
git push
```

## 3. Create a token for the Metrics card

The big metrics card (3D calendar, coding habits, etc.) needs a personal token.

1. Go to https://github.com/settings/tokens → **Generate new token (classic)**
2. Note: `METRICS_TOKEN`
3. Expiration: **No expiration** (or the longest available)
4. Scopes to tick: **`public_repo`**, **`read:org`**, **`read:user`**, **`repo`** (only if you want private-repo stats counted)
5. Click **Generate token** and **copy it** — you won't see it again

Now add it to the repo:

1. Open your `StphenThy` repo → **Settings → Secrets and variables → Actions**
2. **New repository secret**
3. Name: `METRICS_TOKEN` — Value: paste the token
4. **Add secret**

## 4. Allow Actions to write to the repo

`StphenThy` repo → **Settings → Actions → General** → scroll to **Workflow permissions** → select **Read and write permissions** → **Save**.

## 5. Run the workflows for the first time

Go to the **Actions** tab in the repo:

1. Click **Metrics** → **Run workflow** → **Run workflow**
2. Click **Generate Snake** → **Run workflow** → **Run workflow**

Wait 1–3 minutes. The metrics run creates `github-metrics.svg` on `main`; the snake run creates an `output` branch with the SVGs. Refresh your profile at https://github.com/StphenThy and everything should be live.

## 6. Personalize the remaining links

In `README.md`, search for and replace:

| Placeholder       | Replace with                          |
| ----------------- | ------------------------------------- |
| `YOUR_LINKEDIN`   | your LinkedIn profile slug            |
| `YOUR_EMAIL`      | the email you want people to use      |
| `YOUR_FACEBOOK`   | your Facebook username                |
| `YOUR_INSTAGRAM`  | your Instagram username               |

Delete any badge you don't want.

## Customizing

- **Typing text** — edit the `lines=` parameter in the typing SVG URL (separate lines with `;`, spaces as `+`).
- **Tech icons** — edit the `i=` lists in the skillicons URLs. Full icon list: https://skillicons.dev
- **Colors** — the theme uses GitHub's green palette: `0d1117` (bg), `238636`, `39d353`. Change these hex values across the URLs to re-theme.
- **Metrics plugins** — toggle anything in `.github/workflows/metrics.yml`. Docs: https://github.com/lowlighter/metrics
- **GIF** — swap the Giphy URL in the About Me section for any GIF you like.

## Troubleshooting

- **Metrics card shows a broken image** → the workflow hasn't run yet, or `METRICS_TOKEN` is missing. Check the Actions tab for the error.
- **Snake is broken** → the `output` branch doesn't exist yet; run the Generate Snake workflow.
- **Stats cards show "Maximum retries exceeded"** → the public github-readme-stats instance is rate-limited; it usually recovers in a few minutes.
