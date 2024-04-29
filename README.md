# LAB-FAT-ADDA
Implement a CI/CD pipeline with the following real-world scenario:
Scenario: You're building a Python web application. Integrate static code analysis.
Task: Use an action like actions/stylelint to run code style checks or linters before building the code.

## Setup Instructions

### Step 1: Enable GitHub Actions

1. Go to your GitHub repository.
2. Navigate to `Settings`.
3. Under `Actions`, ensure that GitHub Actions is enabled.

### Step 2: Create Workflow Directory

Create a directory named `.github/workflows` in the root of your repository to store your workflow files.

### Step 3: Create Workflow File

Create a file named `python-app.yml` in the `.github/workflows` directory. This file defines the CI/CD pipeline.

### Step 4: Define the Workflow

Add the following configuration to `python-app.yml`:

```yaml
name: Python application CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

permissions:
  contents: read

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Set up Python 3.10
      uses: actions/setup-python@v3
      with:
        python-version: "3.10"
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install flake8 pytest
        if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
    - name: Lint with flake8
      run: |
        flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
        flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
    - name: Test with pytest
      run: |
        pytest tests/ -vv  # Correct path to the tests directory and adding verbosity
```

### Step 5: Configure Linting

To ensure code quality and style consistency, configure linting for your Python files using Flake8. You can adjust linting rules by creating a `.flake8` or `setup.cfg` file in your project's root directory.

Example `.flake8` configuration: 
[flake8]
exclude = .git,migrations
max-line-length = 120
max-complexity = 10

### Step 6: Write Tests

Create a `tests/` directory in your project root to store your test files. Include a file named `test_1.py` for your test cases, and make sure to add a `__init__.py` file within the `tests/` directory to make it a Python module.
project_root/
|-- tests/
|-- init.py
|-- test_1.py

### Step 7: Create a flask based application using HTML and Static.yml to host it
check the `main.py` and `index.html` file for the code
```yaml

# Simple workflow for deploying static content to GitHub Pages
name: Deploy static content to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  # Single deploy job since we're just deploying
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Pages
        uses: actions/configure-pages@v5
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          # Upload entire repository
          path: '.'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

after commiting these files we will get the link 
link to the website: https://sashankchittella.github.io/LAB-FAT-ADDA/


