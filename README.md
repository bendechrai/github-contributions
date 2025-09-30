# GitHub Contributions Automator 🟩

Keep your GitHub contributions graph green with automated commits.

## What It Does

This GitHub Action automatically commits to your repository **every 30 minutes**, creating **48 commits per day**. This is well above the 30 commits needed for the darkest green square on your GitHub contributions graph.

## Setup (2 minutes)

### 1. Fork This Repository

Click the **Fork** button at the top right of this page.

### 2. Make Your Fork Private (Recommended)

Keep the green squares, hide the repo:

1. Go to your fork's **Settings**
2. Scroll to the bottom → **Change visibility** → **Make private**
3. Go to your GitHub profile [Settings](https://github.com/settings/profile)
4. Check the box for **"Include private contributions on my profile"**

Now your contribution graph shows green squares, but nobody can see this repo or that you're using it. It just looks like you're working on private projects! 🎭

### 3. Enable GitHub Actions

1. Go to your forked repository
2. Click the **Actions** tab
3. Click **"I understand my workflows, go ahead and enable them"**

### 4. Enable Write Permissions

**Critical step!** Without this, the action will fail with a 403 error.

1. Go to your fork's **Settings** → **Actions** → **General**
2. Scroll down to **"Workflow permissions"**
3. Select **"Read and write permissions"** (not "Read repository contents and packages permissions")
4. Click **Save**

### 5. Activate the Scheduled Workflow

Scheduled workflows are disabled by default in forks. To activate it:

1. In your fork, click on `.github/workflows/auto-commit.yml`
2. Click the pencil icon (Edit this file)
3. Make any tiny change (add a space, change a comment, anything)
4. Scroll down and click **Commit changes**

That's it! The workflow will start running automatically every 30 minutes.

### 6. Verify It's Working (Optional)

- Go to the **Actions** tab in your fork
- You'll see the "Auto Commits" workflow
- Wait 30 minutes for the first automatic run, or click **Run workflow** to trigger it immediately
- After the first commit, check your contributions graph (may take up to 24 hours to update)

## How It Works

The action automatically:

- Uses **your GitHub noreply email** (`username@users.noreply.github.com`) so commits count toward your profile
- Commits to your **default branch** (required for contribution counting)
- Creates timestamps in `.auto-commit/activity.log` to ensure each commit is unique
- Attributes all commits to your account via `${{ github.actor }}`

## Customization

Want more or fewer commits per day? Edit the cron schedule in `.github/workflows/auto-commit.yml`:

- `*/30 * * * *` = every 30 minutes (48 commits/day) **← default**
- `0 * * * *` = every hour (24 commits/day)
- `0 */2 * * *` = every 2 hours (12 commits/day)

**Note:** From what we can tell, 30+ commits per day gives you the darkest green square.

## FAQ

**Q: Will this work in my fork?**  
A: Yes! Once you enable Actions and make a commit to the workflow file, it will use your username automatically.

**Q: Do I need to configure anything?**  
A: Nope! The action uses `${{ github.actor }}` which automatically becomes your GitHub username.

**Q: Will this spam my real projects?**  
A: No, commits only go to this forked repository.

**Q: Should I make my fork private?**  
A: Yes! That's the whole point. Make it private and enable "Include private contributions" in your [profile settings](https://github.com/settings/profile). You get green squares, but nobody knows you're using this tool.

**Q: How do I stop it?**  
A: Go to Actions tab → Click "Auto Commits" → Click the "..." menu → Disable workflow

**Q: Is this cheating?**  
A: Cheating at what? GitHub's contribution graph is a visual representation of public activity, not a measure of skill or productivity. If someone judges your employability by green squares, they're using a terrible metric. This project is designed to make "green dot counting" meaningless - if everyone can have a full green chart, then green dots don't signal anything. They're already a silly measure: they don't show private work, they reward quantity over quality, and they create pressure to perform for an algorithm instead of focusing on meaningful work. Use this tool to opt out of a game that shouldn't exist in the first place.

## Why GitHub Counts These Contributions

From [GitHub's documentation](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/managing-contribution-settings-on-your-profile/why-are-my-contributions-not-showing-up-on-my-profile):

✅ Commits are to the default branch  
✅ Commits use an email connected to your account (noreply email)  
✅ Commits are in a repo you own (your fork)  
✅ Not a fork of someone else's project (your fork becomes independent)

## Troubleshooting

**Action failing with "Permission denied" or 403 error?**

- Make sure you completed Step 4: Settings → Actions → General → "Read and write permissions"
- This is the most common issue!

**Contributions not showing up?**

- Wait up to 24 hours for GitHub to update your graph
- Check that Actions are enabled in your fork
- Verify the workflow has run (check the Actions tab)
- Make sure you made a commit to the workflow file to activate the schedule

**Want to verify the commit email?**

- Go to any commit in your fork
- Add `.patch` to the end of the URL
- Check that the `From:` field shows your `@users.noreply.github.com` email

## License

MIT - Fork it, modify it, use it however you want!
