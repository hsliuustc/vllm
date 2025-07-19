# Team Collaboration Guide for vLLM Development

This document outlines the guidelines and best practices for team collaboration when contributing to the vLLM project. This guide is specifically designed for teams where one member will be the final PR submitter to the main vLLM repository.

## Table of Contents

- [DCO Compliance](#dco-compliance)
- [Commit Message Standards](#commit-message-standards)
- [Branch Management Strategy](#branch-management-strategy)
- [Code Quality & Testing](#code-quality--testing)
- [PR Process Coordination](#pr-process-coordination)
- [Code Review Checklist](#code-review-checklist)
- [Technical Considerations](#technical-considerations)
- [Communication & Coordination](#communication--coordination)
- [Common Pitfalls to Avoid](#common-pitfalls-to-avoid)
- [Resources](#resources)

## 🔐 DCO (Developer Certificate of Origin) Compliance

### For All Team Members

- **Every commit must be signed**: Use `git commit -s` for all commits
- **Correct author information**: Each person should commit with their own email/name
- **No shared accounts**: Each team member should use their own GitHub account
- **Verify signing**: Always check that your commits include the Signed-off-by line

### For Final PR Submitter

- **Verify all commits are signed**: Check before submitting the final PR
- **Fix any unsigned commits**: Use `git commit --amend -s` if needed
- **Maintain commit history**: Don't squash commits from different authors
- **Check DCO status**: Ensure all commits pass DCO checks

### Example of Properly Signed Commit

```bash
git commit -s -m "[Feature] Add new attention mechanism" -m "This commit adds support for a new attention mechanism that improves performance for long sequences."
```

Result:
```
[Feature] Add new attention mechanism

This commit adds support for a new attention mechanism that improves performance for long sequences.

Signed-off-by: Your Name <your.email@example.com>
```

## 📋 Commit Message Standards

### Format

```
[Category] Brief description (#issue_number)

Detailed description if needed

Signed-off-by: Author Name <email@example.com>
```

### Categories to Use

- `[Feature]` - New features
- `[Bugfix]` - Bug fixes  
- `[Core]` - Core engine changes
- `[Model]` - Model-specific changes
- `[Kernel]` - CUDA kernel changes
- `[Doc]` - Documentation
- `[Misc]` - Miscellaneous changes
- `[CI]` - CI/CD changes
- `[Test]` - Test changes
- `[Perf]` - Performance improvements
- `[Refactor]` - Code refactoring

### Examples

```bash
# Good commit message
git commit -s -m "[Feature] Add support for unquantized models" -m "This commit adds support for unquantized models in the EPLB framework."

# Good commit message with issue reference
git commit -s -m "[Bugfix] Fix memory leak in attention kernel (#1234)" -m "Resolves memory leak issue in the attention kernel implementation."

# Good commit message for multiple authors
git commit -s -m "[Core] Implement new caching mechanism" -m "Co-authored-by: Team Member <member@example.com>"
```

## 🔄 Branch Management Strategy

### Recommended Workflow

1. **Main branch**: Keep your fork's main in sync with upstream
2. **Feature branches**: Create separate branches for each feature
3. **Team branches**: Each team member works on their own feature branch
4. **Integration branch**: Merge all team changes into one branch before final PR

### Branch Naming Convention

```
feature/descriptive-name
bugfix/issue-description
team/feature-name
epic/major-feature
```

### Branch Management Commands

```bash
# Keep main branch updated
git checkout main
git pull upstream main
git push origin main

# Create feature branch
git checkout -b feature/new-attention-mechanism

# Create team integration branch
git checkout -b team/eplb-integration

# Update feature branch with latest main
git checkout feature/new-attention-mechanism
git rebase main
```

## 🧪 Code Quality & Testing

### Before Submitting PRs to Your Fork

- **Run tests**: `python -m pytest tests/`
- **Code formatting**: Use `black`, `isort`, `flake8`
- **Type checking**: Run `mypy` if applicable
- **Linting**: Check for any linting errors
- **Unit tests**: Ensure all unit tests pass
- **Integration tests**: Run integration tests if applicable

### For Final PR to vLLM

- **All tests pass**: Ensure comprehensive test coverage
- **No linting errors**: Clean code quality
- **Documentation updated**: Update relevant docs
- **Backward compatibility**: Ensure changes don't break existing APIs
- **Performance impact**: Consider and document performance implications

### Testing Commands

```bash
# Run all tests
python -m pytest tests/

# Run specific test file
python -m pytest tests/test_attention.py

# Run with coverage
python -m pytest tests/ --cov=vllm

# Format code
black vllm/
isort vllm/

# Lint code
flake8 vllm/
mypy vllm/
```

## 📝 PR Process Coordination

### Team PRs to Your Fork

- **Clear descriptions**: Each PR should have detailed descriptions
- **Reference issues**: Link to relevant GitHub issues
- **Review process**: Review each team member's PR thoroughly
- **CI checks**: Ensure all CI checks pass
- **Test coverage**: Ensure adequate test coverage

### Final PR to vLLM

- **Comprehensive description**: Include all changes and rationale
- **Test results**: Mention test coverage and results
- **Breaking changes**: Clearly document any breaking changes
- **Migration guide**: If needed, provide migration instructions
- **Performance benchmarks**: Include performance impact data

### PR Template

```markdown
## Description
Brief description of the changes

## Related Issues
Closes #1234
Related to #5678

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed

## Checklist
- [ ] Code follows style guidelines
- [ ] All commits are signed
- [ ] Documentation is updated
- [ ] No breaking changes (or documented)
```

## 🔍 Code Review Checklist

### For Team PRs

- [ ] Code follows vLLM style guidelines
- [ ] All commits are properly signed
- [ ] Tests are included and pass
- [ ] Documentation is updated
- [ ] No hardcoded values or secrets
- [ ] Error handling is appropriate
- [ ] Performance impact is considered
- [ ] Code is readable and well-commented
- [ ] No unnecessary dependencies added

### For Final PR

- [ ] All team changes are properly integrated
- [ ] No merge conflicts
- [ ] Commit history is clean and logical
- [ ] All DCO requirements met
- [ ] Follows vLLM contribution guidelines
- [ ] All CI checks pass
- [ ] Performance benchmarks included if applicable

## 🛠 Technical Considerations

### Git Configuration

```bash
# Each team member should set their identity
git config user.name "Your Name"
git config user.email "your.email@example.com"

# For signing commits
git config commit.gpgsign true  # If using GPG

# Set up aliases for common operations
git config alias.co checkout
git config alias.br branch
git config alias.ci commit
git config alias.st status
```

### Branch Protection

Set up branch protection rules on your fork:
- Require reviews before merging
- Require status checks to pass
- Require up-to-date branches before merging
- Restrict force pushes

### Pre-commit Hooks

Set up pre-commit hooks for code quality:

```bash
# Install pre-commit
pip install pre-commit

# Set up pre-commit hooks
pre-commit install

# Run pre-commit on all files
pre-commit run --all-files
```

## 📞 Communication & Coordination

### Team Communication

- **Regular sync-ups**: Coordinate on changes to avoid conflicts
- **Shared documentation**: Use shared docs for design decisions
- **Issue tracking**: Use GitHub issues for task management
- **Code review rotation**: Have different team members review each other's code
- **Slack/Discord channels**: Use dedicated channels for project communication

### Timeline Management

- **Milestone planning**: Set clear milestones and deadlines
- **Dependency management**: Coordinate on dependent changes
- **Integration testing**: Plan for integration testing phase
- **Release planning**: Coordinate release schedules

### Meeting Structure

- **Daily standups**: Quick status updates
- **Weekly reviews**: Code review and planning sessions
- **Sprint planning**: Plan upcoming work
- **Retrospectives**: Reflect on process improvements

## 🚨 Common Pitfalls to Avoid

1. **Squashing team commits**: Don't squash commits from different authors
2. **Missing DCO**: Always check for signed-off-by lines
3. **Incomplete testing**: Don't skip tests to save time
4. **Poor commit messages**: Use descriptive, standardized messages
5. **Breaking changes without notice**: Always document breaking changes
6. **Ignoring CI failures**: Fix all CI issues before merging
7. **Working on the same files simultaneously**: Coordinate to avoid conflicts
8. **Not communicating changes**: Keep team informed of major changes
9. **Skipping code reviews**: Always review each other's code
10. **Not updating documentation**: Keep docs in sync with code changes

## 📚 Resources

### vLLM Contribution Guidelines

- [CONTRIBUTING.md](https://github.com/vllm-project/vllm/blob/main/CONTRIBUTING.md)
- [Code of Conduct](https://github.com/vllm-project/vllm/blob/main/CODE_OF_CONDUCT.md)
- [Development Setup](https://docs.vllm.ai/en/latest/development/setup.html)
- [API Documentation](https://docs.vllm.ai/)

### Tools to Use

- **Pre-commit hooks**: Set up pre-commit hooks for code quality
- **GitHub Actions**: Use CI/CD for automated testing
- **Code review tools**: Use GitHub's review features effectively
- **Project management**: Use GitHub Projects or external tools like Jira

### Useful Commands

```bash
# Check commit signing status
git log --pretty=format:"%h %s%n%b%n---" -10 | grep -A 10 -B 2 "Signed-off-by"

# Check for unsigned commits
git log --pretty=format:"%h %s" --no-merges | while read commit; do
    if ! git show --pretty=format:"%B" $commit | grep -q "Signed-off-by"; then
        echo "Missing DCO: $commit"
    fi
done

# Update branch with latest main
git checkout main && git pull upstream main && git checkout your-branch && git rebase main

# Check test coverage
python -m pytest tests/ --cov=vllm --cov-report=html
```

## 🤝 Team Roles and Responsibilities

### Final PR Submitter
- Coordinate with all team members
- Ensure all DCO requirements are met
- Review and integrate all team changes
- Submit final PR to vLLM repository
- Respond to maintainer feedback

### Team Members
- Follow all coding standards
- Write comprehensive tests
- Document their changes
- Respond to review feedback
- Coordinate with other team members

### Code Reviewers
- Review code thoroughly
- Provide constructive feedback
- Check for security issues
- Ensure code quality standards
- Verify test coverage

---

**Remember**: The goal is to produce high-quality, maintainable code that follows vLLM's standards and can be easily integrated into the main repository. Good communication and coordination are key to successful team collaboration! 