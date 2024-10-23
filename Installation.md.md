# AgentNeo Installation and Setup Guide 
## Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Installation Methods](#installation-methods)
- [Windows Installation](#1-windows-installation)
- [macOS Installation](#2-macos-installation)
- [Linux Installation](#3-linux-installation)
- [Additional Information](#additional-information)

## Overview
AgentNeo is a versatile tool for monitoring AI agents, tracing LLMs, and visualizing their interactions. This guide provides comprehensive installation instructions for multiple platforms and package management tools.

## Prerequisites
- Python 3.8.8 or above
- pip/Conda (latest version recommended)

## Installation Methods
This guide covers the following installation methods:
- pip with virtualenv (all platforms)
- Conda (all platforms)
- Pipenv (all platforms)

## Version Information
- For latest version: `pip install --U`
- For specific version: `pip install agentneo==1.1.2`

## 1. Windows Installation
### 1.1. Using pip and Virtualenv
Create a virtual environment:
```bash
python -m venv agentneo-env
```
Activate the environment:
```bash
agentneo-env\Scripts\activate
```
Install AgentNeo:
```bash
pip install agentneo
```

### 1.2. Using Conda
Create and activate a conda environment:
```bash
conda create --name agentneo-env
conda activate agentneo-env
```
Install AgentNeo:
```bash
pip install agentneo
```

### 1.3. Using Pipenv
Install Pipenv:
```bash
pip install pipenv
```
Set up Pipenv environment:
```bash
pipenv install agentneo
pipenv shell
```

## 2. macOS Installation
### 2.1. Using pip and Virtualenv
Create a virtual environment:
```bash
python -m venv agentneo-env
source agentneo-env/bin/activate
```
Install AgentNeo:
```bash
pip install agentneo
```

### 2.2. Using Conda
Create and activate a conda environment:
```bash
conda create --name agentneo-env
conda activate agentneo-env
```
Install AgentNeo:
```bash
pip install agentneo
```

### 2.3. Using Pipenv
Install and set up Pipenv:
```bash
brew install pipenv
pipenv install agentneo
pipenv shell
```

## 3. Linux Installation
### 3.1. Using pip and Virtualenv (Ubuntu/Debian)
Create a virtual environment:
```bash
python -m venv agentneo-env
source agentneo-env/bin/activate
```
Install AgentNeo:
```bash
pip install agentneo
```

### 3.2. Using Conda
**Step 1: Install Miniconda**
Run the installer:
```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

**Step 2: Set Up Conda Environment**
Create and activate an environment:
```bash
conda create --name agentneo-env
conda activate agentneo-env
```

**Step 3: Install AgentNeo**
```bash
pip install agentneo
```

### 3.3. Using Pipenv
Set up Pipenv environment:
```bash
sudo apt install pipenv
pipenv install agentneo
pipenv shell
```

## Additional Information
### Verifying Installation
To verify that AgentNeo is installed correctly, run:
```bash
python -c "import agentneo; print(agentneo.__version__)"
```
