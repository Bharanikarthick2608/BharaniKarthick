# AgentNeo Installation and Setup Guide

## Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Installation Methods](#installation-methods)
  - [Using pip and Virtualenv](#using-pip-and-virtualenv)
  - [Using Conda](#using-conda)
  - [Using Pipenv](#using-pipenv)
- [Version Information](#version-information)
- [Additional Information](#additional-information)

## Overview
AgentNeo is a versatile tool for monitoring AI agents, tracing LLMs, and visualizing their interactions. This guide provides comprehensive installation instructions for multiple platforms and package management tools.

## Prerequisites
- Python 3.8 or above
- pip/Conda/Pipenv (latest version recommended)

## Installation Methods
This guide covers the following installation methods:
- **pip with virtualenv** (all platforms)
- **Conda** (all platforms)
- **Pipenv** (all platforms)

### Using pip and Virtualenv
1. **Create a virtual environment**:
   ```bash
   python -m venv agentneo-env
   ```

2. **Activate the environment**:
   - **Windows**:
     ```bash
     agentneo-env\Scripts\activate
     ```
   - **macOS/Linux**:
     ```bash
     source agentneo-env/bin/activate
     ```

3. **Install AgentNeo**:
   ```bash
   pip install agentneo
   ```

### Using Conda
1. **Create and activate a conda environment**:
   ```bash
   conda create --name agentneo-env
   conda activate agentneo-env
   ```

2. **Install AgentNeo**:
   ```bash
   pip install agentneo
   ```

### Using Pipenv
1. **Install Pipenv**:
   - **Windows/macOS/Linux**:
     ```bash
     pip install pipenv
     ```
   - **macOS (via Homebrew)**:
     ```bash
     brew install pipenv
     ```
   - **Linux (Ubuntu/Debian)**:
     ```bash
     sudo apt install pipenv
     ```

2. **Set up and activate Pipenv environment**:
   ```bash
   pipenv install agentneo
   pipenv shell
   ```

## Version Information
- For the latest version of AgentNeo:
  ```bash
  pip install --upgrade agentneo
  ```
- For a specific version (e.g., 1.1.2):
  ```bash
  pip install agentneo==1.1.2
  ```

## Additional Information
### Verifying Installation
To verify that AgentNeo is installed correctly, run:
```bash
python -c "import agentneo; print(agentneo.__version__)"
```
