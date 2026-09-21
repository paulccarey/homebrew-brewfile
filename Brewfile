# brew bundle --global
#
# Everything here installs on every machine except the "Work machine only"
# section at the bottom, which is gated on INDEED_USERNAME being set.

# Homebrew scrubs the environment before evaluating this file, so a bare
# INDEED_USERNAME never reaches ENV here -- only HOMEBREW_*-prefixed vars
# survive. INDEED_USERNAME is set by ~/.zprofile (via ~/env/etc/indeed_profile),
# so read it back out of a login zsh. Non-interactive, ~150ms, no rc to hang on.
# Set HOMEBREW_INDEED_USERNAME to skip the subshell.
WORK_MACHINE = [
  ENV["HOMEBREW_INDEED_USERNAME"],
  ENV["INDEED_USERNAME"],
  `/bin/zsh -lc 'printf %s "$INDEED_USERNAME"' 2>/dev/null`,
].any? { |v| !v.to_s.strip.empty? }

# --- Terminals & Editors ---
# GPU-accelerated terminal
cask "ghostty"
# feature-rich terminal emulator
cask "iterm2"
# GUI wrapper for vim
cask "macvim-app"
# VS Code editor
cask "visual-studio-code"

cask "mark-text"

# --- Browsers ---
# Google Chrome browser
cask "google-chrome"
# Dia browser by The Browser Company
cask "thebrowsercompany-dia"

# --- Communication ---
# Team messaging
cask "slack"
# WhatsApp desktop client
cask "whatsapp"

# --- Productivity & Window Management ---
# Keyboard-driven window manager
cask "rectangle"
# App launcher and productivity hub
cask "raycast"
# Clipboard manager with history
cask "maccy"
# Prevent display sleep on demand
cask "caffeine"

# --- Notes & Knowledge ---
# Markdown-based personal knowledge base
cask "obsidian"

# --- Media ---
# Music and podcast streaming
cask "spotify"
# Universal media player
cask "vlc"
# Voice/audio tool
cask "fluidvoice"
# Command-line audio/video converter and toolkit
brew "ffmpeg"

# --- Cloud & Storage ---
# Google Drive desktop sync
cask "google-drive"
# Cloudflare WARP VPN and DNS
cask "cloudflare-warp"
# FTP, S3, and cloud storage browser
cask "cyberduck"

# --- Development Tools ---
# Docker desktop and Linux VM alternative
cask "orbstack"
# API client (Bruno)
cask "bruno"

# --- AI Tools ---
# Anthropic Claude CLI
cask "claude-code"
# Chat GPT app
cask "chatgpt"
# OpenAI Codex CLI
cask "codex"
# Google Gemini desktop app
cask "google-gemini"
# Google AntiGravity
cask "antigravity"
# Google AntiGravity IDE
cask "antigravity-ide"
# Run and chat with local LLMs
cask "lm-studio"

# --- Brews: AI Tools ---
# Token-optimized CLI proxy — reduces Claude API token usage 60-90%
brew "rtk"
# AI-powered issue tracker and memory management
brew "beads"

# --- Brews: Version Management ---
# Multi-runtime version manager (ruby, node, python, etc.)
brew "asdf"

# --- Brews: Environment & Secrets ---
# Load/unload env vars from .envrc based on current directory
brew "direnv"
# Bitwarden CLI for secrets access in terminal
brew "bitwarden-cli"

# --- Brews: Git & Dev Workflow ---
# GitHub CLI
brew "gh"
# GitLab CLI
brew "glab"
# Syntax-highlighted, side-by-side git diff pager
brew "delta"
# Backup and restore macOS app configuration
brew "mackup"

# --- Brews: Build Dependencies ---
# GnuPG — required by asdf plugins and general crypto
brew "gpg"
# GNU awk — required for building various tools
brew "gawk"
# PostgreSQL client library — required to build the pg gem
brew "libpq"
# File watcher — required by VS Code extensions (e.g. Sorbet)
brew "watchman"

# --- Brews: CLI Utilities ---
# General-purpose fuzzy finder for files, history, and more
brew "fzf"
# Fast and user-friendly alternative to find
brew "fd"
# Non-interactive network downloader
brew "wget"
# Smarter cd — learns frequent directories
brew "zoxide"
# Terminal log file viewer with filtering and highlighting
brew "lnav"
# Fast Python package and project manager
brew "uv"

# --- Hardware & Making ---
# Bambu Lab 3D printer slicing software
cask "bambu-studio"

# --- Fonts ---
# Terminal font for kitty (Ghostty bundles its own copy)
cask "font-jetbrains-mono"

# --- Mac App Store ---
# Bitwarden password manager
mas "bitwarden", id: 1352778147
# Apple presentation app
mas "Keynote", id: 361285480
# Apple word processor
mas "Pages", id: 361309726
# Apple spreadsheet app
mas "Numbers", id: 361304891

# --- Work machine only (INDEED_USERNAME is set) ---
if WORK_MACHINE
  tap "datadog-labs/pack"
  tap "atlassian/homebrew-acli"
  tap "sourcegraph/src-cli"
  tap "ai4dp/ensemble", "ssh://git@code.corp.indeed.com/ai4dp/ensemble.git"

  # AI-assisted code editor built on VS Code
  cask "cursor"
  # JetBrains IDE suite manager
  cask "jetbrains-toolbox"
  # Indeed AI4DP Ensemble
  cask "ai4dp/ensemble/ensemble"

  # Kubernetes CLI
  brew "kubectl"
  # Terminal UI for Kubernetes cluster management
  brew "derailed/k9s/k9s"
  # Rust compiler — required for Ruby 3.2 native extensions
  brew "rust"

  # Atlassian CLI for Jira and Confluence
  brew "acli"
  # Datadog CLI
  brew "datadog-labs/pack/pup"
  # Sourcegraph CLI for code search
  brew "sourcegraph/src-cli/src-cli"
end
