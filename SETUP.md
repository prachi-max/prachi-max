# How to put this on the GitHub profile

## The one thing that makes it work

GitHub has a hidden rule: if you create a repository whose **name is exactly your
username**, GitHub shows that repository's README on your profile page.

That is the whole trick. Nothing else is special about it.

    Username:   prachi-nawale
    Repo name:  prachi-nawale     <- must match exactly, including capitals

---

## Step by step

**1. Create the repository**

- GitHub → New repository
- Repository name: type your username exactly
- A message appears: *"You found a secret! ... this special repository"* — that
  confirms the name is correct
- Visibility: **Public** (it will not show on your profile if it is private)
- Tick **Add a README file**
- Create

**2. Add the files**

Copy into the new repository:

    README.md
    .github/workflows/snake.yml
    .github/workflows/profile-3d.yml

**3. Replace the placeholders**

Open `README.md` and find-and-replace:

| Find | Replace with |
|---|---|
| `USERNAME` | the real GitHub username |
| `YOUR-LINKEDIN` | the LinkedIn profile slug |

**4. Turn on write permission for Actions**

Both workflows push files back into the repository, so they need permission:

- Repository → **Settings** → **Actions** → **General**
- Scroll to **Workflow permissions**
- Select **Read and write permissions** → Save

Skip this step and both workflows fail with a `403` error.

**5. Run the workflows once by hand**

- Repository → **Actions** tab
- If prompted, click *"I understand my workflows, enable them"*
- Click **Generate Snake Animation** → **Run workflow**
- Click **Generate 3D Contribution Graph** → **Run workflow**

Each takes about a minute. After that they run on a schedule.

---

## What each part of the README needs

| Section | Needs |
|---|---|
| Banner, typing text | Nothing — works immediately |
| Badges (Gmail, LinkedIn…) | Just the placeholder replacement |
| GitHub Stats, Top Languages | Nothing — reads public data |
| Streak stats | Nothing |
| Activity graph | Nothing |
| **3D contribution graph** | The `profile-3d.yml` workflow to run first |
| **Snake animation** | The `snake.yml` workflow to run first |
| Profile views counter | Nothing |

If a workflow has not run yet, its image shows as broken. Run the workflow and it fixes itself.

---

## Things that break, and why

- **Repository is private** → the README does not appear on the profile at all.
- **Workflow permissions not set to read/write** → both workflows fail with `403`.
- **Streak stats image broken** → `github-readme-streak-stats.herokuapp.com` is a free
  community service that goes down occasionally. It is not your fault and it usually
  comes back. If it stays broken, delete that one line.
- **Everything is hosted by third parties.** The banner, typing text, stats cards, activity
  graph and quote all come from free community services (Vercel-hosted, mostly). They are
  widely used and stable, but none of them are run by GitHub. If one disappears, that image
  breaks and you delete the line.
- **Do not put a personal access token in the workflow files.** The built-in
  `secrets.GITHUB_TOKEN` is enough for both. A token pasted into a public repository is
  live within minutes of being pushed.
