# Setup Guide

Everything visual (badges, banner, stats cards, streak, LeetCode) works the moment you
commit `README.md` — no setup needed. The features below run as GitHub Actions inside
your `Randeepa23/Randeepa23` repo, so they need a bit of one-time configuration.

## 0. Turn on write access for Actions (needed by all four workflows)
Repo → **Settings → Actions → General → Workflow permissions** →
select **"Read and write permissions"** → Save.

## 1. Fill in the placeholders in README.md
| Placeholder | Where | Replace with |
|---|---|---|
| `assets/*.gif` | Featured Projects table | A short screen recording of each project (record with ScreenToGif/Kap/Peek, commit into an `assets/` folder) |
| `#` links in Featured Projects | Featured Projects table | Real repo / live-demo URLs |
| `YOUR_LEETCODE_USERNAME` | LeetCode Stats section | Your actual LeetCode username |
| Currently Learning badges | Currently Learning section | Your real in-progress courses/certs |

## 2. Contribution Snake (`snake.yml`)
No secrets needed. Just make sure step 0 is done, then run it once manually:
Repo → **Actions** tab → **Generate Snake Animation** → **Run workflow**.
It creates an `output` branch that the README already points to.

## 3. Metrics Dashboard (`metrics.yml`)
Needs a Personal Access Token (the default token doesn't have enough GraphQL access):
1. GitHub → **Settings → Developer settings → Personal access tokens → Tokens (classic)** → Generate new token
2. Scopes: `repo`, `read:user`, `user:email`
3. Copy the token → your `Randeepa23` repo → **Settings → Secrets and variables → Actions → New repository secret**
4. Name it `METRICS_TOKEN`, paste the value
5. Run the **Metrics Dashboard** workflow once manually (Actions tab)

## 4. Weekly Coding Activity (`waka-readme.yml`)
1. Create a free account at [wakatime.com](https://wakatime.com), install the WakaTime
   plugin for your editor (VS Code / PyCharm), and let it track a day of coding
2. Copy your API key from **WakaTime → Account Settings**
3. Add it as a repo secret named `WAKATIME_API_KEY`
4. Add a second secret `GH_TOKEN` — you can reuse the same PAT you made in step 3
5. Run the **Waka Readme** workflow once manually

## 5. Latest Activity feed (`latest-activity.yml`)
Uses the same `GH_TOKEN` secret from step 4 — nothing else to add. Run it once manually
to populate the section immediately instead of waiting 6 hours.

## 6. Spotify "Now Playing" (optional, most involved)
This one needs its own small deployment since it reads your live Spotify session:
1. Fork [novatorem/spotify-github-profile](https://github.com/novatorem/spotify-github-profile)
2. Create a Spotify app at [developer.spotify.com/dashboard](https://developer.spotify.com/dashboard)
   to get a Client ID and Secret
3. Deploy your fork to Vercel, adding the Spotify credentials as environment variables
   (the fork's README walks through the OAuth redirect step)
4. Replace the placeholder URL in README.md
   (`novatorem-randeepa23.vercel.app`) with your actual deployment URL

If you'd rather skip Spotify for now, just delete the "What I'm Listening To" section —
everything else works independently of it.

---

**Tip:** after wiring up secrets, trigger each workflow manually once from the
**Actions** tab instead of waiting for the cron schedule, so you can see the README
update immediately and catch any typos in a username/secret name.
