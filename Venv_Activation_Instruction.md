# Local Project Setup & Environment Activation

This guide outlines the steps to correctly initialize the environment and activate the local Conda interpreter for this project. Use these steps if the environment is not automatically recognized by VS Code or when starting a new terminal session.

## 1. Prerequisites
* **Anaconda/Miniconda** must be installed at `C:/Anaconda3` (or your specific install path).
* **VS Code** with the Python extension installed.

## 2. Terminal Activation Sequence
Copy and paste these commands into your VS Code PowerShell terminal to initialize and activate the environment:

```powershell
# Step A: Enable script execution for the current session
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process

# Step B: Initialize the Conda shell hook for PowerShell
& "C:/Anaconda3/Scripts/conda.exe" "shell.powershell" "hook" | Out-String | Invoke-Expression

# Step C: Activate the project-specific environment by path
conda activate d:\Projects\LLM_RAG_Projects\.conda