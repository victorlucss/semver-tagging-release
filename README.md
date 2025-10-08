# 🚀 Automated Release Management

This repository uses a streamlined approach to automatic versioning, changelog generation, and releases based on conventional commits.

## 📋 Workflows

### 1. **Release Workflow** (`.github/workflows/release.yml`)
- **Triggers:** Push to `main` branch
- **Purpose:** Automatic versioning and release management
- **Features:**
  - Calculates next version from conventional commits
  - Updates `package.json` automatically
  - Generates high-quality changelog
  - Creates git tags and GitHub releases
  - Uses Changesets for professional package management

### 2. **PR Validation** (`.github/workflows/simple-pr-validation.yml`)
- **Triggers:** PR opened, edited, or new commits
- **Purpose:** Ensures commit messages follow conventional format
- **Features:**
  - Validates all commits in PR
  - Comments with validation results
  - Provides fix instructions for invalid commits
  - Updates comment automatically on new commits

### 3. **Build on Tag** (`.github/workflows/build-on-tag.yml`)
- **Triggers:** New git tags created
- **Purpose:** Runs development and production builds
- **Features:**
  - Development build runs automatically
  - Production build requires manual approval
  - Environment-based approval workflow

## 🎯 How It Works

### For Developers

#### Writing Commits
Use conventional commit format for automatic versioning:

```bash
# Feature (minor version bump)
git commit -m "feat: add user authentication"

# Bug fix (patch version bump)  
git commit -m "fix: resolve login issue"

# Breaking change (major version bump)
git commit -m "feat!: redesign API

BREAKING CHANGE: API endpoints have changed"

# Maintenance (patch version bump)
git commit -m "chore: update dependencies"
```

#### PR Workflow
1. Create PR with conventional commits
2. PR validation automatically checks commit format
3. Fix any invalid commits if needed
4. Merge PR to `main`
5. Release workflow automatically:
   - Calculates next version
   - Updates `package.json`
   - Generates changelog
   - Creates tag and GitHub release

### Version Bump Rules

| Commit Type | Version Bump | Example |
|-------------|---------------|---------|
| `feat:` | Minor (1.0.0 → 1.1.0) | `feat: add new feature` |
| `fix:` | Patch (1.0.0 → 1.0.1) | `fix: resolve bug` |
| `BREAKING CHANGE:` | Major (1.0.0 → 2.0.0) | `feat!: breaking change` |
| `chore:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:` | Patch | `chore: update deps` |

## 🔧 Configuration

### Required Secrets
- `GITHUB_TOKEN` (automatically provided)
- `NPM_TOKEN` (if publishing to npm)

### Environment Setup
- Create `production` environment in GitHub for manual approval
- Configure reviewers for production builds

## 📁 Files Modified

- **`package.json`** - Version automatically updated
- **`CHANGELOG.md`** - Persistent changelog maintained
- **Git tags** - New version tags created
- **GitHub Releases** - Releases with changelog created

## 🚀 Benefits

✅ **Zero developer overhead** - just write conventional commits  
✅ **Automatic versioning** - no manual version management  
✅ **Professional changelogs** - high-quality changelog generation  
✅ **PR validation** - ensures commit format compliance  
✅ **Build automation** - development and production builds  
✅ **Manual approval** - production builds require approval  

## 🔍 Troubleshooting

### Release workflow doesn't run
- Check if commit message contains `[skip ci]`
- Ensure you're pushing to `main` branch
- Check Actions tab for any errors

### Version not bumping
- Verify commit messages follow conventional format
- Check if commits are actually new since last tag
- Look at workflow logs for semver calculation details

### PR validation failing
- Update commit messages to follow conventional format
- Use interactive rebase to fix commit messages
- Force push after changes

## 📚 Learn More

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Changesets](https://github.com/changesets/changesets)
- [Semantic Versioning](https://semver.org/)
