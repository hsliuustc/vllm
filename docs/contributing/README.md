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

## Developing

Depending on the kind of development you'd like to do (e.g. Python, CUDA), you can choose to build vLLM with or without compilation.
Check out the [building from source][build-from-source] documentation for details.

For an optimized workflow when iterating on C++/CUDA kernels, see the [Incremental Compilation Workflow](./incremental_build.md) for recommendations.

### Building the docs with MkDocs

#### Introduction to MkDocs

[MkDocs](https://github.com/mkdocs/mkdocs) is a fast, simple and downright gorgeous static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file.

#### Install MkDocs and Plugins

Install MkDocs along with the [plugins](https://github.com/vllm-project/vllm/blob/main/mkdocs.yaml) used in the vLLM documentation, as well as required dependencies:

```bash
pip install -r requirements/docs.txt
```

!!! note
    Ensure that your Python version is compatible with the plugins (e.g., `mkdocs-awesome-nav` requires Python 3.10+)

#### Verify Installation

Confirm that MkDocs is correctly installed:

```bash
mkdocs --version
```

Example output:

```console
mkdocs, version 1.6.1 from /opt/miniconda3/envs/mkdoc/lib/python3.10/site-packages/mkdocs (Python 3.10)
```

#### Clone the `vLLM` repository

```bash
git clone https://github.com/vllm-project/vllm.git
cd vllm
```

#### Start the Development Server

MkDocs comes with a built-in dev-server that lets you preview your documentation as you work on it. Make sure you're in the same directory as the `mkdocs.yml` configuration file, and then start the server by running the `mkdocs serve` command:

```bash
mkdocs serve
```

Example output:

```console
INFO    -  Documentation built in 106.83 seconds
INFO    -  [22:02:02] Watching paths for changes: 'docs', 'mkdocs.yaml'
INFO    -  [22:02:02] Serving on http://127.0.0.1:8000/
```

#### View in Your Browser

Open up [http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your browser to see a live preview:.

#### Learn More

For additional features and advanced configurations, refer to the official [MkDocs Documentation](https://www.mkdocs.org/).

## Testing

??? console "Commands"

    ```bash
    pip install -r requirements/dev.txt

    # Linting, formatting and static type checking
    pre-commit install --hook-type pre-commit --hook-type commit-msg

    # You can manually run pre-commit with
    pre-commit run --all-files

    # To manually run something from CI that does not run
    # locally by default, you can run:
    pre-commit run mypy-3.9 --hook-stage manual --all-files

    # Unit tests
    pytest tests/

    # Run tests for a single test file with detailed output
    pytest -s -v tests/test_logger.py
    ```

!!! tip
    Since the <gh-file:docker/Dockerfile> ships with Python 3.12, all tests in CI (except `mypy`) are run with Python 3.12.

    Therefore, we recommend developing with Python 3.12 to minimise the chance of your local environment clashing with our CI environment.

!!! note
    Currently, the repository is not fully checked by `mypy`.

!!! note
    Currently, not all unit tests pass when run on CPU platforms. If you don't have access to a GPU
    platform to run unit tests locally, rely on the continuous integration system to run the tests for
    now.

## Issues

If you encounter a bug or have a feature request, please [search existing issues](https://github.com/vllm-project/vllm/issues?q=is%3Aissue) first to see if it has already been reported. If not, please [file a new issue](https://github.com/vllm-project/vllm/issues/new/choose), providing as much relevant information as possible.

!!! important
    If you discover a security vulnerability, please follow the instructions [here](gh-file:SECURITY.md#reporting-a-vulnerability).

## Pull Requests & Code Reviews

Thank you for your contribution to vLLM! Before submitting the pull request,
please ensure the PR meets the following criteria. This helps vLLM maintain the
code quality and improve the efficiency of the review process.

### DCO and Signed-off-by

When contributing changes to this project, you must agree to the <gh-file:DCO>.
Commits must include a `Signed-off-by:` header which certifies agreement with
the terms of the DCO.

Using `-s` with `git commit` will automatically add this header.

!!! tip
    You can enable automatic sign-off via your IDE:
  
    - **PyCharm**: Click on the `Show Commit Options` icon to the right of the `Commit and Push...` button in the `Commit` window.
      It will bring up a `git` window where you can modify the `Author` and enable `Sign-off commit`.
    - **VSCode**: Open the [Settings editor](https://code.visualstudio.com/docs/configure/settings)
      and enable the `Git: Always Sign Off` (`git.alwaysSignOff`) field.

### PR Title and Classification

Only specific types of PRs will be reviewed. The PR title is prefixed
appropriately to indicate the type of change. Please use one of the following:

- `[Bugfix]` for bug fixes.
- `[CI/Build]` for build or continuous integration improvements.
- `[Doc]` for documentation fixes and improvements.
- `[Model]` for adding a new model or improving an existing model. Model name
  should appear in the title.
- `[Frontend]` For changes on the vLLM frontend (e.g., OpenAI API server,
  `LLM` class, etc.)
- `[Kernel]` for changes affecting CUDA kernels or other compute kernels.
- `[Core]` for changes in the core vLLM logic (e.g., `LLMEngine`,
  `AsyncLLMEngine`, `Scheduler`, etc.)
- `[Hardware][Vendor]` for hardware-specific changes. Vendor name should
  appear in the prefix (e.g., `[Hardware][AMD]`).
- `[Misc]` for PRs that do not fit the above categories. Please use this
  sparingly.

!!! note
    If the PR spans more than one category, please include all relevant prefixes.

### Code Quality

The PR needs to meet the following code quality standards:

- We adhere to [Google Python style guide](https://google.github.io/styleguide/pyguide.html) and [Google C++ style guide](https://google.github.io/styleguide/cppguide.html).
- Pass all linter checks. Please use `pre-commit` to format your code. See
  <https://pre-commit.com/#usage> if `pre-commit` is new to you.
- The code needs to be well-documented to ensure future contributors can easily
  understand the code.
- Include sufficient tests to ensure the project stays correct and robust. This
  includes both unit tests and integration tests.
- Please add documentation to `docs/` if the PR modifies the user-facing behaviors of vLLM.
  It helps vLLM users understand and utilize the new features or changes.

### Pre-commit Hooks and Code Quality Automation

vLLM uses [pre-commit](https://pre-commit.com/) to automate code quality checks and formatting before code is committed. This helps ensure consistency and code health across all contributions.

#### What is pre-commit?
- **pre-commit** is a framework for managing and maintaining multi-language code quality hooks that run automatically every time you make a commit in git.
- It runs a set of checks (called "hooks") on your code before the commit is finalized. These hooks can automatically fix issues (like formatting), or block the commit if there are problems (like lint errors, unsorted imports, or missing sign-offs).

#### Common hooks in vLLM include:
- **isort**: Automatically sorts Python imports.
- **yapf**/**black**: Formats Python code.
- **ruff**/**flake8**: Lints Python code for errors and style issues.
- **typos**: Checks for spelling mistakes.
- **mypy**: Checks type annotations.
- **custom hooks**: vLLM may add project-specific checks (e.g., for license headers, filenames, etc.).

#### How does it work?
1. The `.pre-commit-config.yaml` file in the repo lists all the hooks to run.
2. Install pre-commit with `pip install pre-commit` and set it up with `pre-commit install`.
3. Every time you run `git commit`, pre-commit runs the hooks on your staged files.
4. If a hook fails (e.g., isort changes your file), the commit is blocked until you fix the issues and try again.

#### Why is it useful?
- **Consistency**: Everyone’s code is formatted and checked the same way.
- **Automation**: Catches issues before they get into the codebase.
- **Saves time**: Reduces code review comments about style and simple mistakes.

#### Example output:
```
isort...............................................................................................Failed
- hook id: isort
- files were modified by this hook
Fixing vllm/model_executor/models/qwen3_moe.py
```
This means isort fixed your imports, and you need to add and commit the changes.

#### How to resolve pre-commit issues (e.g., isort):
1. **Re-run pre-commit locally** (or just run isort) to apply the changes:
   ```bash
   pre-commit run isort --all-files
   # or
   isort vllm/model_executor/models/qwen3_moe.py
   ```
2. **Stage the changes**:
   ```bash
   git add vllm/model_executor/models/qwen3_moe.py
   ```
3. **Amend your commit or create a new commit**:
   ```bash
   git commit --amend --no-edit  # if you want to keep the same commit message
   # or
   git commit -m "Fix import order with isort"
   ```
4. **Push the changes** (force push if you amended):
   ```bash
   git push --force-with-lease
   ```

#### Summary
- pre-commit is a tool that helps keep your code clean and consistent by running checks automatically before every commit.
- If a hook (like isort) fails, let it fix your code, then add and commit the changes.
- For more details, see the [pre-commit documentation](https://pre-commit.com/).

### Pre-commit Usage Guide

To ensure code quality and consistency, vLLM uses pre-commit hooks. Here’s how to set up and use pre-commit in your development workflow:

#### 1. Install pre-commit
```bash
pip install pre-commit
```

#### 2. Install the pre-commit hooks for this repository
This sets up the hooks to run automatically on every commit:
```bash
pre-commit install
```

#### 3. (Optional) Install commit-msg hooks for DCO sign-off
```bash
pre-commit install --hook-type commit-msg
```

#### 4. Run all hooks on all files (recommended before pushing a PR)
```bash
pre-commit run --all-files
```

#### 5. What happens if a hook fails?
- If a hook (like isort or yapf) fails, it may automatically fix your files. You’ll see output like:
  ```
  isort....................................................................Failed
  - hook id: isort
  - files were modified by this hook
  Fixing vllm/model_executor/models/qwen3_moe.py
  ```
- **You must add and commit the changes again:**
  ```bash
  git add <modified-files>
  git commit --amend --no-edit  # or create a new commit
  ```
- Then re-run pre-commit if needed, and push your changes.

#### 6. Bypassing pre-commit (not recommended)
If you need to bypass pre-commit for a specific commit (e.g., in emergencies):
```bash
git commit --no-verify
```

#### 7. Troubleshooting
- If you see errors about missing tools, run `pip install -r requirements/lint.txt` to install all linting dependencies.
- If you see repeated failures, carefully read the output—often, the tool will tell you what to fix or will fix it for you.
- For more help, see the [pre-commit documentation](https://pre-commit.com/).

**Summary:**
- Always run pre-commit before pushing a PR.
- Let pre-commit fix your code, then add and commit the changes.
- This keeps the codebase clean and saves time for everyone!

### Adding or Changing Kernels

When actively developing or modifying kernels, using the [Incremental Compilation Workflow](./incremental_build.md) is highly recommended for faster build times.
Each custom kernel needs a schema and one or more implementations to be registered with PyTorch.

- Make sure custom ops are registered following PyTorch guidelines:
  [Custom C++ and CUDA Operators](https://pytorch.org/tutorials/advanced/cpp_custom_ops.html#cpp-custom-ops-tutorial)
  and [The Custom Operators Manual](https://docs.google.com/document/d/1_W62p8WJOQQUzPsJYa7s701JXt0qf2OfLub2sbkHOaU).
- Custom operations that return `Tensors` require meta-functions.
  Meta-functions should be implemented and registered in Python so that dynamic
  dims can be handled automatically. See above documents for a description of
  meta-functions.
- Use [torch.library.opcheck()](https://pytorch.org/docs/stable/library.html#torch.library.opcheck)
  to test the function registration and meta-function for any registered ops.
  See `tests/kernels` for examples.
- When changing the C++ signature of an existing op, the schema must be updated
  to reflect the changes.
- If a new custom type is needed, see the following document:
  [Custom Class Support in PT2](https://docs.google.com/document/d/18fBMPuOJ0fY5ZQ6YyrHUppw9FA332CpNtgB6SOIgyuA).

### Notes for Large Changes

Please keep the changes as concise as possible. For major architectural changes
(>500 LOC excluding kernel/data/config/test), we would expect a GitHub issue
(RFC) discussing the technical design and justification. Otherwise, we will tag
it with `rfc-required` and might not go through the PR.

### What to Expect for the Reviews

The goal of the vLLM team is to be a *transparent reviewing machine*. We would
like to make the review process transparent and efficient and make sure no
contributor feels confused or frustrated. However, the vLLM team is small, so we
need to prioritize some PRs over others. Here is what you can expect from the
review process:

- After the PR is submitted, the PR will be assigned to a reviewer. Every
  reviewer will pick up the PRs based on their expertise and availability.
- After the PR is assigned, the reviewer will provide status updates every 2-3
  days. If the PR is not reviewed within 7 days, please feel free to ping the
  reviewer or the vLLM team.
- After the review, the reviewer will put an `action-required` label on the PR
  if there are changes required. The contributor should address the comments and
  ping the reviewer to re-review the PR.
- Please respond to all comments within a reasonable time frame. If a comment
  isn't clear or you disagree with a suggestion, feel free to ask for
  clarification or discuss the suggestion.
- Note that not all CI checks will be executed due to limited computational
  resources. The reviewer will add `ready` label to the PR when the PR is
  ready to merge or a full CI run is needed.

## Thank You

Finally, thank you for taking the time to read these guidelines and for your interest in contributing to vLLM.
All of your contributions help make vLLM a great tool and community for everyone!

## Team Collaboration & Advanced Workflow

This section provides advanced guidelines and best practices for teams collaborating on vLLM development, especially when multiple contributors are working together and one member will be the final PR submitter to the main vLLM repository.

### Commit Message Standards (Advanced)

- Use descriptive, standardized commit messages for clarity and traceability.
- Format:
  ```
  [Category] Brief description (#issue_number)

  Detailed description if needed

  Signed-off-by: Author Name <email@example.com>
  ```
- Categories: `[Feature]`, `[Bugfix]`, `[Core]`, `[Model]`, `[Kernel]`, `[Doc]`, `[Misc]`, `[CI]`, `[Test]`, `[Perf]`, `[Refactor]`
- Example:
  ```bash
  git commit -s -m "[Feature] Add support for unquantized models" -m "This commit adds support for unquantized models in the EPLB framework."
  ```

### Branch Management Strategy

- Keep your fork's main branch in sync with upstream.
- Use feature branches for each new feature or fix.
- For teams, use an integration branch to combine all changes before the final PR.
- Branch naming: `feature/descriptive-name`, `bugfix/issue-description`, `team/feature-name`, `epic/major-feature`
- Example workflow:
  ```bash
  git checkout main
  git pull upstream main
  git push origin main
  git checkout -b feature/new-attention-mechanism
  git checkout -b team/eplb-integration
  git checkout feature/new-attention-mechanism
  git rebase main
  ```

### Code Quality & Testing (Team Focus)

- Run all tests: `python -m pytest tests/`
- Format code: `black vllm/`, `isort vllm/`
- Lint: `flake8 vllm/`, `mypy vllm/`
- Ensure all unit and integration tests pass before PR.
- Document performance impact and update docs as needed.

### PR Process Coordination

- Use clear, detailed PR descriptions and reference issues.
- Review all team PRs thoroughly before merging.
- For the final PR to vLLM:
  - Include comprehensive description, test results, breaking changes, migration guide, and performance benchmarks.
- Example PR template:
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

### Code Review Checklist (Team)

- [ ] Code follows vLLM style guidelines
- [ ] All commits are properly signed
- [ ] Tests are included and pass
- [ ] Documentation is updated
- [ ] No hardcoded values or secrets
- [ ] Error handling is appropriate
- [ ] Performance impact is considered
- [ ] Code is readable and well-commented
- [ ] No unnecessary dependencies added
- [ ] All team changes are properly integrated
- [ ] No merge conflicts
- [ ] Commit history is clean and logical
- [ ] All DCO requirements met
- [ ] Follows vLLM contribution guidelines
- [ ] All CI checks pass
- [ ] Performance benchmarks included if applicable

### Technical Considerations

- Each team member should set their git identity:
  ```bash
  git config user.name "Your Name"
  git config user.email "your.email@example.com"
  git config commit.gpgsign true  # If using GPG
  ```
- Set up branch protection rules on your fork (require reviews, status checks, up-to-date branches, restrict force pushes).
- Use pre-commit hooks for code quality (see earlier section for details).

### Communication & Coordination

- Hold regular sync-ups and use shared documentation for design decisions.
- Use GitHub issues for task management and code review rotation.
- Plan milestones, integration testing, and releases as a team.
- Use daily standups, weekly reviews, sprint planning, and retrospectives for effective teamwork.

### Common Pitfalls to Avoid

1. Squashing team commits (don't squash commits from different authors)
2. Missing DCO (always check for signed-off-by lines)
3. Incomplete testing
4. Poor commit messages
5. Breaking changes without notice
6. Ignoring CI failures
7. Working on the same files simultaneously
8. Not communicating changes
9. Skipping code reviews
10. Not updating documentation

### Resources & Useful Commands

- [CONTRIBUTING.md](https://github.com/vllm-project/vllm/blob/main/CONTRIBUTING.md)
- [Code of Conduct](https://github.com/vllm-project/vllm/blob/main/CODE_OF_CONDUCT.md)
- [Development Setup](https://docs.vllm.ai/en/latest/development/setup.html)
- [API Documentation](https://docs.vllm.ai/)

#### Useful Git Commands
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

### Team Roles and Responsibilities

- **Final PR Submitter**: Coordinates with all team members, ensures DCO, reviews and integrates changes, submits final PR, responds to maintainer feedback.
- **Team Members**: Follow coding standards, write tests, document changes, respond to review feedback, coordinate with others.
- **Code Reviewers**: Review code, provide feedback, check for security issues, ensure code quality, verify test coverage.

---

This document merges the previous team_collaboration.md into the main contributing guide.
