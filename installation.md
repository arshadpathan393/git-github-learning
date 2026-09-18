# Git + GitHub + VS Code — Complete Setup Steps

## 1. Install Git
Download and install **Git for Windows**.
During installation:
- **Components:** Keep the useful/default options enabled.
- **Start Menu Folder:** `Git`
- **Default editor:** Vim can be kept, but VS Code is preferable once VS Code is installed.
- **Initial branch name:** Select **Override** and use:
  `main`
- **PATH environment:** Select:
  `Git from the command line and also from 3rd-party software`
- **HTTPS transport:** Select:
  `Use the native Windows Secure Channel library`
- **Line endings:** Select:
  `Checkout Windows-style, commit Unix-style line endings`
- **Terminal emulator:** Select:
  `Use MinTTY`
- **git pull behavior:** Select:
  `Merge`
- **Credential helper:** Select:
  `Git Credential Manager`
- **Extra options:** Keep:
  `Enable file system caching`
Install Git.
---

## 2. Verify Git
    Open Command Prompt:
        cmd
        git --version

    Expected:
        git version 2.55.0.windows.1

## 3. Configure Git Identity
    Set your global username:
        git config --global user.name "Arshad Pathan"

    Set your GitHub email:
        git config --global user.email "your-github-email"

    Verify:
        git config --global --list

## 4. Configure VS Code as Git Editor
    After installing VS Code:
        git config --global core.editor "code --wait"

    Verify:
        git config --global core.editor

    Expected:
        code --wait

    Also verify that the VS Code command works:
        code --version

## 5. Install VS Code
    Install Visual Studio Code.

    During installation, enable:
        Register Code as an editor for supported file types
        Add to PATH

    Then verify:
        code --version

## 6. Configure GitHub SSH Authentication
    Because GitHub is being used through SSH, create an SSH key on the new Windows installation.

    First check whether .ssh exists:
    dir %USERPROFILE%\.ssh

    If it doesn't exist:
    mkdir %USERPROFILE%\.ssh

## 7. Generate ED25519 SSH Key
    Run:
        ssh-keygen -t ed25519 -C "your-github-email" -f "%USERPROFILE%\.ssh\id_ed25519"

    When asked for a passphrase:
        Enter a passphrase, or

    Press Enter twice for no passphrase.

    This creates:
        id_ed25519

    Private key — never share this
    and:
        id_ed25519.pub

    Public key — this is the key added to GitHub.

## 8. Copy the Public Key
    Display it:
        type "%USERPROFILE%\.ssh\id_ed25519.pub"

    Copy the complete line beginning with:
        ssh-ed25519

## 9. Add SSH Key to GitHub
    In GitHub:
        Profile → Settings → SSH and GPG keys → New SSH key
    Enter a title such as:
        Office PC

    Paste the public key.
    Save it.

## 10. Test GitHub SSH Authentication
    Run:
        ssh -T git@github.com

    The first time, GitHub may ask:
        Are you sure you want to continue connecting (yes/no/[fingerprint])?

    Enter:
        yes

    Successful authentication looks like:
        Hi arshadpathan393! You've successfully authenticated,
        but GitHub does not provide shell access.

    This means:
        Office PC → SSH → GitHub = Working

## 11. Create Development Folder
    Create:
        D:\Development

    Inside it:
        D:\Development\Git_GitHub

    Final structure:
        D:\
        └── Development
            └── Git_GitHub

## 12. Open the Folder in VS Code
    From the terminal:
        cd /d D:\Development\Git_GitHub

    Then:
        code .
    VS Code opens the development folder.

## 13. Clone Existing GitHub Repositories
    Since the repositories already exist on GitHub, clone them instead of creating new repositories.

    Example:
        git clone git@github.com:arshadpathan393/git-github-learning.git
    
    This creates:
        D:\Development
        └── Git_GitHub
            └── git-github-learning

        Then open the repository in VS Code.

## 14. Verify the Cloned Repository

    Inside the repository:
        git status

    Expected:
        On branch main
        Your branch is up to date with 'origin/main'.

        nothing to commit, working tree clean

    Check the remote:
        git remote -v

    You should see the GitHub SSH repository configured as:
        origin

## 15. Normal Git + GitHub Workflow

    Once the setup is complete, the normal workflow is:

    Open VS Code
        ↓
    Open Repository
        ↓
    Edit/Create Files
        ↓
    git status
        ↓
    git add
        ↓
    git commit
        ↓
    git push
        ↓
    GitHub

    For getting changes from GitHub:

    GitHub
    ↓
    git pull
    ↓
    Local Repository
    ↓
    Continue Working
    Complete Environment

    After the setup, the environment looks like:

    Windows
    │
    ├── Git
    │    ├── Git Configuration
    │    ├── Git Credential Manager
    │    └── SSH
    │
    ├── VS Code
    │    └── Git Integration
    │
    └── Development
            └── Git_GitHub
                └── git-github-learning

    The important connection is:

    VS Code
    ↕
    Local Git Repository
    ↕ SSH
    GitHub