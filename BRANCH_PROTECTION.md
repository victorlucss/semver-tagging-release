# 🛡️ Branch Protection Setup

To prevent merging PRs that fail validation, you need to set up branch protection rules. This ensures that the PR validation workflow must pass before a PR can be merged.

## 🔧 How to Set Up Branch Protection

### Step 1: Navigate to Repository Settings
1. Go to your GitHub repository
2. Click on **Settings** tab
3. Click on **Branches** in the left sidebar

### Step 2: Add Branch Protection Rule
1. Click **Add rule** button
2. In **Branch name pattern**, enter: `main` (or your main branch name)
3. Check the following options:

#### ✅ **Required Status Checks**
- Check **Require status checks to pass before merging**
- Check **Require branches to be up to date before merging**
- In the search box, type: `PR Validation`
- Select **PR Validation / validate-pr** from the dropdown

#### ✅ **Additional Options (Recommended)**
- Check **Require pull request reviews before merging**
- Check **Dismiss stale PR approvals when new commits are pushed**
- Check **Require review from code owners** (if you have CODEOWNERS file)
- Check **Restrict pushes that create files** (optional)

### Step 3: Save the Rule
1. Click **Create** button
2. The rule is now active

## 🎯 What This Does

### **Before Branch Protection:**
- ❌ PRs can be merged even if validation fails
- ❌ No enforcement of commit standards
- ❌ Manual review required to catch issues

### **After Branch Protection:**
- ✅ **PRs cannot be merged** if validation fails
- ✅ **Automatic enforcement** of conventional commits
- ✅ **Quality gate** prevents bad commits from reaching main
- ✅ **Clear feedback** via PR comments

## 🔍 How It Works

1. **Developer creates PR** → Validation workflow runs
2. **If validation passes** → ✅ Green checkmark, PR can be merged
3. **If validation fails** → ❌ Red X, PR cannot be merged
4. **Developer fixes issues** → Pushes new commits
5. **Validation runs again** → Repeats until all checks pass

## 📋 Example Workflow

```
Developer creates PR with bad commit:
❌ "Add new feature" (invalid format)

↓

Validation fails:
❌ PR Validation / validate-pr (pull_request) Failing

↓

Merge button is disabled:
🚫 "Merging can be performed automatically" (but blocked by failing checks)

↓

Developer fixes commit:
✅ "feat: add new feature" (valid format)

↓

Validation passes:
✅ PR Validation / validate-pr (pull_request) Passing

↓

Merge button is enabled:
✅ "Merging can be performed automatically"
```

## 🚨 Troubleshooting

### **"Require status checks" not showing PR Validation**
- Make sure the workflow has run at least once
- Check that the workflow file is in `.github/workflows/`
- Verify the workflow name matches exactly: `PR Validation`

### **Merge button still enabled despite failing checks**
- Check that branch protection rule is applied to the correct branch
- Verify the status check name matches exactly
- Make sure the rule is saved and active

### **Workflow not running**
- Check that the workflow file is valid YAML
- Verify the workflow triggers on `pull_request` events
- Check the Actions tab for any error messages

## 🎯 Benefits

- 🛡️ **Prevents bad commits** from reaching main branch
- 📚 **Educates developers** on conventional commit format
- 🚀 **Ensures automatic versioning** works correctly
- 🔄 **Maintains code quality** automatically
- 📝 **Clear feedback** via PR comments

## 🔧 Advanced Configuration

### **Require Multiple Reviews**
- Set **Required number of reviewers** to 2 or more
- Ensures multiple people review changes

### **Code Owner Reviews**
- Create a `CODEOWNERS` file in repository root
- Specify who must review changes to specific files
- Example:
  ```
  # Global owners
  * @username1 @username2
  
  # Specific file owners
  /src/ @frontend-team
  /docs/ @docs-team
  ```

### **Restrict Push Access**
- Check **Restrict pushes that create files**
- Prevents direct pushes to main branch
- Forces all changes through PRs

This setup ensures that your repository maintains high code quality and follows conventional commit standards automatically!
