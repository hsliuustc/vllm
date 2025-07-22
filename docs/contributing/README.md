# Contributing to vLLM

Thank you for your interest in contributing to vLLM! Our community is open to everyone and welcomes all kinds of contributions, no matter how small or large. There are several ways you can contribute to the project:

- Identify and report any issues or bugs.
- Request or add support for a new model.
- Suggest or implement new features.
- Improve documentation or contribute a how-to guide.

We also believe in the power of community support; thus, answering queries, offering PR reviews, and assisting others are also highly regarded and beneficial contributions.

Finally, one of the most impactful ways to support us is by raising awareness about vLLM. Talk about it in your blog posts and highlight how it's driving your incredible projects. Express your support on social media if you're using vLLM, or simply offer your appreciation by starring our repository!

## Job Board

Unsure on where to start? Check out the following links for tasks to work on:

- [Good first issues](https://github.com/vllm-project/vllm/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22good%20first%20issue%22)
    - [Selected onboarding tasks](gh-project:6)
- [New model requests](https://github.com/vllm-project/vllm/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22new-model%22)
    - [Models with multi-modal capabilities](gh-project:10)

## License

See <gh-file:LICENSE>.

## Essential Requirements for Contributing

Before submitting any contribution, you must follow these two critical requirements:

### 1. DCO (Developer Certificate of Origin) Compliance

**Every commit must be signed** to certify agreement with the [Developer Certificate of Origin](gh-file:DCO).

#### How to Sign Your Commits

**Option A: Automatic sign-off (Recommended)**
```bash
git commit -s -m "Your commit message"
```

**Option B: Manual sign-off**
```bash
git commit -m "Your commit message" -m "Signed-off-by: Your Name <your.email@example.com>"
```

#### IDE Integration

- **PyCharm**: Click `Show Commit Options` → Enable `Sign-off commit`
- **VSCode**: Enable `Git: Always Sign Off` in settings (`git.alwaysSignOff`)

#### Verify Your Sign-off
```bash
git log --pretty=format:"%h %s%n%b" -1
```

You should see:
```
[commit-hash] Your commit message

Signed-off-by: Your Name <your.email@example.com>
```

### 2. Pre-commit Setup and Usage

vLLM uses [pre-commit](https://pre-commit.com/) to ensure code quality and consistency.

#### Quick Setup

```bash
# Install pre-commit
pip install pre-commit

# Install hooks for this repository
pre-commit install

# Optional: Install commit-msg hooks for automatic DCO sign-off
pre-commit install --hook-type commit-msg
```

#### Run Pre-commit

```bash
# Run on all files (recommended before pushing)
pre-commit run --all-files

# Run on staged files only
pre-commit run
```

#### What Happens When Pre-commit Fails?

Pre-commit hooks may automatically fix your code. You'll see output like:
```
isort....................................................................Failed
- hook id: isort
- files were modified by this hook
Fixing vllm/your_file.py
```

**To resolve:**
```bash
# 1. Add the fixed files
git add <modified-files>

# 2. Amend your commit
git commit --amend --no-edit

# 3. Push (force push if you amended)
git push --force-with-lease
```

#### Common Pre-commit Hooks in vLLM

- **isort**: Sorts Python imports
- **yapf**: Formats Python code
- **ruff**: Lints Python code
- **typos**: Checks spelling
- **mypy**: Type checking
- **signoff-commit**: Ensures DCO compliance

## Pull Request Guidelines

### PR Title Format
Use one of these prefixes:
- `[Bugfix]` - Bug fixes
- `[Feature]` - New features
- `[Doc]` - Documentation
- `[Model]` - Model-related changes
- `[Core]` - Core engine changes
- `[Kernel]` - CUDA kernel changes
- `[Misc]` - Other changes

### Before Submitting
- [ ] All commits are signed (DCO compliant)
- [ ] Pre-commit passes: `pre-commit run --all-files`
- [ ] Tests pass: `pytest tests/`
- [ ] Code follows style guidelines
- [ ] Documentation is updated (if applicable)

## Quick Troubleshooting

**"pre-commit command not found"**
```bash
pip install pre-commit
```

**"Missing DCO" error**
```bash
git commit --amend -s
git push --force-with-lease
```

**Pre-commit keeps failing**
- Read the error output carefully
- Let pre-commit fix your code, then add and commit the changes
- Run `pre-commit run --all-files` to check everything

## Additional Resources

- [Full Development Setup](https://docs.vllm.ai/en/latest/development/setup.html)
- [Building from Source](./building_from_source.md)
- [Incremental Compilation Workflow](./incremental_build.md)
- [Pre-commit Documentation](https://pre-commit.com/)

## Thank You

Thank you for taking the time to read these guidelines and for your interest in contributing to vLLM. All of your contributions help make vLLM a great tool and community for everyone!
