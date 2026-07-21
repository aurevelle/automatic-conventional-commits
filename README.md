# AI Generated Conventional Commits
A really nice, easy way to write commits without doing the work! Amazing hook that enforces [Conventional Commits](https://www.conventionalcommits.org/) because programmers are lazy!

## Installation
1. Install dependencies
```bash
sudo apt install jq -y
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

## Configuration
The script requires a [Gemini API key](https://aistudio.google.com/api-keys). Add this environment variable to your shell profile (~/.bashrc, ~/.zshrc, etc.):
```bash
export GEMINI_API_KEY="your_api_key_here"
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

