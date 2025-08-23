# github-actions-demo-project
A hands-on repository to learn and experiment with GitHub Actions for automation, CI/CD, and workflow management.



🔧 GitHub Actions Workflow Basics

A workflow YAML file defines:

1. When to run (on)
2. What machine to run on (runs-on)
3. What steps to take (steps, using either run: or uses:)

GitHub Actions Workflow Structure Overview

🔹 jobs:

A job is a collection of steps that run in the same environment (e.g. one runner).
Each job runs in a separate VM/container by default, and they can run in parallel or sequentially (if configured with needs:).	

🔹 steps:

A step is a single task inside a job — like checking out code, running a script, installing dependencies, etc.
All steps in a job run on the same runner, so they can share state (e.g., files, environment).


💡 Example: Multiple Jobs

	jobs:
	  build:
		runs-on: ubuntu-latest
		steps:
		  - name: Build
			run: echo "Building app..."

	  test:
		runs-on: ubuntu-latest
		needs: build  # wait for build to finish
		steps:
		  - name: Run tests
			run: echo "Running tests..."

💡 Example: Multiple Steps in One Job

	jobs:
	  build:
		runs-on: ubuntu-latest
		steps:
		  - name: Checkout
			uses: actions/checkout@v4

		  - name: Build
			run: ./mvnw clean install

		  - name: Test
			run: ./mvnw test


How Workflows Differ (by use case)

1. Simple Hello World Workflow
	For learning and basic automation:
	
name: Hello World

on: [push]

jobs:
  say-hello:
    runs-on: ubuntu-latest
    steps:
      - name: Say hello
        run: echo "Hello, GitHub Actions!"
  	
