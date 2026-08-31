# AI Generated Conventional Commits
A really nice, easy way to write commits without doing the work! Amazing hook that enforces [Conventional Commits](https://www.conventionalcommits.org/) because programmers are lazy!

Works on Linux, macOS, and Windows (via Git Bash, which ships with [Git for Windows](https://git-scm.com/download/win)).

## Installation
1. Install dependencies

Node.js is required (it powers both commitlint and the hook's JSON handling). `curl` is already included with Git for Windows and with most Linux/macOS systems.
```bash
npm install -g @commitlint/cli @commitlint/config-conventional
```

2. Configure global commitlint
```bash
mkdir -p ~/.config/commitlint
echo "module.exports = {extends: ['@commitlint/config-conventional']};" > ~/.config/commitlint/config.js
```

3. Download and enable the hook
```bash
curl -o .git/hooks/commit-msg https://raw.githubusercontent.com/aurevelle/automatic-conventional-commits/main/commit-msg
chmod +x .git/hooks/commit-msg
```

 OPTIONAL: To install globally instead of locally, replace step 3 with:
 ```bash
 mkdir -p ~/.config/git/hooks
 curl -o ~/.config/git/hooks/commit-msg https://raw.githubusercontent.com/aurevelle/automatic-conventional-commits/main/commit-msg
 chmod +x ~/.config/git/hooks/commit-msg
 git config --global core.hooksPath ~/.config/git/hooks
 ```

### Windows notes
Run all of the commands above from **Git Bash**, not from PowerShell or CMD. Git runs hooks
through its bundled shell, so the hook works no matter which terminal you actually run
`git commit` from.

If you download the hook with a browser or with PowerShell instead of `curl`, make sure the
file keeps **LF line endings**. A `commit-msg` saved with CRLF fails with an error like
`/bin/sh^M: bad interpreter`. To fix an already-broken file:
```bash
sed -i 's/\r$//' .git/hooks/commit-msg
```

The interactive prompt needs a terminal. GUI clients and IDEs that run `git commit` without
one will show the suggestion and then stop with a non-zero exit rather than committing, so
you can rerun the commit from a terminal to use the prompt.

## Configuration
The script requires a [Gemini API key](https://aistudio.google.com/api-keys).

On Linux/macOS, add this environment variable to your shell profile (~/.bashrc, ~/.zshrc, etc.):
```bash
export GEMINI_API_KEY="your_api_key_here"
```

On Windows, set it once as a user environment variable so every terminal and Git GUI can see it
(run this in PowerShell, then restart your terminal):
```powershell
setx GEMINI_API_KEY "your_api_key_here"
```

## Usage
Just use git exactly as you normally would:
```bash
git add .
git commit -m "fixing stuff"
```
Because it is **not** a valid conventional commit, the hook will intercept it, read your staged changes, and give you an interactive prompt:
```bash
Expected Format:
  <type>(<scope>): <description>

Generating suggestion based on changes...
  Suggestion:

fix(auth): resolve null pointer exception in login flow

What would you like to do?
  [y] Accept and commit
  [e] Edit this suggestion
  [n] Deny and exit
Choice (y/e/n):
```
