🏗️ Professional Git & DevOps Cheat Sheet
1. Global Setup & Identity
These should be configured once on every new environment (e.g., your Lenovo ThinkPad P1 or a new RHEL server).

# Identity
git config --global user.name "Slimane"
git config --global user.email "your.email@example.com"

# Standardize branch naming to 'main'
git config --global init.defaultBranch main

# Handle line endings (Crucial for DevOps/Middleware on Linux)
git config --global core.autocrlf input

# UI and Pruning
git config --global color.ui auto
git config --global fetch.prune true