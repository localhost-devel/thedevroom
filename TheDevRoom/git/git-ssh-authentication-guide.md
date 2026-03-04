# Git Authentication Using SSH (First-Time Onboarding)

This guide helps you set up SSH for Git so `push`, `pull`, and `clone` work without typing your password each time.

## Quick Start (Linux/macOS)

Run these commands in order:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
```

Then:
1. Copy the printed public key.
2. Add it to your Git provider account (GitHub/GitLab/Bitbucket).
3. Test connection with the correct host command from Step 5.

## Prerequisites

- Git installed: `git --version`
- SSH installed: `ssh -V`
- A Git provider account: GitHub, GitLab, or Bitbucket

## Step-by-Step Setup

### 1. Check if you already have SSH keys

```bash
ls -al ~/.ssh
```

If you see `id_ed25519` and `id_ed25519.pub`, you can reuse them.  
If not, create a new key in Step 2.

### 2. Generate a new SSH key (recommended: Ed25519)

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

- Press Enter to accept default path: `~/.ssh/id_ed25519`
- Set a passphrase (recommended)

### 3. Start SSH agent and add your key

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### 4. Copy your public key and add it to your provider

Print key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Clipboard shortcuts:

- macOS: `pbcopy < ~/.ssh/id_ed25519.pub`
- Linux (xclip): `xclip -sel clip < ~/.ssh/id_ed25519.pub`
- Linux (xsel): `xsel --clipboard --input < ~/.ssh/id_ed25519.pub`

Where to paste:

- GitHub: `Settings -> SSH and GPG keys -> New SSH key`
- GitLab: `Preferences -> SSH Keys`
- Bitbucket: `Personal settings -> SSH keys -> Add key`

### 5. Test SSH connection

Use the command for your provider:

```bash
# GitHub
ssh -T git@github.com

# GitLab
ssh -T git@gitlab.com

# Bitbucket
ssh -T git@bitbucket.org
```

You may see a host authenticity prompt the first time. Type `yes`.

### 6. Clone repositories using SSH

Use SSH URLs (not HTTPS):

```bash
# GitHub
git clone git@github.com:user/repo.git

# GitLab
git clone git@gitlab.com:user/repo.git

# Bitbucket
git clone git@bitbucket.org:user/repo.git
```

### 7. If repo is already cloned with HTTPS, switch remote to SSH

Check current remote:

```bash
git remote -v
```

Update remote:

```bash
# Example (GitHub)
git remote set-url origin git@github.com:user/repo.git
```

Verify:

```bash
git remote -v
```

## Optional Git identity setup

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

## Troubleshooting (common first-time issues)

- `Permission denied (publickey)`:
  - Ensure your public key was added to the correct account.
  - Run `ssh-add ~/.ssh/id_ed25519` again.
  - Verify with `ssh -T` for the right provider host.
- Wrong repo URL type:
  - Use SSH URL format (`git@...:user/repo.git`), not `https://...`.
- Multiple keys/accounts:
  - Add a `~/.ssh/config` entry to map each host to the correct key.

## Security tips

- Use a strong passphrase for your private key.
- Never share your private key file (`~/.ssh/id_ed25519`).
- Rotate keys if your team/security policy requires it.

## References

- [GitHub: Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [GitLab: Use SSH keys to communicate with GitLab](https://docs.gitlab.com/ee/user/ssh.html)
- [Bitbucket Cloud: Set up personal SSH keys](https://support.atlassian.com/bitbucket-cloud/docs/set-up-personal-ssh-keys-on-linux/)
