name: CI/CD Pipeline

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    # Checkout repository
    - name: Checkout Code
      uses: actions/checkout@v3

    # Set up Python environment
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.9' # Specify your Python version

    # Install dependencies
    - name: Install Dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    # Run tests
    - name: Run Tests
      run: python -m unittest discover

  deploy:
    runs-on: ubuntu-latest
    needs: build

    steps:
    # Checkout repository
    - name: Checkout Code
      uses: actions/checkout@v3

    # Deploy application (example deployment script)
    - name: Deploy to Server
      run: |
        echo "Deploying application..."
        # Replace with actual deployment commands
        ssh user@server 'bash deploy-script.sh'
