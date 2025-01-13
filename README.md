# pep8-and-coverage

This repository is a Python project configured to enforce **PEP8 compliance**, **automatic code formatting**, and **code coverage** using various tools. It integrates:

- **flake8**: For Python code linting and PEP8 style checks.
- **black**: For automatic code formatting.
- **pytest**: For running unit tests.
- **coverage**: To measure code coverage and ensure it meets a minimum threshold.

## Table of Contents

1. [Project Setup](#project-setup)
2. [Configuration Files](#configuration-files)
   - [`.flake8`](#flake8-configuration)
   - [`.pre-commit-config.yaml`](#pre-commit-configyaml-configuration)
3. [Usage](#usage)
   - [Install Dependencies](#install-dependencies)
   - [Install Pre-commit Hooks](#install-pre-commit-hooks)
   - [Run Pre-commit Hooks](#run-pre-commit-hooks)
4. [Contributing](#contributing)
5. [License](#license)

---

## Project Setup

This project is configured with pre-commit hooks to ensure that only high-quality, well-tested code is committed to the repository. It integrates `flake8` for linting, `black` for formatting, and `pytest` for testing. Additionally, `coverage` ensures that your code has adequate test coverage.

To get started with this project, follow the instructions below.

---

## Configuration Files

### `.flake8` Configuration

The `.flake8` file is used to configure `flake8`, a Python linting tool that checks the code against PEP8 standards and other checks.

#### Explanation of Configuration Options for `.flake8`:

- **max-line-length**: Specifies the maximum line length for code (88 characters, which is the PEP8 recommended maximum). This helps maintain readability by keeping lines short.
  
- **ignore**: A comma-separated list of warnings that should be ignored. For example:
  - `E203`: Whitespace before a colon (PEP8 recommends not ignoring this, but some projects prefer ignoring it).
  - `W503`: Line break before binary operator (PEP8 recommends `W503` to be fixed, but this rule was later updated, and some prefer ignoring it).

- **select**: Specifies which types of checks `flake8` will perform. Commonly used check types:
  - `B`: Pyflakes (checks for errors and unused imports)
  - `C`: McCabe complexity
  - `E`: PEP8 errors
  - `F`: Flake8-specific checks
  - `W`: PEP8 warnings

- **plugins**: Additional `flake8` plugins to enhance functionality:
  - `flake8-unused-imports`: Warns about unused imports.
  - `flake8-docstrings`: Checks for docstring style compliance.

### `.pre-commit-config.yaml` Configuration

The .pre-commit-config.yaml file defines hooks that will be executed before each commit, ensuring code quality and consistency. It includes the following hooks:

#### Explanation of Configuration Options for `.pre-commit-config.yaml`:

- **repos**: Defines the repositories where the pre-commit hooks are stored. Each repository can contain one or more hooks.
  - **repo**: The URL of the repository where the hook resides.
  - **rev**: The specific revision (tag or commit hash) of the repository to use. This ensures you are using a stable version of the hook.
  - **hooks**: A list of hooks from the repository that should be enabled in the project.
    - **id**: The unique identifier for the hook. For example, `flake8` or `black`.
    - **args**: Additional command-line arguments to pass to the hook. For example, `--max-line-length=88` for `flake8` to configure the line length.
    - **language_version**: The version of the programming language to use for the hook (e.g., `python3`).
    - **name**: The custom name for a local hook (in case you define your own hook that isn't part of a repository).
    - **entry**: The command to run for the hook, like `pytest --maxfail=1 --disable-warnings -q` for running tests.

#### Example Breakdown:

1. **Flake8**:
   - Repository: `https://github.com/pycqa/flake8`
   - Revision: `7.1.1`
   - Hook ID: `flake8`
   - Arguments: 
     - `--max-line-length=88`: Set the maximum line length to 88 characters (PEP8 recommended).
     - `--ignore=E203,W503`: Ignore specific warnings, such as whitespace before colon (`E203`) and line breaks before binary operators (`W503`).

2. **Black**:
   - Repository: `https://github.com/psf/black`
   - Revision: `24.8.0`
   - Hook ID: `black`
   - Arguments:
     - `--line-length=88`: Set the maximum line length to 88 characters.
   - Language Version: `python3`.

3. **Pytest** (Local Hook):
   - Name: `Run Pytest`
   - Command: `pytest --maxfail=1 --disable-warnings -q`: Run tests with a limit of one failure, suppress warnings, and produce concise output.
   
4. **Coverage Check**:
   - Repository: `https://github.com/pre-commit/mirrors-flake8`
   - Revision: `v5.0.0`
   - Hook ID: `coverage`
   - Command: `coverage run -m pytest && coverage report --fail-under=90`: Run tests and check code coverage, ensuring it's at least 90%.

#### Summary of Common Configurations:
- `repos`: Defines where the hooks are coming from.
- `rev`: Ensures you are using a specific, stable version of the hook.
- `args`: Allows you to configure the hook's behavior (e.g., max line length, which errors to ignore).
- `language_version`: Specifies the version of the language to run the hook with.
- `entry`: Defines the command for running a local hook, like tests or coverage checks.

This configuration ensures that your project adheres to style guidelines and runs tests and coverage checks automatically during the commit process.
