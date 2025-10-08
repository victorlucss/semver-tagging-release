# 🚀 Simple Release Workflow

This repository uses a streamlined GitHub Actions workflow that automatically handles versioning, changelog generation, and releases based on conventional commits.

## How It Works

### 1. **Automatic Trigger**
- Runs on every push to `main` branch
- Can be triggered manually via GitHub Actions UI
- Skips if commit message contains `[skip ci]`

### 2. **Version Calculation**
- Analyzes commits since the last tag using conventional commit format
- Calculates next version based on commit types:
  - `feat:` → Minor version bump (1.0.0 → 1.1.0)
  - `fix:` → Patch version bump (1.0.0 → 1.0.1)
  - `BREAKING CHANGE:` → Major version bump (1.0.0 → 2.0.0)

### 3. **What Happens When Version Changes**
1. **Updates `package.json`** with new version
2. **Generates changelog** with categorized changes:
   - 🚀 Features
   - 🐛 Bug Fixes  
   - 🔧 Maintenance
3. **Updates persistent `CHANGELOG.md`** file
4. **Commits changes** with `[skip ci]` to prevent loops
5. **Creates git tag** with the new version
6. **Creates GitHub Release** with changelog

### 4. **What Happens When No Changes**
- Workflow completes successfully
- No version bump, no commits, no tags created

## For Developers

### Writing Commits
Use conventional commit format for automatic versioning:

```bash
# Feature (minor bump)
git commit -m "feat: add user authentication"

# Bug fix (patch bump)  
git commit -m "fix: resolve login issue"

# Breaking change (major bump)
git commit -m "feat!: redesign API

BREAKING CHANGE: API endpoints have changed"

# Maintenance (patch bump)
git commit -m "chore: update dependencies"
```

### Manual Release
If you need to trigger a release manually:
1. Go to **Actions** tab in GitHub
2. Select **Simple Release** workflow
3. Click **Run workflow**
4. Choose branch and click **Run workflow**

### Skipping Release
To skip automatic release for a commit:
```bash
git commit -m "docs: update README [skip ci]"
```

## Workflow Steps Explained

| Step | Purpose | When It Runs |
|------|---------|--------------|
| **Checkout** | Get repository code | Always |
| **Setup Node.js** | Install Node.js 20 | Always |
| **Configure Git** | Set up git user for commits | Always |
| **Fetch tags** | Get latest tags from remote | Always |
| **Calculate version** | Determine next version from commits | Always |
| **Check if bump needed** | Compare current vs next version | Always |
| **Update package.json** | Bump version in package.json | Only if version changes |
| **Create changelog** | Generate categorized changelog | Only if version changes |
| **Commit changes** | Push version and changelog updates | Only if version changes |
| **Create tag** | Create git tag for release | Only if version changes |
| **Create release** | Create GitHub release with changelog | Only if version changes |

## Files Modified

- **`package.json`** - Version number updated
- **`CHANGELOG.md`** - Persistent changelog maintained
- **Git tags** - New version tag created
- **GitHub Release** - Release with changelog created

## Benefits

✅ **Simple**: One workflow handles everything  
✅ **Automatic**: No manual intervention needed  
✅ **Safe**: Only runs when version actually changes  
✅ **Clear**: Easy to understand what's happening  
✅ **Complete**: Handles versioning, changelog, and releases  

## Troubleshooting

### Workflow doesn't run
- Check if commit message contains `[skip ci]`
- Ensure you're pushing to `main` branch
- Check Actions tab for any errors

### Version not bumping
- Verify commit messages follow conventional format
- Check if commits are actually new since last tag
- Look at workflow logs for semver calculation details

### Changelog issues
- Check if commits are properly formatted
- Verify git history is clean
- Look at generated `CHANGELOG_NEW.md` in workflow logs
