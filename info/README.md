# Git Information

This folder contains Git-related documentation and reference materials.

## Quick Reference

### Common Git Commands

```bash
# Check repository status
git status

# View changes
git diff

# Stage files
git add <file>

# Create commit
git commit -m "commit message"

# View commit history
git log --oneline -10

# Push to remote
git push

# Pull latest changes
git pull
```

### Workflow Guidelines

- Create commits only when explicitly requested by the user
- Do not commit files containing secrets (.env, credentials.json, etc.)
- Avoid force pushes to main/master branch
- Follow existing commit message style from git history

## Resources

- [Git Documentation](https://git-scm.com/doc)
- [GitHub Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
