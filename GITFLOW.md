# Gitflow Configuration

This repository follows the Gitflow workflow model.

## Branch Structure

### Main Branches
- **main**: Production-ready code. Only release and hotfix branches should be merged here.
- **develop**: Integration branch for features. This is where the latest development changes are.

### Supporting Branches

#### Feature Branches
- **Naming**: `feature/feature-name`
- **Branch from**: develop
- **Merge into**: develop
- **Purpose**: Develop new features

#### Release Branches
- **Naming**: `release/version-number`
- **Branch from**: develop
- **Merge into**: main and develop
- **Purpose**: Prepare for production release

#### Hotfix Branches
- **Naming**: `hotfix/issue-description`
- **Branch from**: main
- **Merge into**: main and develop
- **Purpose**: Quick fixes for production issues

## Workflow Commands

### Starting a Feature
```bash
git checkout develop
git pull origin develop
git checkout -b feature/your-feature-name
```

### Finishing a Feature
```bash
git checkout develop
git merge --no-ff feature/your-feature-name
git branch -d feature/your-feature-name
git push origin develop
```

### Starting a Release
```bash
git checkout develop
git pull origin develop
git checkout -b release/1.0.0
```

### Finishing a Release
```bash
# Merge to main
git checkout main
git merge --no-ff release/1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"

# Merge back to develop
git checkout develop
git merge --no-ff release/1.0.0
git branch -d release/1.0.0
git push origin main develop --tags
```

### Starting a Hotfix
```bash
git checkout main
git pull origin main
git checkout -b hotfix/critical-bug-fix
```

### Finishing a Hotfix
```bash
# Merge to main
git checkout main
git merge --no-ff hotfix/critical-bug-fix
git tag -a v1.0.1 -m "Hotfix version 1.0.1"

# Merge to develop
git checkout develop
git merge --no-ff hotfix/critical-bug-fix
git branch -d hotfix/critical-bug-fix
git push origin main develop --tags
```

## Branch Protection Rules (Recommended)

Consider setting up branch protection rules for:
- **main**: Require pull request reviews, dismiss stale reviews, require status checks
- **develop**: Require pull request reviews, require up-to-date branches

## Getting Started

1. Clone the repository
2. The `develop` branch is your main development branch
3. Create feature branches from `develop`
4. Submit pull requests to merge features back to `develop`
5. Create release branches when ready to deploy
6. Use hotfix branches for urgent production fixes
