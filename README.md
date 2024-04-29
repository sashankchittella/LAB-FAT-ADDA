# LAB-FAT-ADDA
Implement a CI/CD pipeline with the following real-world scenario:
Scenario: You're building a Python web application. Integrate static code analysis.
Task: Use an action like actions/stylelint to run code style checks or linters before building the code.

**Step 0:** setting up GitHub actions → go to settings→enable GitHub actions
**Step 1:** Create a .github/workflows directory in your repository:
 This directory will contain all your GitHub Actions workflow files

**Step 2: Create a workflow file:**
You can name it python-app.yml. This file will define the steps that your CI/CD pipeline will execute.

**Step 3: Defining a workflow:**
The workflow file should include the following components:
**Trigger:** Define when the workflow should run, such as on push or pull requests to specific branches.
**Jobs:** Define what the workflow does, such as installing dependencies, running linters, testing, building, and deploying.

**Step 4: Add Static Code analysis**
**Linting configuration:** Adjust linting rules in your project by configuring .flake8 or setup.cfg file. This Flake8 is a library where we can check errors, and styling issues in the codebase programs

**Note:** we can Customise it futher using other Linters like pyLint

**Step 5:Testing and Iterations**

--> so in the step 3: work flow should be created in such a way the "/tests/test_1.py" inside the .py write the test codes 
--> now add the path of this tests/ in the yml file so the pyTest will run all the test files in the directory
--> Note: __init__.py is mandatory to create in the tests/ directory
