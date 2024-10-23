# AgentNeo Installation and Setup Guide (Python 3.9+)

## Contents
- [Overview](#overview)
- [Installation Methods](#installation-methods)
- [Windows Installation](#1-windows-installation)
  - [Using pip and Virtualenv](#11-using-pip-and-virtualenv)
  - [Using Conda](#12-using-conda)
  - [Using Pipenv](#13-using-pipenv)
- [macOS Installation](#2-macos-installation)
  - [Using pip and Virtualenv](#21-using-pip-and-virtualenv)
  - [Using Conda](#22-using-conda)
  - [Using Pipenv](#23-using-pipenv)
- [Linux Installation](#3-linux-installation)
  - [Using pip and Virtualenv](#31-using-pip-and-virtualenv-ubuntudebian)
  - [Using Pipenv](#32-using-pipenv)

## Overview
AgentNeo is a versatile tool for monitoring AI agents, tracing LLMs, and visualizing their interactions. This guide provides comprehensive installation instructions for multiple platforms and package management tools.

## Installation Methods
This guide covers the following installation methods:
- pip with virtualenv (all platforms)
- Conda (Windows and macOS)
- Pipenv (all platforms)

## 1. Windows Installation

### 1.1. Using pip and Virtualenv

**Step 1: Install Python 3.9+**
- Download from [Python.org](https://www.python.org/downloads/)
- Add Python to PATH during installation

**Step 2: Set Up a Virtual Environment and Install AgentNeo**

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

**Step 1: Install Miniconda/Anaconda**
- Download from [Anaconda website](https://www.anaconda.com/download)

**Step 2: Set Up Conda Environment**

Create a conda environment:
```bash
conda create --name agentneo-env python=3.9
```

Activate the environment:
```bash
conda activate agentneo-env
```

Install AgentNeo:
```bash
pip install agentneo
```

### 1.3. Using Pipenv

**Step 1: Install Pipenv**
```bash
pip install pipenv
```

**Step 2: Set Up Pipenv Environment**

Install Python 3.9 and AgentNeo in the environment:
```bash
pipenv install --python 3.9 agentneo
```

Activate the Pipenv shell:
```bash
pipenv shell
```

## 2. macOS Installation

### 2.1. Using pip and Virtualenv

**Step 1: Install Python 3.9 via Homebrew**
```bash
brew install python@3.9
```

**Step 2: Set Up Virtual Environment**

Create a virtual environment:
```bash
python3.9 -m venv agentneo-env
```

Activate the environment:
```bash
source agentneo-env/bin/activate
```

Install AgentNeo:
```bash
pip install agentneo
```

### 2.2. Using Conda

**Step 1: Install Miniconda**
```bash
brew install --cask miniconda
```

**Step 2: Set Up Conda Environment**

Create and activate a conda environment:
```bash
conda create --name agentneo-env python=3.9
conda activate agentneo-env
```

Install AgentNeo:
```bash
pip install agentneo
```

### 2.3. Using Pipenv

**Step 1: Install Pipenv**
```bash
brew install pipenv
```

**Step 2: Set Up Pipenv Environment**

Install Python 3.9 and AgentNeo:
```bash
pipenv install --python 3.9 agentneo
```

Activate Pipenv:
```bash
pipenv shell
```

## 3. Linux Installation

### 3.1. Using pip and Virtualenv (Ubuntu/Debian)

**Step 1: Install Python 3.9**
```bash
sudo apt update
sudo apt install python3.9 python3.9-venv python3-pip
```

**Step 2: Set Up Virtual Environment**

Create a virtual environment:
```bash
python3.9 -m venv agentneo-env
```

Activate the environment:
```bash
source agentneo-env/bin/activate
```

Install AgentNeo:
```bash
pip install agentneo
```

### 3.2. Using Pipenv

**Step 1: Install Pipenv**
```bash
sudo apt install pipenv
```

**Step 2: Set Up Pipenv Environment**

Install Python 3.9 and AgentNeo:
```bash
pipenv install --python 3.9 agentneo
```

Activate the environment:
```bash
pipenv shell
```
