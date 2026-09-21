# Homebrew Brewfile

Global Brewfile for setting up a new Mac. Installs apps, CLI tools, and Mac App Store apps via [Homebrew Bundle](https://github.com/Homebrew/homebrew-bundle).

## What's included

- **Apps**: Chrome, Slack, Zoom, VS Code, Cursor, Zed, Obsidian, Raycast, iTerm2, OrbStack, Notion, Spotify, etc.
- **CLI tools**: `gh`, `kubectl`, `fzf`, `direnv`, `asdf`, `delta`, `bitwarden-cli`, `rtk`, `uv`, `pup`, `acli`, `src-cli`, etc.
- **Mac App Store**: Bitwarden, Keynote, Pages, Numbers

## Profiles: work vs personal

The Brewfile is Ruby, so there is one file and no extra tooling. Everything
installs everywhere except the profile-specific blocks at the bottom:
`if WORK_MACHINE` holds work-only apps (Cursor, JetBrains Toolbox, Ensemble,
kubectl, k9s, rust, acli, pup, src-cli) and the taps they need, while
`unless WORK_MACHINE` holds personal-only apps (rekordbox).

A machine counts as a work machine when `INDEED_USERNAME` is set. Homebrew
scrubs the environment before it evaluates the Brewfile, so that variable never
reaches `ENV` directly -- the Brewfile reads it back out of a login zsh instead.
No setup needed on either machine. Export `HOMEBREW_INDEED_USERNAME` to skip
that subshell, or to force the work profile on a machine that lacks the var.

Check which profile you resolve to:

```bash
brew bundle list --all --global
```

---

## New machine setup

### One-liner (copy and paste)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" && \
  brew install git && \
  git clone https://github.com/paulccarey/homebrew-brewfile.git ~/.homebrew-brewfile && \
  ln -sf ~/.homebrew-brewfile/Brewfile ~/.Brewfile && \
  brew bundle --global
```


---

### Step by step

**1. Install Homebrew**

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

On Apple Silicon, add Homebrew to your PATH after install:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

**2. Clone this repo**

```bash
git clone https://github.com/paulccarey/homebrew-brewfile.git ~/.homebrew-brewfile
```

**3. Link the Brewfile globally**

`brew bundle --global` looks for `~/.Brewfile` by default.

```bash
ln -sf ~/.homebrew-brewfile/Brewfile ~/.Brewfile
```

**4. Install everything**

```bash
brew bundle --global
```

This installs all taps, formulae, casks, and Mac App Store apps. Takes 10–30 minutes on a fresh machine.

---

## Ongoing use

**After adding packages to Brewfile:**

```bash
brew bundle --global
```

**Check what's installed vs what's in the Brewfile:**

```bash
brew bundle check --global
```

**Remove packages no longer in Brewfile:**

```bash
brew bundle cleanup --global
```

**List everything that would be removed (dry run):**

```bash
brew bundle cleanup --global --dry-run
```

---

## Keeping it up to date

When you install something new and want to track it:

```bash
brew bundle dump --global --force
```

This overwrites `~/.Brewfile` with everything currently installed — useful as a starting point, but review and clean up the output before committing.

Or just manually add the entry to `Brewfile` and commit.
